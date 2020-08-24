```
location ~ .*\.(htm|html)$ {
    ...
    # add_header Access-Control-Allow-Origin http://www.qq.com/index.html;
    add_header Access-Control-Allow-Origin *; # 允许所有
    add_header Access-Control-Allow-Methods GET,POST,PUT,DELETE,OPTIONS;
    ...
}
```
