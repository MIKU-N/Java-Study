# Spring对事务的支持

## Spring事务

### 什么是事务

事务是一系列的动作,要么都成功,只要有一个失败,
就要回到最初始的状态

### Spring事务

Spring提供了对事务的支持,定义了统一编程模型的
接口PlatformTransactionManager,具体的事务策略
由各个技术平台实现.

## TransactionDefinition 事务属性/事务定义

## 事务的传播

- `REQUIRED`
  如果当前没有事务,就新建一个事务,如果已经存在
  一个事务中,加入到这个事务中.这是最常见的选择.

- `SUPPORTS`
  支持当前事务,如果当前没有事务,就以非事务方式
  执行.

- `MANDATORY`
  使用当前的事务,如果当前没有事务,就抛出异常.

- `REQUIRES_NEW`
  新建事务,如果当前存在事务,把当前事务挂起.

- `NOT_SUPPORTED` 
  以非事务方式执行操作,如果当前存在事务,就把
  当前事务挂起.

- `NEVER`
  以非事务方式执行,如果当前存在事务,则抛出异常.

- `NESTED`
  如果当前存在事务,则在嵌套事务内执行.如果当前
  没有事务,则执行与PROPAGATION_REQUIRED类似的
  操作

## 事务的隔离

### 一个事务受其他事务影响的程度

- 脏读
  
  > 事务1读取到了事务2未提交的数据
  
  事务1:`select sal from emp where id=1;1W`
  事务2:`update emp set sal=10W whereid=1;`
  
- 不可重复读
  >事务1读取到了事务2提交的数据(修改)
  
  事务1:`select sal from emp where id=1;1W`
  事务2:`update emp set sal=10W whereid=1;commit`

 - 幻读
   >事务1读取到了事务2提交的数据(添加删除)
   
   事务1:`select count(*) from emp where sal=1W;10`
   事务2:`insert into emp values(1W);commit();`
   

#### 默认隔离级别

mysql数据库默认的隔离级别:`repeatable-read`

#### Spring支持的隔离级别

- `ISOLATION-DEFAULT`:与后台数据库默认隔离级别一致
- `ISOLATION-READ-UNCOMMITTED`:读未提交的
- `ISOLATION-READ-COMMITTED`:读已提交
- `ISOLATION-REPEATABLE-READ`:可重复读

## 事务的超时

事务的超时是一个定时器,当超过指定时间时,事务
会自动回滚,而不是继续等待.

## 事务的只读

如果事务只对数据库做查询操作,可以将事务设置成
只读,如此可以提高响应的效率.

## 事务的回滚机制

### spring默认回滚机制

>  运行期异常会自动回滚,而检查型异常不会回滚.

运行期异常:
检查型异常:

## 事务管理方式

- 基于编程式事务管理
- 基于声明式事务管理

### 区别

> 基于编程式事务管理需要修改原先的代码,耦合度较高,代码的侵入性较强,不便于维护.
> 声明式事务管理是基于AOP思想将事务管理策略以低耦合的方式作用到目标组件上,编写简单,便于维护.

### XML配置实现事务管理

1. 在spring主配置文件添加事务管理器的bean定义,并且给其注入连接池对象

2. 指定事务管理器 配置事务策略
3. 配置AOP 定义切入点,方面组件,通知类型  

### 注解配置实现事务管理

1. 同上
2. 启用事务注解
3. 在目标组件类或者方法的上方使用`@Transactional`