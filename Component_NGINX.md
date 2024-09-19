<p align="center">
  <img src="images/LernaAI.png" alt="Lerna AI" />
</p>

# Lerna AI nginx Gateway
Lerna AI uses nginx as an SSL termination gateway for each service that exposes REST API.

## Execution

nginx runs as service on major unix distributions and supports multiple platforms [[1]](#references).

## Configuration

### Dashboard
```shell
server {
     server_name my.eu-west-1.lerna.ai;
     gzip on;
     gzip_types text/plain application/xml application/javascript text/javascript text/css;

     root /var/www/dashboard;

     index index.html index.htm;

     add_header Access-Control-Allow-Origin "*";

     location / {
          try_files $uri $uri/ /index.html;
     }

    listen 443 ssl;
    ssl_certificate /etc/sshkeys/eu-west-1.lerna.ai/fullchain.pem;
    ssl_certificate_key /etc/sshkeys/eu-west-1.lerna.ai/privkey.pem;
}

```

### Config Server

```shell
server {
    listen 443 ssl;
    server_name config.lerna.ai;
    ssl_certificate /etc/sshkeys/config.lerna.ai/fullchain.pem;
    ssl_certificate_key /etc/sshkeys/config.lerna.ai/privkey.pem;

    location /health {
        access_log off;
        return 200 'Config Proxy Server: OK!';
        add_header Content-Type text/plain;
    }

    add_header 'Access-Control-Allow-Origin' '*';

    location / {
        proxy_pass http://127.0.0.1:8088/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header   X-Real-IP          $remote_addr;
        proxy_set_header   X-Forwarded-Proto  $scheme;
        proxy_set_header   X-Forwarded-For    $proxy_add_x_forwarded_for;
        proxy_cache_bypass $http_upgrade;
    }
}
```

### FL-API

```shell
server {
    listen 5000 ssl;
    server_name api.eu-west-1.lerna.ai;

    ssl_certificate /etc/sshkeys/eu-west-1.lerna.ai/fullchain.pem;
    ssl_certificate_key /etc/sshkeys/eu-west-1.lerna.ai/privkey.pem;

    location /health {
        access_log off;
        return 200 'FL Proxy Server: OK!';
        add_header Content-Type text/plain;
    }

    location / {

        if ($request_method = 'OPTIONS') {
            add_header 'Access-Control-Allow-Origin' '*';
            add_header 'Access-Control-Allow-Credentials' 'true';
            add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
            add_header 'Access-Control-Allow-Headers' 'DNT,Authorization,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';
            add_header 'Access-Control-Max-Age' 1728000;
            add_header 'Content-Type' 'text/plain charset=UTF-8';
            add_header 'Content-Length' 0;
            return 204;
        }

        proxy_hide_header Access-Control-Allow-Origin;
        add_header Access-Control-Allow-Origin '*' always;
        add_header 'Access-Control-Allow-Credentials' 'true';
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
        add_header 'Access-Control-Allow-Headers' 'DNT,Authorization,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';


        proxy_pass http://127.0.0.1:8088/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header   X-Real-IP          $remote_addr;
        proxy_set_header   X-Forwarded-Proto  $scheme;
        proxy_set_header   X-Forwarded-For    $proxy_add_x_forwarded_for;
        proxy_cache_bypass $http_upgrade;
    }
}

```

### MPC Gateway

```shell
server {
    listen 8080 ssl;
    server_name api.eu-west-1.lerna.ai;

    ssl_certificate /etc/sshkeys/eu-west-1.lerna.ai/fullchain.pem;
    ssl_certificate_key /etc/sshkeys/eu-west-1.lerna.ai/privkey.pem;

    location /health {
        access_log off;
        return 200 'MPC GW Proxy Server: OK!';
        add_header Content-Type text/plain;
    }

    location / {

        if ($request_method = 'OPTIONS') {
            add_header 'Access-Control-Allow-Origin' '*';
            add_header 'Access-Control-Allow-Credentials' 'true';
            add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
            add_header 'Access-Control-Allow-Headers' 'DNT,Authorization,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';
            add_header 'Access-Control-Max-Age' 1728000;
            add_header 'Content-Type' 'text/plain charset=UTF-8';
            add_header 'Content-Length' 0;
            return 204;
        }

        proxy_hide_header Access-Control-Allow-Origin;
        add_header Access-Control-Allow-Origin '*' always;
        add_header 'Access-Control-Allow-Credentials' 'true';
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
        add_header 'Access-Control-Allow-Headers' 'DNT,Authorization,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';

        proxy_pass http://127.0.0.1:8081/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header   X-Real-IP          $remote_addr;
        proxy_set_header   X-Forwarded-Proto  $scheme;
        proxy_set_header   X-Forwarded-For    $proxy_add_x_forwarded_for;
        proxy_cache_bypass $http_upgrade;
    }
}
```

## Requires

* Dashboard (port 443)

* Config Server (port 8088) (currently exposed by FL-API application)

* FL-API (port 8088)

* MPC Gateway (port 8081)

* SSL Certificate signed by CA (e.g. LetsEncrypt)

## Required by

* Host applications of Lerna SDK

* Dashboard UI

## References

[1] [nginx official website](https://nginx.org/)
