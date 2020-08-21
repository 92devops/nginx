该ngx_http_auth_basic_module模块允许通过使用“ HTTP基本身份验证”协议验证用户名和密码来限制对资源的访问。

```
~]# htpasswd  -c /etc/nginx/htpasswd tom
New password:
Re-type new password:
Adding password for user tom
```

```
location = /basic_status {
        stub_status;
        auth_basic           "closed site";
        auth_basic_user_file /etc/nginx/htpasswd;
}
```
