```
valid_referers none blocked MY_IP  ~/baidu\.;

if ($invalid_referer) {
    return 403;
}
```

```
curl -e "http://www.baidu.com" -I http://MY_IP/index.png
```
