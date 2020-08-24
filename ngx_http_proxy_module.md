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
    #include proxy_params;
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

#### 代理缓存服务

```
http {
    ...
    proxy_cache_path /var/cache/nginx/proxy_temp/cache levels=1:2 keys_zone=nginx_cache:10m max_size=10g inactive=60m use_temp_path=off;

    server {
      ...
      if ($request_uri ~ ^/(url3|login|register|password\/reset)) {
            set $cookie_nocache 1;
      }
      location /app {
              #limit_req zone=one burst=5;
              proxy_pass http://backend;
              proxy_cache nginx_cache;
              proxy_cache_valid  200 304 12h;
              proxy_cache_valid any 10m;
              proxy_cache_key $host$uri$is_args$args;
              proxy_no_cache $cookie_nocache $arg_nocache $arg_comment;
              proxy_no_cache $http_pragma $http_authorization;
              add_header Nginx-Cache "$upstream_cache_status";
              proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
              include proxy_params;
      }
    }

}
```
