---
ref: Framework-Engine
judul: Framework Engine
title: 'Framework Engine'
description: 'ASP.NET WebAPI with several enhancements for a more flexible system'
tags: [idea]
category: Idea
category_url: idea
---

# Framework Engine

I built an _ASP.NET WebAPI_ with several _enhancements_, making the system more flexible:

- Setting from Environment
- Dynamic route prefix
- JWT via Bearer at Swagger UI
- Every config at _Global_Data_FRM_

## Settings loaded from Environment

- Setting values are loaded from Environment {not from a config file}
- when running on Linux, this can be done in the _.service_ file

```
[Service]
Environment=Swagger_Prefix=docsDEV
Environment=ApiPrefix=apiDEV
Environment=Jwt_Key=abcXYZ
Environment=Jwt_Issuer=xyzABC
```

- when running on Windows {for example during development}, this can be done in a _.bat_ file

```
set Swagger_Prefix=docsDEV
set ApiPrefix=apiDEV
set Jwt_Key=abcXYZ
set Jwt_Issuer=xyzABC
```

## Global_Data_FRM

- a `static` class responsible for reading values from the Environment
- serves as the **single reference point** for all Settings needed by the Framework
- used by `SwaggerExtensions`, `RoutePrefixExtensions`, and `AppOtherExtensions`

```
Environment Variable  →  Global_Data_FRM  →  Extensions  →  App
```

Properties read from the Environment:

| Property         | Environment Variable | Description                      |
| ---------------- | -------------------- | -------------------------------- |
| `Swagger_Prefix` | `Swagger_Prefix`     | URL prefix for Swagger UI        |
| `Api_Prefix`     | `ApiPrefix`          | Route prefix for all Controllers |
| `Jwt_Key`        | `Jwt_Key`            | Secret key for signing JWT       |
| `Jwt_Issuer`     | `Jwt_Issuer`         | Issuer and Audience for JWT      |

> **note:** all Extensions do not read the Environment directly — they always go through `Global_Data_FRM`

## Route on Controller

- the Route on a Controller is not `hardcoded` — its value comes from a Setting
    - not static, but dynamic
    - easy to change at _runtime_
    - supports "aliasing"
    - instead of always hardcoding `/api`
    - it can become:
        - _/api_
        - _/apiDEV_
        - _/apiCompanyX_
        - _/apiCompanyY_
        - _/apiCompanyZ_
- this _BackEnd_ Route behaviour has an effect on the _FrontEnd_
    - FrontEnd also has a Setting for a `Url`
        - a .js file for this setting
        - fetch that .js file
        - store to LocalStorage
    - all FrontEnd code, when accessing the BackEnd — must always be aware of that Setting value

`BackEnd` - Controller:

```c#
namespace OurFramework.Controllers
{
    [Route("[controller]")]
    [ApiController]
    public class XyzController : ControllerBase
```

> note:
> there will be an Extension that combines
>
> - the prefix taken from the Setting
> - the Controller name

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

- problem: Controller uses `[Route("[controller]")]` — without a prefix
- solution: dynamically inject a prefix into **all Controllers** via `IApplicationModelConvention`
- result: the prefix from `Global_Data_FRM.Api_Prefix` is automatically combined with the Controller name

```
[Route("[controller]")]  +  ApiPrefix  →  /apiDEV/Xyz
```

How it works:

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

Registered via `RoutePrefixExtensions`:

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

> **note:** `PropertyNamingPolicy = null` means JSON property names follow the C# property names as-is (not camelCased)

## Extensions C#

Several Extensions are created:

- SwaggerExtensions
- RoutePrefixExtensions
- AppOtherExtensions

which are loaded by `Program.cs`

```c#
var builder = WebApplication.CreateBuilder(args);

builder.Services.UseCustomPreparation(builder.Configuration);
builder.Services.UseCustomAddControllers(builder.Configuration);
```

## Authentication — additional Settings for `JwtBearer`

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
                ValidateLifetime = false,  // No need to validate Lifetime here, because Lifetime will be checked in the getCurrentUser() function
                ValidateIssuerSigningKey = true,
                ValidIssuer = Global_Data_FRM.Jwt_Issuer,
                ValidAudience = Global_Data_FRM.Jwt_Issuer,
                IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(Global_Data_FRM.Jwt_Key))
            };
        });
    }
}
```

## Swagger UI Enhancement

I wanted the Swagger UI to support entering a `Token` value. I needed the following additional _code_:

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
