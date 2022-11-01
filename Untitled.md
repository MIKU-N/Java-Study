1、查询每个课程最低分的学生学号

```mysql
select stuno,min(score)
from scoreinfo
group by classno
having min(score);
```

2、查询001课程最高成绩的学生学号

```mysql
select stuno,classno,score
from scoreinfo
where classno=001 and score=(
select max(score)
from scoreinfo
where classno=001
);
```

3、查询成绩总和比5003高的学生

```mysql
select stuno,sum(score)
from scoreinfo
group by stuno
having sum(score)>(
select sum(score)
from scoreinfo
where stuno=5003
);
```

4、查询'张三'有哪些课程号(两个'张三')

```mysql
select stuno,classno
from scoreinfo
where stuno in(
select stuno
from stundentinfo
where stuname="张三"
)
```

5、查询有哪些课程(非关联子查询)
   ps:满足课程表中课程号出现成绩表

```mysql
select classno,classname
from classinfo
where classno in(
select classno from scoreinfo
)
```



6、查询有哪些课程(关联子查询)

```mysql
select classno,classname
from classinfo c
where exists(
select 1 from scoreinfo
where classno=c,classnos
)
```



7、学生没有哪些课程
   insert into classinfo values(004,'网页基础');

```mysql
insert into classinfo values(004,'网页基础');
select classno,classname
from classinfo s 
where score<(
select avg(in)
)
```

8、查询课程低于本课程平均成绩的学生

```mysql
select stuno,classno,score
from scoreinfo s
where score<(
select avg (ifnull(score,0))
from scoreinfo
where classno=s.classno
);
```

9、查询001课程低于本课程平均成绩的学生	

```mysql
select stuno,classno
from scroe<(
select avg(ifnull(score,0))
from scoreinfo
where classno=s.classno and classno==001
);
```

10、查询课程人数比001课程人数多

```mysql
select classno,count(*)
from scoreinfo
group by classno
having count(*)>(
select count(*)
from scoreinfo
where classno==001
)
```



