---
ref: Framework-Engine
judul: Framework Engine
title: 'Framework Engine'
description: 'Framework Engine: ASP.NET WebAPI dengan enhancement untuk dynamic route prefix, JWT authentication, dan Swagger UI — semua dikonfigurasi via Environment Variable.'
tags: [ide]
category: Ide
category_url: ide
---

# Framework Engine

Saya membuat _ASP.NET WebAPI_ dengan beberapa _enhancement_, sehingga system yang saya buat menjadi lebih fleksibel:

- Setting dari Environment
- Dynamic route prefix
- JWT via Bearer di Swagger UI
- Semua config terpusat di _Global_Data_FRM_

## Setting di load dari Environment

- nilai Setting di load dari Environment {bukan dari file config}
- saat running di Linux, bisa dilakukan pada file _.service_

```
[Service]
Environment=Swagger_Prefix=docsDEV
Environment=ApiPrefix=apiDEV
Environment=Jwt_Key=abcXYZ
Environment=Jwt_Issuer=xyzABC
```

- saat running di Windows {misalnya saat proses development}, bisa dilakukan pada file _.bat_

```
set Swagger_Prefix=docsDEV
set ApiPrefix=apiDEV
set Jwt_Key=abcXYZ
set Jwt_Issuer=xyzABC
```

## Global_Data_FRM

- class `static` yang bertugas membaca nilai dari Environment
- menjadi **satu titik referensi** untuk semua Setting yang dibutuhkan oleh Framework
- digunakan oleh `SwaggerExtensions`, `RoutePrefixExtensions`, dan `AppOtherExtensions`

```
Environment Variable  →  Global_Data_FRM  →  Extensions  →  App
```

Properti yang dibaca dari Environment:

| Properti         | Environment Variable | Keterangan                          |
| ---------------- | -------------------- | ----------------------------------- |
| `Swagger_Prefix` | `Swagger_Prefix`     | Prefix URL untuk Swagger UI         |
| `Api_Prefix`     | `ApiPrefix`          | Prefix route untuk semua Controller |
| `Jwt_Key`        | `Jwt_Key`            | Secret key untuk signing JWT        |
| `Jwt_Issuer`     | `Jwt_Issuer`         | Issuer dan Audience untuk JWT       |

> **catatan:** semua Extensions tidak membaca Environment secara langsung — selalu melalui `Global_Data_FRM`

## Route pada Controller

- Route pada Controller, tidak `hardcoded`, tetapi nilainya suatu Setting
    - tidak static, tetapi dynamic
    - mudah diubah saat _runtime_
    - bisa "aliasing"
    - daripada selalu _hardcoded_ `/api`
    - bisa menjadi:
        - _/api_
        - _/apiDEV_
        - _/apiCompanyX_
        - _/apiCompanyY_
        - _/apiCompanyZ_
- behaviour Route pada _BackEnd_ di atas, akan efek ke _FrontEnd_
    - FrontEnd juga mempunyai Setting terhadap suatu `Url`
        - file .js untuk setting ini
        - fetch ke file .js tersebut
        - simpan ke LocalStorage
    - semua coding pada FrontEnd, saat akses ke BackEnd -- harus selalu aware terhadap nilai Setting tersebut

`BackEnd` - Controller:

```c#
namespace OurFramework.Controllers
{
    [Route("[controller]")]
    [ApiController]
    public class XyzController : ControllerBase
```

> catatan:
> akan ada Extensions yang akan melakukan kombinasi
>
> - prefix yang diambil dari Setting
> - nama Controller

`Frontend` - file _app-settings.json_:

```javascript
{
    "Endpoint": "http://localhost:9091/apiDEV"
}
```

`Frontend` - fetch _app-settings.json_:

```javascript
const response = await fetch('app-settings.json')
```

## RoutePrefixConvention

- masalah: Controller menggunakan `[Route("[controller]")]` — tanpa prefix
- solusi: inject prefix secara dinamis ke **semua Controller** via `IApplicationModelConvention`
- hasilnya: prefix dari `Global_Data_FRM.Api_Prefix` otomatis digabung dengan nama Controller

```
[Route("[controller]")]  +  ApiPrefix  →  /apiDEV/Xyz
```

Cara kerjanya:

```c#
public class RoutePrefixConvention : IApplicationModelConvention
{
    private readonly AttributeRouteModel _routePrefix;

    public RoutePrefixConvention(string prefix)
    {
        _routePrefix = new AttributeRouteModel(new RouteAttribute(prefix));
    }

    public void Apply(ApplicationModel application)
    {
        foreach (var controller in application.Controllers)
        {
            foreach (var selector in controller.Selectors.Where(s => s.AttributeRouteModel != null))
            {
                selector.AttributeRouteModel = AttributeRouteModel.CombineAttributeRouteModel(_routePrefix, selector.AttributeRouteModel);
            }
        }
    }
}
```

