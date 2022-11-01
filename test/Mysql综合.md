-- 创建部门表

```
create table dept_test (
	deptno int,
	dname varchar(10),
	location varchar(10)
)
```

-- 初始化部门表

```
insert into dept_test values(10,'研发一部','南京');
insert into dept_test values(20,'销售部','苏州');
insert into dept_test(deptno,dname,location) values(30,'研发二部','无锡');
insert into dept_test(deptno,dname,location) values(40,'市场部','杭州');
```

-- 创建员工表

```
create table emp_test(
empno int,
ename varchar(10),
position varchar(20),
salary double(7,2),
bonus double(5,2),
hiredate date,
leader int,
deptno int 
);
```

-- 初始化员工表

```
insert into emp_test values(1001,'张三丰','开发人员',99999.99,999.99,'2010-03-11',NULL,10);
insert into emp_test values(1002,'张无忌','产品经理',5000,NULL,'2011-07-01',1001,10);
insert into emp_test values(1003,'杨过','测试人员',8000,500,'2008-05-15',NULL,10);
insert into emp_test values(1004,'郭靖','销售',4500,999,'2009-11-10',1005,20);
insert into emp_test values(1005,'黄蓉','测试人员',6000,NULL,'2009-09-01',NULL,20);
insert into emp_test values(1006,'洪七公','运营',3000,NULL,'2009-02-01',1005,20);
insert into emp_test values(1007,'韦小宝','销售',4000,800,'2009-02-20',NULL,30);
insert into emp_test values(1008,'乔峰','开发人员',8000,600,'2009-06-01',1007,30);
insert into emp_test values(1009,'小龙女','测试人员',1500,NULL,'2012-09-10',1008,30);
insert into emp_test values(1010,'段誉','董事长',15000,100,'2008-02-20',NULL,40);
insert into emp_test values(1011,'孙悟空','销售',50000,300,'2010-06-28',1010,40);
insert into emp_test values(1012,'燕小六','开发人员',12000,999.99,'2014-11-11',1010,40);
insert into emp_test values(1014,'张无忌','运营',8000,800,now(),1013,null);
```

//查询1005员工信息

```mysql
select * from emp_test where empno=1005;
```

//查询员工的基本工资和一年的基本工资

```mysql
select ename,salary,salary*12 年工资 from emp_test;
```

//查询员工的月薪

```mysql
select ename from emp_test;
```

//查询员工姓名、职位，如果没有职位则显示"No Position"

```mysql	
select ename,ifnull(position,"No Position")
from emp_test;
```

//查询员工信息，要求将员工姓名和职位连接在一起

```mysql
select concat(ename,ifnull(position,"No Position")
from emp_test;
```

//查询有哪些职位

```mysql
sele
```



//查询每个部门不重复的职位
//查询职位为'开发人员'的员工信息
//查询薪水大于等于5000并且小于10000的员工信息
//查询职位是'测试人员'或者'开发人员'的员工姓名和职位
//查询员工姓名中包含'张'字员工信息
//查询职位中第2个字符是'张'的员工姓名和职位
//查询哪些员工没有奖金
//查询哪些员工有奖金
//查询薪水不在5000到10000之间的员工
//查询不是20号部门和30号部门的员工信息	
//查询员工表中薪水总和
//查询员工表中人数总和、薪水总和、平均薪水
//查询员工表中最高薪水、最低薪水
//查询员工姓名和薪水，要求薪水从低到高进行排序
//按照部门号升序，同一个部门按照薪水降序
//查询每个部门的最高薪水和最低薪水，要求没有部门的不算在内
//查询每个部门的薪水总和和平均薪水，要求没有部门的不算在内
//按照职位分组，每个职位的最高薪水、最低薪水、人数总和，要求没有职位的不算在内
//查询平均薪水大于5000的部门和平均薪水，没有部门的不算在内
//查询每个部门的平均薪水
//查询薪水总和大于20000的部门号和薪水总和，要求没有部门的不算在内  
//查询哪些职位的人数超过2个人，没有职位的不算在内，
//查询谁的薪水比'张无忌'高 
//查询'研发部'有哪些职位
//查询谁的薪水比'张无忌'高，如果有多个'张无忌'
//查询哪些人的薪水比'张无忌'高，如果有多个'张无忌'
--查询谁和'郭靖'同部门，列出除了'郭靖'之外的
--查询谁是'张三丰'的下属
--查询每个部门拿最高薪水的是谁
--查询哪些部门的平均薪水比20号部门的平均薪水高
--查询员工所在部门的平均薪水大于5000的员工姓名和职位
--查询哪些员工的薪水是本部门的平均薪水
--查询哪些员工的薪水比本部门的平均薪水值低
--查询哪些人有下属
--查询哪些部门有员工