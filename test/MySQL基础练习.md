```mysql
学生表:
create table studentinfo(
stuno int,
stuname varchar(20),
stubirth date,
stusex int,
stuaddr varchar(30),
stutel char(11)
);
insert into studentinfo values(05001,'张三','1988-12-12',0,'江苏南京','12345');
insert into studentinfo values(05002,'李四','1987-06-05',1,'上海','12346');
insert into studentinfo values(05003,'王五','1987-12-01',0,'北京','12347');
insert into studentinfo values(05004,'赵六','1986-02-23',1,'广东深圳','12348');
insert into studentinfo values(05005,'张三','1988-04-01',0,'重庆','12349');
insert into studentinfo values(05006,'孙七','1988-07-03',1,'湖北武汉',null);

课程表:
create table classinfo(
classno int,
classname varchar(10)
);
insert into classinfo values(001,'计算机');
insert into classinfo values(002,'日语');
insert into classinfo values(003,'英语');

成绩表:
create table scoreinfo(
stuno int,
classno int,
score double(3,1)
);
insert into scoreinfo values(05001,001,95);
insert into scoreinfo values(05001,002,90);
insert into scoreinfo values(05001,003,88);
insert into scoreinfo values(05002,001,91);
insert into scoreinfo values(05002,002,93);
insert into scoreinfo values(05002,003,88);
insert into scoreinfo values(05003,001,95);
insert into scoreinfo values(05003,002,73);
insert into scoreinfo values(05003,003,58);
insert into scoreinfo values(05004,001,47);
insert into scoreinfo values(05004,003,61);
insert into scoreinfo values(05005,002,59);
insert into scoreinfo values(05005,003,47);
```

1、查询全部学生信息

```mysql
select * from studentinfo;
```

2、查询'张三'学生信息

```mysql
select * from studentinfo where stuname='张三';
```

3、查询学生的姓名和联系方式，没有联系方式的提示'No Stutel'

```mysql
select stuname,ifnull(stutel,'No Stutel')
from studentinfo;
```

4、查询学生的姓名和家庭住址，数据显示使用连接符

```mysql
select concat(stuname,"-",stuaddr)
from studentinfo;
```

5、查询课程号和成绩

```mysql
select classno,score
from scoreinfo;
```

6、查询001课程成绩是91或95学生的学号

```mysql
select stuno,classno,score
from scoreinfo
where classno=001
and score in(91,95);
```

7、查询所有姓名包含'孙'的学生信息

```mysql
select *
from studentinfo
where stuname like "%孙%";
```

8、查询所有没联系方式的学生信息

```mysq
select *
from studentinfo
where stutel is null;
```

9、查询所有成绩优秀(大于90)和成绩不及格(低于60)的学生学号和课程号

```mysql
select stuno,classno
from scoreinfo
where score>90
or score<60;
```

10、查询哪些学生有联系方式

```mysql
select *
from studentinfo
where stutel is not null;
```

11、查询学生姓名的长度

```mysql
select stuname,length(stuname)
from studentinfo;
```

12、查询87年以后出生的学生信息

```mysql
select *
from studentinfo
where year(stubirth)>1987;
```

1、给定一个数据123.456,按照指定格式显示,
   要求四舍五入保留两位，截取到小数点后1位。

```mysql
select truncate(round(123.456,2),1) from dual;
```

2、获取系统当前时间

```mysql
select now() from dual;
```

3、按照指定要求显示时间'%X-%m-%d %H:%i:%s'

```mysql
select date_format(now(),'%X-%m-%d %H:%i:%s') from dual;
```

4、查询所有学生信息,按照生日从大到小排序

```mysql
select *
from studentinfo
order by stubirth desc;
```

5、按课程号升序，同一个课程按成绩降序排序

```mysql
select classno,score
from scoreinfo
order by classno asc,score desc;
```

6、计算每门课程的最高分和最低分

```mysql
select classno,max(score),min(score)
from scoreinfo
group by classno;
```

7、计算课程平均分大于80的课程号

```mysql
select classno,avg(score)
from scoreinfo
group by classno;
having avg(score)>80;
```

8、计算每个学生的成绩总和

```mysql
select stuno,sum(score)
from scoreinfo
group by stuno;
```

9、查询学生成绩总分大于250

```mysql
select stuno,sum(score)
from scoreinfo
group by stuno
having sum(score)>250;
```

10、显示昨天，今天，明天的时间

```mysql
select adddate(now(),interval -1 day),now(),adddate(now(),interval 1 day)  from dual;
```

