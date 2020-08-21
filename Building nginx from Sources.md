
## NGINX 编译安装

编译安装 nginx， 操作系统为CentOS 7.6.1810 X86_64

#### 编译环境准备


- 如果用ssl模块，要安装openssl开发包;如果用url重写模块，要安装pcre的开发包;默认有可能都没安装

~]# yum -y install openssl-devel pcre-devel zlib-devel

- 安装编译环境包组

~]# yum -y groupinstall "Development Tools" "Server Platform Development"

- 添加用户和程序目录

~]# useradd nginx
~]# mkdir /var/cache/nginx && chown nginx.nginx /var/cache/nginx/

#### 获取源码包

首先下载程序包

~]# wget https://nginx.org/download/nginx-1.18.0.tar.gz

> 18为次版本号，为偶数表示是稳定版本

#### 编译安装

~]# tar -xf nginx-1.18.0.tar.gz
~]# cd nginx-1.18.0
~]# ./configure  --prefix=/usr/local/nginx \
            --sbin-path=/usr/sbin/nginx \
            --conf-path=/etc/nginx/nginx.conf \
            --error-log-path=/var/log/nginx/error.log \
            --http-log-path=/var/log/nginx/access.log \
            --pid-path=/var/run/nginx.pid \
            --lock-path=/var/run/nginx.lock \
            --http-client-body-temp-path=/var/cache/nginx/client_temp \
            --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
            --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
            --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
            --http-scgi-temp-path=/var/cache/nginx/scgi_temp \
            --user=nginx \
            --group=nginx \
            --with-http_ssl_module \
            --with-http_realip_module \
            --with-http_addition_module \
            --with-http_sub_module \
            --with-http_dav_module \
            --with-http_flv_module \
            --with-http_mp4_module \
            --with-http_gunzip_module \
            --with-http_gzip_static_module \
            --with-http_random_index_module \
            --with-http_secure_link_module \
            --with-http_stub_status_module \
            --with-http_auth_request_module \
            --with-threads \
            --with-stream \
            --with-stream_ssl_module \
            --with-http_slice_module \
            --with-mail \
            --with-mail_ssl_module \
            --with-file-aio \
            --with-http_v2_module \
            --with-debug

~]# make && make install

## NGINX 命令

nginx -h
    Shows the NGINX help menu.
nginx -v
    Shows the NGINX version.
nginx -V
    Shows the NGINX version, build information, and configura‐ tion arguments, which shows the modules built in to the NGINX binary.
nginx -t
    Tests the NGINX configuration.
nginx -T
    Tests the NGINX configuration and prints the validated config‐ uration to the screen. This command is useful when seeking support.
nginx -s signal
    The -s flag sends a signal to the NGINX master process. You can send signals such as stop, quit, reload, and reopen. The stop signal discontinues the NGINX process immediately. The quit signal stops the NGINX process after it finishes processing inflight requests. The reload signal reloads the configuration. The reopen signal instructs NGINX to reopen log files.
