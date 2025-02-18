---
title: nginx
description: 
published: true
date: 2025-02-18T10:51:52.927Z
tags: 
editor: markdown
dateCreated: 2025-02-15T20:11:24.257Z
---


# NginX Commands

## Basic Commands

```bash
sudo systemctl start nginx - start NginX
sudo systemctl stop nginx - stop NginX
sudo systemctl restart nginx - restart NginX
sudo systemctl reload nginx - reload without downtime
sudo systemctl status nginx - check status
sudo nginx -t - check configuration
```

## Configuration File Locations

```bash
- Main configuration file: `/etc/nginx/nginx.conf`
- Additional configuration files: `/etc/nginx/conf.d/` or `/etc/nginx/sites-available/` (symlink to `/etc/nginx/sites-enabled/`)
```

# Basic Configuration Example

```bash
user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

events {
    worker_connections 1024;
}

http {
    include /etc/nginx/mime.types;
    default_type application/octet-stream;
    sendfile on;
    keepalive_timeout 65;
    include /etc/nginx/conf.d/*.conf;
}
```

# Server Block Example=====

```bash
server {
    listen 80;
    server_name example.com www.example.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    error_page 404 /404.html;
        location = /40x.html {
    }

    error_page 500 502 503 504 /50x.html;
        location = /50x.html {
    }
}
```

## SSL Configuration Example

```bash
sudo yum install epel-release
sudo yum install certbot python3-certbot-nginx
sudo certbot --nginx - install SSL Certificate
sudo certbot renew --dry-run - check SSL renewal cronjob

server {
    listen 443 ssl;
    server_name example.com www.example.com;

    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers on;
    ssl_ciphers 'ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256';

    ssl_session_timeout 1d;
    ssl_session_cache shared:SSL:10m;
    ssl_session_tickets off;

    ssl_stapling on;
    ssl_stapling_verify on;

    resolver 8.8.8.8 8.8.4.4 valid=300s;
    resolver_timeout 5s;

    add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload" always;
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## Common Directives

```bash
- `listen`: Specifies the port and IP address for the server to listen on.
- `server_name`: Defines the domain names for the server.
- `location`: Defines how to process requests that match a given pattern.
- `proxy_pass`: Forwards requests to a proxied server.
- `root`: Specifies the root directory for serving files.
- `index`: Defines the default file to serve.
- `error_page`: Specifies custom error pages.
- `rewrite`: Defines URL rewriting rules.
```


## Location Block Examples

### Match exact path

```bash
location = /exact {
    return 200 'Exact match';
}
```

### Match path prefix

```bash
location /prefix {
    return 200 'Prefix match';
}
```

### Match by regex

```bash
location ~ \.php$ {
    fastcgi_pass 127.0.0.1:9000;
    fastcgi_index index.php;
    include fastcgi_params;
}
```

### Match any request

```bash
location / {
    try_files $uri $uri/ =404;
}
```

## Load Balancing

```bash
upstream backend {
    server backend1.example.com;
    server backend2.example.com;
}

server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## Rate Limiting

```bash
http {
    limit_req_zone $binary_remote_addr zone=mylimit:10m rate=10r/s;

    server {
        listen 80;
        server_name example.com;

        location / {
            limit_req zone=mylimit burst=20 nodelay;
            proxy_pass http://localhost:3000;
        }
    }
}
```

## Caching

```bash
http {
    proxy_cache_path /data/nginx/cache keys_zone=my_cache:10m;

    server {
        listen 80;
        server_name example.com;

        location / {
            proxy_cache my_cache;
            proxy_pass http://localhost:3000;
            add_header X-Proxy-Cache $upstream_cache_status;
        }
    }
}
```
