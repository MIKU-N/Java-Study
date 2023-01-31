JDBC(Java Datebase Connectivity)

>  希望以相同的方式访问不同数据库，以实现与具体数据库无关的Java操作
>
> JDBC定义了一套标注的接口，即访问数据库的API。不同的数据库厂商根据各自数据库的特点去实现接口，从而得到Java程序的访问



JDBC接口

`DriverManager` 驱动管理类(注册驱动)

`Connection` 链接接口

`Statement` 语句对象接口

`PreparedStatement` 

`ResultSet` 结果集接口

JDBC执行过程

1. 加载驱动，创建链接
2. 创建语句对象
3. 执行SQL语句
4. 处理结果集（查询）
5. 关闭资源(链接、语句对象、结果集)

演示:以员工表(emp_li)为例实现增删改查操作

创建包:

1. com.example.entity 实体类包
2. com.example.dao 业务逻辑包
   1. .xxxDao 接口
   2. .impl 实现类包
3. com.example.util 工具类包
4. com.example.test 测试类包

> 说明:加载驱动可以不写，在创建链接时会自动寻找对应的驱动类

员工表中增加一条记录

```mysql
insert into emp_li values('1014','张三','Clerk',8000,800,日期,1012,10)
```

```mysql
//员工表种更新一条记录
根据员工号更新其他所有数据
update emp_li set ename="李四",position="Clerk",salary=1145,bonus=14,hiredate="2008-08-08",leader=null,deptno=10 where empno=1014;
```





