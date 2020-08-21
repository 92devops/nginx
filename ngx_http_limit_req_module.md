用于限制每个已定义 key 的请求处理速率，特别是来自单个 IP 地址请求的处理速率。限制机制采用了 leaky bucket （漏桶算法）方法完成。

```

http {
    limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s; #
    ...
    server {
        ...
        location /app/ {
            #limit_req zone=one burst=5; #平均每秒最多允许不超过1个请求，并且突发不超过5个请求

        }
```

验证：`ab -n 50 -c 20 http://127.0.0.1:18088/app/`
