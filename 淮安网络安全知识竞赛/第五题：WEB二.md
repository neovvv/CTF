#WEB二

打开http://101.37.25.214:8003，显示

```html
请从本地访问！
```

判断是需要做IP伪装。

使用BurpSuite抓包，修改HTTP头，加入
```html
X-forwarded-For: 127.0.0.1
```

拿到key:50AEC3D1D7370C68
