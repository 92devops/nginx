#### 生成密钥和CA证书

```
ssl]# openssl  genrsa -idea -out nginx.key 1024
```
```
ssl]# openssl  req -new -key nginx.key  -out nginx.csr
-----
Country Name (2 letter code) [XX]:CN
State or Province Name (full name) []:beijing
Locality Name (eg, city) [Default City]:beijing
Organization Name (eg, company) [Default Company Ltd]:OP    
Organizational Unit Name (eg, section) []:devops
Common Name (eg, your name or your server's hostname) []:nginx.linux.cc  
Email Address []:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```
```
ssl]# openssl  x509 -req -days 3650 -in nginx.csr -signkey  nginx.key  -out nginx.crt
Signature ok
subject=/C=CN/ST=beijing/L=beijing/O=OP/OU=devops/CN=nginx.linux.cc
Getting Private key
Enter pass phrase for nginx.key:
```