Didaftarkan melalui `RoutePrefixExtensions`:

```c#
public static class RoutePrefixExtensions
{
    public static void UseCustomAddControllers(this IServiceCollection services, IConfiguration config)
    {
        var routePrefix = Global_Data_FRM.Api_Prefix;

        services.AddControllers(options =>
        {
            options.Conventions.Insert(0, new RoutePrefixConvention(routePrefix));
        }).AddJsonOptions(options =>
        {
            options.JsonSerializerOptions.PropertyNamingPolicy = null;
            options.JsonSerializerOptions.PropertyNameCaseInsensitive = true;
        });
    }
}
```

> **catatan:** `PropertyNamingPolicy = null` berarti nama JSON property mengikuti nama C# property apa adanya (tidak di-camelCase)

## Extensions C#

dibuat beberapa Extensions:

- SwaggerExtensions
- RoutePrefixExtensions
- AppOtherExtensions

yang akan diload oleh `Program.cs`

```c#
var builder = WebApplication.CreateBuilder(args);

builder.Services.UseCustomPreparation(builder.Configuration);
builder.Services.UseCustomAddControllers(builder.Configuration);
```

## Authentication ditambahkan beberapa nilai Setting untuk `JwtBearer`

```c#
public static class AppOtherExtensions
{
    public static void UseCustomPreparation(this IServiceCollection services, IConfiguration config)
    {
        services.AddMemoryCache();
        services.AddAuthentication(options =>
        {
            options.DefaultAuthenticateScheme = JwtBearerDefaults.AuthenticationScheme;
            options.DefaultChallengeScheme = JwtBearerDefaults.AuthenticationScheme;
        })
        .AddJwtBearer(options =>
        {
            options.TokenValidationParameters = new TokenValidationParameters
            {
                ValidateIssuer = true,
                ValidateAudience = true,
                ValidateLifetime = false,  // Tidak usah dilakukan Validasi Lifetime di sini, karena Lifetime akan dicheck pada function getCurrentUser()
                ValidateIssuerSigningKey = true,
                ValidIssuer = Global_Data_FRM.Jwt_Issuer,
                ValidAudience = Global_Data_FRM.Jwt_Issuer,
                IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(Global_Data_FRM.Jwt_Key))
            };
        });
    }
}
```

## Enhancement pada UI Swagger

Saya ingin pada UI Swagger, kita bisa input nilai `Token`. Saya memerlukan tambahan _coding_ berikut:

```c#
public static class SwaggerExtensions
{
    private static string _Name = "Framework Engine";

    public static void AddCustomSwagger(this IServiceCollection services)
    {
        services.AddSwaggerGen(options =>
        {
            options.SwaggerDoc("v1", new() { Title = _Name + ": " + App_Signature.Signature, Version = "v1" });

            // Add JWT Bearer
            options.AddSecurityDefinition("Bearer", new Microsoft.OpenApi.OpenApiSecurityScheme
            {
                Name = "Authorization",
                Type = Microsoft.OpenApi.SecuritySchemeType.Http,
                Scheme = "bearer",
                BearerFormat = "JWT",
                In = Microsoft.OpenApi.ParameterLocation.Header,
                Description = "Enter 'Bearer' [space] and then your valid token in the text input below.\r\n\r\nExample: \"Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6...\""
            });

            options.AddSecurityRequirement(document => new OpenApiSecurityRequirement
            {
                [new OpenApiSecuritySchemeReference("Bearer", document)] = []
            });


            var xmlFile = $"{Assembly.GetExecutingAssembly().GetName().Name}.xml";
            var xmlPath = Path.Combine(AppContext.BaseDirectory, xmlFile);
            options.IncludeXmlComments(xmlPath);
        });
    }

    public static void UseCustomSwaggerUI(this IApplicationBuilder x, IConfiguration config)
    {
        var swaggerPrefix = Global_Data_FRM.Swagger_Prefix + "2";

        x.UseSwagger(options =>
        {
            options.RouteTemplate = $"{swaggerPrefix}/{{documentName}}/swagger.json";
            options.OpenApiVersion = Microsoft.OpenApi.OpenApiSpecVersion.OpenApi3_1;
        });

        x.UseSwaggerUI(options =>
        {
            options.RoutePrefix = Global_Data_FRM.Swagger_Prefix;

            options.SwaggerEndpoint($"/{swaggerPrefix}/v1/swagger.json", _Name + " v1");
        });
    }
}
```
