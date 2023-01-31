获取Ajax对象(前端)

```javascript
```

XMLHttpRequest相关

1. `.readyStatus` 与服务器之间的通讯状态 `0 1 2 3 4`
   - 状态`4`代表服务器响应结束
2. `.onreadystatechange` 给ajax对象注册监听
3. `.responseText` 服务器返回的相应文本
4. `.responseXML` 服务器返回的响应XML文本
5. `.status` 服务器返回的状态码 `500 404 200 302`

## 使用Ajax发送请求(Java)

### Get请求

1. 获取Ajax对象
2. 初始化`xhr.open("get","check.do?name=zs",true)`
   - true 异步请求
   - false 同步请求，ajax对象向服务器发送请求的同时，当前页面会被锁死；只要当服务器响应结束，用户才可以在页面上做其他操作
3. `.xhr.onreadystatechange=function(){}`
4. 发送请求 `xhr.send(null)`

#### 特殊情况(针对IE浏览器)

1. 中文乱码
   - IE浏览器默认采用GBK来处理数据，而chrome与Firefox采用UTF-8；通常情况下服务器编解码集也为UTF-8，因此IE会出现乱码问题
2. 缓存问题

### Post请求

1. 获取Ajax对象
2. 初始化`xhr.open("post","check.do",true)`
3. .`xhr.onreadystatechange=function(){}`
4. xhr.send(name="张三")