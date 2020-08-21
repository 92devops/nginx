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
log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                  '$status $body_bytes_sent "$http_referer" '
                  '"$http_user_agent" "$http_x_forwarded_for" "$upstream_addr"';
```


```
~]# LANG="zh_CN.UTF-8"
~]# goaccess -f /opt/app/logs/access.log
```

```
~]# cat goaccess.sh
#cat /root/goaccess.sh
#!/bin/bash

LANG="zh_CN.UTF-8" bash -c "/usr/local/bin/goaccess /opt/app/logs/access.log  -o /opt/app/html/report.html -p /usr/local/etc/goaccess/goaccess.conf"

```
