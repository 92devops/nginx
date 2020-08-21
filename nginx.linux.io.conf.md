```
upstream backend {
        server  172.31.0.7:80 max_fails=3 fail_timeout=3s;
        server  172.31.0.8:80 max_fails=3 fail_timeout=3s;

}

server {
        listen 0.0.0.0:18088;
        server_name  nginx.linux.io;
        location / {
            root /opt/app/html;
            index index.html index.htm;
        }
        location /bbs/ {
            root /opt/app/html/;
        }

        location /web/ {
            alias /opt/app/html/;
        }

        error_page   500 502 503 504  404  /50x.html;
        location = /50x.html {
            root   /opt/app/error;
        }

        location /app {
                proxy_pass http://backend; # 资源路径为：/DocRoot/app/
        }
        access_log /opt/app/logs/access.log main;
        error_log  /opt/app/logs/error.log;
}
```
