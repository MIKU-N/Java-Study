设计表

```mysql
create table sale(
id int primary key auto_increment,
    name varchar(30),
    
)
```

实体类

DAO接口

```java
public List<Sale> findTop3() throws Exception;
```

DAO实现类

```mysql
select * from sale order by qty desc limit 3;
```

定义ActionServlet

```java
调用DAO.findTop3 -->Json字符串
```

定义sale.html

> 添加div元素，并给其相应的样式（宽高 背景颜色……）
>
> 将后台返回的数据展示在div中
>
> 请求发起的时机onload()
>
> 配合定时器 setInterval(f1,5000);