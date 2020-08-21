默认情况下未构建此模块，应使用--with-http_stub_status_module 配置参数启用它 。

```
server {
  '''
  location = /basic_status {
          stub_status;
  }
  '''
}
```

```
curl 127.0.0.1:18088/basic_status
Active connections: 1
server accepts handled requests
50 50 47
Reading: 0 Writing: 1 Waiting: 0
```

- `Active connections`：当前活动的客户端连接数，包括Waiting连接数
- `accepts`：接受的客户端连接总数
- `handled`：已处理的连接总数。通常，参数值与accepts 相同
- `requests`：客户端请求总数
- `Reading`：nginx正在读取请求头部的当前连接数
- `Writing`：nginx正在将响应写回到客户端的当前连接数
- `Waiting`：当前等待请求的空闲客户端连接数
