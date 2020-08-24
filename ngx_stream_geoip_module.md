基于 IP 地址 匹配 MaxMind GeoIP 二进制文件，读区IP所在的地域信息

#### 使用场景

- 区别国内外做 HTTPS 访问规则
- 区别国内城市地域作 HTTPS 访问规则

##### 安装模块

```
 ~]# yum install nginx-module-geoip # 需配置好 nginx.repo
```

#### 配置 nginx.conf 加载模块

```
~]# vim /etc/nginx/nginx.conf
load_module "modules/ngx_http_geoip_module.so";
load_module "modules/ngx_stream_geoip_module.so";
user  nginx;
```

未完待续
