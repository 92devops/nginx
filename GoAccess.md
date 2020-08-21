## 安装

安装GoAccess非常简单。只需使用以下命令下载，解压并编译它

```
 ~]# yum install -y GeoIP-devel ncursesw-devel
 ~]# wget https://tar.goaccess.io/goaccess-1.4.tar.gz
 ~]# tar -xzvf goaccess-1.4.tar.gz -C /usr/local/
 ~]# ln -sv /usr/local/goaccess-1.4/ /usr/local/goaccess
 ~]# cd /usr/local/goaccess
 goaccess]# ./configure --enable-utf8 --enable-geoip=legacy
 goaccess]# make
 goaccess]# make install
```

## 使用

```
log_format main '[$time_local] $remote_addr $server_name "$request" '
                '$status $body_bytes_sent "$http_referer" '
                '"$http_user_agent" "$http_x_forwarded_for" '
                '$upstream_addr $request_time $upstream_response_time';
```

为了让 GoAccess 能适配这个格式，需要将 goaccess.conf 中修改成如下格式 `%^[%d:%t %^] %h %v "%r" %s %b "%R" "%u"`

```
~]# LANG="zh_CN.UTF-8"
~]# goaccess -f /opt/app/logs/access.log
```

```
cat  >>/usr/local/etc/goaccess/goaccess.conf<<EOF
time-format %H:%M:%S
date-format %d/%b/%Y
#NCSA Combined Log Format
log-format %h %^[%d:%t %^] "%r" %s %b "%R" "%u"
EOF
```

```
~]# cat goaccess.sh
#cat /root/goaccess.sh
#!/bin/bash

LANG="zh_CN.UTF-8" bash -c "/usr/local/bin/goaccess /opt/app/logs/access.log  -o /opt/app/html/report.html -p /usr/local/etc/goaccess/goaccess.conf"

```
