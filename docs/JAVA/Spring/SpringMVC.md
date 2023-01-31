# MVC

- M:model(模型):封装以及处理数据(entity dao service)

- V:view(视图):收集以及展示数据(JSP)
- C:controller(控制器):协调模型与视图,负责整个流程的控制(ActionServlet Filter)

> MVC是一个软件架构的设计思想,按照功能的不同将软件划分为三个模块,分别是模型、视图和控制器(负责协调模型与视图,模型处理之后的数据不会直接交给视图去展示,而是返回给控制器,由控制器调用视图来展示数据.反之,视图先向控制器发请求,由控制器调用模型来处理数据

## 优点

- 提高代码(模型)的复用率
- 当模型与视图其中一方发生改变时,不会影响另一方.
- 方便测试

## 缺点

- 使用MVC之后,代码的复杂度以及代码量会有所增加.
- 相应的开发成本会有所提高.

# SpringMVC

> springMVC是一个轻量级的MVC型框架,偏于快速高效的开发一个web应用.

## 体系结构

- DispatcherServlet(前端控制器 请求入口)

- HandlerMapping(映射处理器 请求分发)
- Controller (业务处理器 请求处理)
- ModelAndView (模型 封装数据以及视图名称)
- ViewResolver (视图解析器 定位视图与传递数据)

## 请求流程

1. 请求发起之后,先经过前端控制器`DispatcherServlet`

2. 前端控制器通过映射处理`HandlerMapping`调用相应的业务控制器`Controller`来处理请求.
3. 执行业务器里约定的方法,在方法中调用模型来处理数据,将处理的结果封装到`ModelAndView`对象中.
4. 前端控制器调用视图解析器`ViewResolver`,解析`ModelAndView`对象中的数据,定位视图资源并传递处理的数据,生成页面返回给用户.

## 入门实例

> hello.do --> hello.jsp

### 基于XML配置
1. 在web.xml中配置前端控制器,拦截*.do的请求.

2. 定义业务控制器,实现Controller接口
3. 在spring主配置文件配置映射处理器,指定请求地址与controller的对应关系
4. 在spring主配置文件配置视图解析器,定义前缀和后缀

### 基于注解配置
1. 同上 配置前端控制器

2. 定义业务控制器Controller 在类上方使用@Controller注解标记

3. 在spring主配置文件中开启组件扫描以及启用MVC注解标记.

4. 同上 配置视图解析器

5. 获取请求参数

   1. 使用HttpServletRequest获取
      - 优点:直接 
      - 缺点:繁琐 需要自己做类型转换
   2. 在方法中定义与请求参数相同的形参.若名称不一致,可以使用`@RequestParam("请求参数名")`注入数据
   3. 若请求参数较多,建议封装成实体类,在方法中用引用类型的变量(实体类中属性与请求参数名相同)

6. 向页面传递数据

   1. 使用`HttpServletRequest`
   2. 使用`ModelAndView(String viewName,Map<String,Object> map)`
   3. 使用`ModelMap`
   4. 使用`@ModelAttribute(绑定名)`

7. 如何重定向

   1. 返回数据类型String

      ```
      return "redirect:url";
      ```

   2. 返回数据类型是ModelAndView

      ```
      return new ModelAndView(new RedirectView(url));
      ```

      