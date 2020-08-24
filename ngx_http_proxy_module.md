#### 反向代理

```
location /app {
    proxy_pass       http://localhost:8000;
    proxy_redirect default;

    proxy_set_header Host $http_host;
    proxy_set_header X-Real-IP $remote_addr;

    proxy_connect_timeout 30;
    proxy_send_timeout 60;
    proxy_read_timeout 60;

    proxy_buffer_size 32k;
    proxy_buffering on;
    proxy_buffers 4 128k;
    proxy_busy_buffers_size 256k;
    proxy_max_temp_file_size 256k;
}
```

#### 正向代理

应用场景一：我们在真实服务器上设置访问控制然后由正向代理服务器代替我们去访问

```
// 真实服务器
location / {
    ...
    if ( $http_x_forwarded_for !~* "^117\.xxx\.xxx\.88") {
        return 403;
    }
```

```
// 正向代理服务器
server {
    ...
    resolver 114.114.114.114;

    location / {
        ...
        proxy_pass http://$http_host$request_uri;
    }
}
```
