#### 场景

- url访问跳转，页面跳转，兼容性支持，展示效果
- SEO 优化
- 后台维护、流量转发
- 安全

```
rewrite ^(.*) /pages/maintain.html break; # 挂维护页
```

```
server {
        listen 0.0.0.0:18080;
        server_name  0.0.0.0;
        root /opt/app/html;

        location ~ ^/break {
                rewrite ^/break /test/ break;
        }

        location ~ ^/last {
                rewrite ^/last /test/ last;
        }

        location /test/ {
                default_type application/json;
                return 200 '{"status":"success"}';
        }

        access_log /opt/app/logs/access.log main;
        error_log  /opt/app/logs/error.log;
}
```

```
]# curl 127.0.0.1:18080/test/
{"status":"success"}[root@linux-node01 conf.d]# curl 127.0.0.1:18080/last/
{"status":"success"}[root@linux-node01 conf.d]# curl 127.0.0.1:18080/break/
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.18.0</center>
</body>
</html>
```

#### seo

简化访问路径,方便搜索引擎进行收录

```
~]# cat /opt/app/html/course/01/02/course_03.html
test page
```
```
~]# curl 127.0.0.1:18080/course/01/02/course_03.html # 重写前的访问路径
test page
```

```
server {
        listen 0.0.0.0:18080;
        server_name  0.0.0.0;
        root /opt/app/html;

        location / {
                rewrite ^/course-(\d+)-(\d+)-(\d+)\.html$ /course/$1/$2/course_$3.html break;
        }
        access_log /opt/app/logs/access.log main;
        error_log  /opt/app/logs/error.log;
}
```

```
~]# curl 127.0.0.1:18080/course-01-02-03.html  # 重写后的访问路径      
test page
```
