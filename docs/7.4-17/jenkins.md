# Proxy
> 如果有用 Proxy 伺服器
```
server {
    listen      80;
    listen      [::]:80;
    server_name jenkins.example.com;

    location / {
        return 301 https://jenkins.example.com$request_uri;
    }
}
server {
    listen                  443 ssl http2;
    listen                  [::]:443 ssl http2;
    server_name jenkins.example.com;
    location / {
            proxy_pass http://192.168.xx.x:8080;
            proxy_read_timeout  90;
            proxy_set_header X-Forwarded-Host $host:$server_port;
            proxy_set_header X-Forwarded-Server $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_set_header X-Real-IP $remote_addr;
    }
}
```
