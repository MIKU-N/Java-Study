### 两种架构

- BS 浏览器/服务器
- CS 客户端/服务器

---

### BS架构

> 客户端采用的是标准的浏览器，服务端采用的是标准的web服务器，客户端与服务端采用的是标准http通讯协议

#### 优点

1. 编程相对简单，不需要编写通讯模块与自定义协议
2. 不需要用户手动安装；后期升级也不需要用户手动更新

## Tomcat



## Servlet

> 用于扩展web服务器功能的组件规范
>
> 因为早期的web服务器只能处理静态资源文件，不能处理动态资源文件(需要经过一系列的计算生成的页面)，所以需要servlet扩展

### 扩展方式

> 组件+容器

- 组件:符合规范，实现特定功能的软件模块
- 容器:符合规范，为组件提供运行环境，并管理组件的生命周期

## 使用servlet编写web应用步骤

1. 定义Java类，继承HttpServlet
2. 重写 `service()`
3. 在 `web.xml`中配置servlet组件

### 在servlet中正确输出中文

- 原因:编码格式与解码格式不一致，需设置两端格式一致

### servlet获取请求参数

参数名唯一

```java
String str = request.getParameter("name");
```

参数名不唯一

```java
```

#### 中文参数乱码

在服务器端，设置编码集为对应编码集，例如

```java
request.setCharacterEncoding("UTF-8");
```

### 常见错误

1. servlet组件未继承HttpServlet返回500错误
2. servlet方法签名写错 返回405错误
3. web.xml中`<servlet-class>`路径写错 返回500
4. `web.xml` 中`<servlet>`与`<servlet-mapping>`中的`<servlet-name>`不一致  部署出错
5. 访问地址错误 返回404

### 运行原理

1. 浏览器根据IP地址和端口号与相应的服务器建立连接
2. 浏览器将数据按照HTTP协议进行打包
3. 浏览器向服务器发送请求
4. 服务器将数据按照HTTP协议拆包，并将拆包之后的数据存放到request对象上
5. 服务器根据请求地址查找对应的servlet组件，创建servlet对象，调用service方法进行处理
   - 通过request来获取请求参数
   - 将处理后的数据写入到response中
6. 服务器去除response中缓存的数据，按照HTTP协议打包
7. 服务器发送响应
8. 浏览器按照HTTP协议拆包，生成新的页面

## admin案例

数据库创建

```mysql
create table admin(
    id int primary key auto_increment,
    username varchar(30),
    password varchar(30),
    realname varchar(30)
);
```

## servlet如何请求资源路径

路径例如

```
localhost:8080/web02/list
```

则请求路径为`/web02/list`

处理过程

> 容器根据应用名查找webapps目录下对应的文件夹，如果找到了该文件夹，容器会先认为访问的servlet组件，根据`list`与`web.xml`中的`url-pattern`进行匹配，若匹配成功，则调用相应的servlet进行处理，若匹配失败，容器会认为访问的是静态资源文件，根据路径来查找该文件，找到返回该文件，找不到返回404

匹配规则

1. 精确匹配（完全匹配）

   > 以`/`开头，例如`/list`

2. 通配符匹配

   > 同样以`/`开头，例如`/*` 、`/abc/*`

3. 后缀匹配

   > 不能以`/`开头，例如`*.do`  `*.action`


## 使用一个servlet处理多个资源路径

1. 采用后缀匹配
2. 在servlet获取请求资源路径，在分析判断，用一个分支处理一个请求

## servlet生命周期

> 所谓的生命周期指的是容器如何给其实例化、初始化、就绪以及销毁的整个过程

四个阶段

1. 实例化

   > 容器创建servlet对象
   >
   > 默认情况下，请求到达容器时，容器会先检查内存中是否包含servlet组件对象，若没有，则创建新的servlet组件对象；反之返回内存中的对象
   >
   > 可以通过`<load-on-startup>1</load-on-startup>`提前实例化servlet组件，提前到容器启动时或者项目重新部署时再创建对象，参数值>=0整数，数值越小优先级越高

2. 初始化

   > 为servlet分配初始化资源

3. 就绪

   > 调用service方法处理请求

4. 销毁

   > 释放资源空间

## serverlet相关接口与抽象类

