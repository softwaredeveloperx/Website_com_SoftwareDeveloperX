---
ref: Infrastructure__Server_CI_CD__multi_Tenant
judul: 'Infrastructure {Server, CI/ CD, multi Tenant}'
title: 'Infrastructure {Server, CI/ CD, multi Tenant}'
description: ''
tags: [idea]
category: Idea
category_url: idea
---

# Infrastructure {Server, CI/ CD, multi Tenant}

saya develop System {Product} dengan component:

- BackEnd --> Framework
- BackEnd --> Engine {plugin}
- FrontEnd

Environment {seperti biasa} dalam bentuk:

- DEV
- Test
- PROD

Selanjutnya, PROD dipecah menjadi beberapa `cubicle`:

- Tenant 1
- Tenant A
- Tenant X
- ...
- Tenant n

Kombinasi di atas:

- Tenant 1
    - BackEnd --> Framework Engine
    - BackEnd --> App Engine {plugin}
    - FrontEnd
- Tenant A
    - BackEnd --> Framework
    - BackEnd --> Engine {plugin}
    - FrontEnd

## Server

pada server, saya punya beberapa file

Folder: /etc/systemd/system

```
Product_env_dev.service
Product_env_test.service
Product_Tenant_1.service
Product_Tenant_A.service
Product_Tenant_X.service
```

Folder: /etc/nginx/conf.d

```
nginx-handle-env_dev.conf
nginx-handle-env_test.conf
nginx-handle-Tenant_1.conf
nginx-handle-Tenant_A.conf
nginx-handle-Tenant_X.conf
```

File: .service:

```
[Unit]
Description=Product - Tenant X
After=network.target

[Service]
Type=simple
WorkingDirectory=/var/www-custom/Product_Tenant_X-Framework-Engine
ExecStart=/usr/bin/dotnet /var/www-custom/Product_Tenant_X-Framework-Engine/Framework-Engine.dll
Restart=always
RestartSec=10
KillSignal=SIGINT
SyslogIdentifier=Product_Tenant_X
User=nginx
Group=nginx
Environment=ASPNETCORE_ENVIRONMENT=Development
Environment=ASPNETCORE_URLS=http://localhost:9001
Environment="IdentityDB=Server=DatabaseServer-Penting-banget-lho;Database=Product_Tenant_X_Framework;User ID=userKita;Password=pwdKita;Encrypt=false;Connect Timeout=3000;pooling=false;MultipleActiveResultSets=True;"
Environment=Jwt_Key=hehehe--Kereeeennn
Environment=Jwt_Issuer=SoftwareDevelopeRx.com
Environment=Swagger_Prefix=docs
Environment=ApiPrefix=api
TimeoutStartSec=30
TimeoutStopSec=30

[Install]
WantedBy=multi-user.target
```

File: nginx .conf

```
server {
    listen 80;
    listen [::]:80;
    server_name tenantX.SoftwareDevelopeRx.com;

    client_max_body_size 100M;
    root /var/www-custom/Product_Tenant_X-App-UI;

    location / {
        index index.html index.htm;
        try_files $uri $uri/ /index.html;
    }

    location /api {
        proxy_pass http://localhost:9001/api;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep-alive;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_connect_timeout 1200;
        proxy_send_timeout 1200;
        proxy_read_timeout 1200;
        send_timeout 1200;
        fastcgi_buffers 4 256k;
        fastcgi_buffer_size 256k;
    }

    location /docs {
        proxy_pass http://localhost:9001/docs;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep-alive;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_connect_timeout 1200;
        proxy_send_timeout 1200;
        proxy_read_timeout 1200;
        send_timeout 1200;
        fastcgi_buffers 4 256k;
        fastcgi_buffer_size 256k;
    }

    location /framework {
        alias /var/www-custom/Product_Tenant_X-Framework-UI;
        try_files $uri $uri/ /framework/index.html;
    }

    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;
}
```

Folder: /var/www-custom

SubFolder:

- Product_Tenant_X-App-UI
- Product_Tenant_X-Framework-UI
- Product_Tenant_X-Framework-Engine
