# Cookie

## 创建

```java
Cookie c=new Cookie("username","张三");
response.addCookie(c);
```

## 查找

```java

```

## 删除

```java
Cookie c=new Cookie(name,"");
c.setPath(path);
c.setMaxAge(0);
response.addCookie(c);
```

# Session(会话)

> 浏览器向服务器发送请求，服务器会创建session对象，该对象具有唯一的标识`SessionID`，服务器会将`SessionID`以`set-cookie`消息头的形式返回给浏览器，浏览器会将其保存在内存中，当浏览器再次向服务器发送请求时，会将`SessionID`以cookie消息头的方式发送给服务器，服务器会根据 `SessionID`查找session对象，通过这种方式来实现状态管理

## 如何获取

### 方式一

```java
HttpSession session=request.getSession(boolean flag);
//两种机制，取决于flag的值(true/false)
flag=true;	//浏览器会向服务器发送请求，服务器会先检查请求数据是否包含sessionID；如果没有则创建新的Session对象，如果有则根据SessionID查找Session对象，找到即返回；否则，创建新的session对象

flag=false;	//寻找到SessionID则返回，找不到则返回null
```

### 方式二

```java
HttpSession session=request.getSession();
//等价于方式一的flag=true，一般来说实际使用此方式
```

HttpSession接口相关方法

1. 获取sessionId

   ```java
   String:sessionId
   ```

2. 绑定数据

   ```java
   session.setAttribute(name,obj)
   ```

3. 根据绑定查找绑定值

   ```java
   Object:session.get
   ```

   