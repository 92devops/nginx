该ngx_http_sub_module模块是一个过滤器，通过将一个指定的字符串替换为另一个指定的字符串来修改响应。

默认情况下未构建此模块，应使用--with-http_sub_module 配置参数启用它。

```
~]# curl  http://127.0.0.1:18088/sub.html
This is a sub page, show you sub !
```

```
location / {
    root /opt/app/html;
    index index.html index.htm;
    sub_filter_once off;
    sub_filter 'sub' 'SUB';
}
```

```
~]# nginx -s reload
~]# curl  http://127.0.0.1:18088/sub.html     
This is a SUB page, show you SUB !
```

- `sub_filter_once`：查找要替换一次还是重复替换的某个字符串
- `sub_filter`：设置要替换的字符串和替换字符串
