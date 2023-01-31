创建表

```mysql
create table user_li(
id int,
username varchar(10),
password varchar(12)
);
insert into user_li  values(1,'张三','666');
insert into user_li  values(1,'李四','888');
```

模拟登录:查询操作，查询结果做判断

```
```



事务

> 事务在数据库中保证交易可靠的机制，JDBC支持数据库事务概念，在JDBC中事务默认是自动提交

事务的特性：ACID

原子性：事务必须以原子为工作单元，对于数据的修改要么一起成功提交，要么失败取消

一致性：事务在完成时，全部数据必须保持一致状态

隔离性：由并发事务操作的修改与其他并发操作修改隔离

持久性：事务完成后，对于系统的影响永久有效

> 事务是属于数据库的概念，JDBC支持事务，本质上还是在数据库中实现的

JDBC支持事务提供API

```java
//获取事务提交 默认自动提交
Connection.getAutoCommit();
//设置事务提交方式，不自动提交
Connection.setAutoCommit(false);
//事务提交
Connection.commit();
//事务回滚
Connection.rollback();
```

```mysql
//创建测试表
create table account_li(
id char(1),
money int
);
insert into account_li values('A',1000);
insert into account_li values('B',2000);
select * from account_li;
```

```java
//转账操作:更新
void translate(String from,String to,int num);
```



批处理

> 发送到

批处理提供API

`addBatch(sql)` `Statement` 语句对象的方法，可以将多条待处理的SQL语句添加到该语句对象列表中

`addBatch()` `PrepareStatement` 语句对象的方法，可以将多条待处理的SQL语句添加到该语句对象列表中

`executeBatch()` 把 `Statement`和`PrepareStatement`语句对象职中全部的SQL语句发送到数据库中进行批处理

`clearBatch()`清空语句对象列表中的SQL语句

> 如果对象中包含过多待处理的SQL语句，可能会出现内存溢出的问题，建议及时处理语句对象列表

```mysql
//创建表
create table stu_li(
id int primary key,
name varchar(10) not null
);
//批量增加数据 Statement
void insertBatch();
//批量删除数据 PrepareStatement
void deleteBatch();
```



返回自动生成的主键值

mysql支持主键自增 `primay key auto_increment`

```mysql
//修改表结构 alter
//员工表中员工号添加主键
alter table emp_li add primary key(empno);
//员工表中添加自增
alter table emp_li modify empno int auto_increment;
//部门表中部门号添加主键自增
alter table dept_li change deptno deptno int primary key auto_increment;
//员工表中部门号添加外键（关系 主表/从表）
alter table emp_li add foreign key(deptno) references dept_li(deptno);
```

```
//关联表插入
//往部门表中增加一条数据，同时往员工表内增加一条记录（将员工分配给该部门）
//单表操作
部门表中插入记录-》查询员工号-》员工表插入记录
insert into deptno_li(dname,location) values(?,?);
select deptno from dept_li where dname=?;
insert into emp_li(ename,deptno) values(?,?);

//关联表操作
利用PreparedStatement的getGeneratedKeys方法获取自增类型的数据，只有一次数据交互，性能良好
```

分页查询

```mysql
//分页查询SQL
select 字段 from 表 每页开始下标，每页记录数
//下标计算公式
下标=（第几页-1）*记录数;
//分页查询
List<Emp> findByPage(int page,int pagesize);
delete from users where is_email_confirmed=0;
```



补充：

设计模式

为解决一类相同或相似问题而提出来的解决方案，并为其命名
