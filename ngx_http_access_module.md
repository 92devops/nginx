该ngx_http_access_module模块允许限制对某些客户端地址的访问.

```
location = /basic_status {
    stub_status;
    deny  192.168.1.1;
    allow 192.168.1.0/24;
    deny  all;
}
```
