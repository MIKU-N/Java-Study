## XML处理指令

处理指令用于指挥处理引擎如何解析XML文档内容

```xml
<xml version="1.0" encoding="uft-8"?></xml>
```

## XML组成

XML文档中包含XML元素，元素指的是从开始标签到结束标签，元素包含其他元素、文本，元素也可以拥有属性，属性提供关于元素的额外信息

### 属性

> 属性提供关于元素的额外信息

```xml
<a id="1">
	<b>root</b>
    <c>1234</c>
</a>
```

#### 注意

1. XML文档中只有一个根元素（不被其他元素包裹）
2. 元素必须有开始标签与结束标签
3. XML对大小写敏感
4. 属性值必须带有引号
5. 元素必须正确嵌套

```xml
<?xml version="1.0" encoding="UTF-8"?>
<list>
	<student id="1">
		<name>张三</name>
		<age>22</age>
		<money>1000</money>
	</student>
	<student id="2">
		<name>李四</name>
		<age>14</age>
		<money>5141</money>
	</student>
	<student id="3">
		<name>王五</name>
		<age>51</age>
		<money>4191</money>
	</student>
</list>
```

## XML解析方式

1. DOM解析

   > 全称:`Document Object Model` 文档对象模型
   >
   > DOM解析器在解析XML文档时会把文档中全部元素按照出现的层次结构关系，解析形成一个个对象节点

   - 优点: 把XML文档在内存中形成一个树形结构，可以遍历和修改节点
   - 缺点: 如果文档比较大，内存压力较大，解析时间较长

2. SAX解析

   >  全称:`Simple APIs for XML XML`简单应用程序接口
   >
   > 相比于DOM解析，SAX是一种速度更快，更为有效的解析方式
   >
   > 它逐行扫描文件，一边扫描一边解析，SAX可以在文档中任意时刻停止解析

   - 优点:解析可以立刻开始，速度快内存压力小
   - 缺点:无法对节点进行修改

3. JDOM解析

   特点:

   1. 使用具体类而不是接口
   2. API大量使用`Collection`类

4. DOM4j解析

   1. DOM4j是开源的，基于Java库来解析XML文档
   2. 具有性能优异、灵活性好、功能强大和易用特点

读XML文档

```java
//SAXReader对象
SAXReader reader =new SAXReader();
//读指定XML文档
//Document对象:文档树的根，可以为提供文档数据最初的访问入口
Document document=reader.read(new File(""));
//获取根元素
//Element对象:XML文档中元素，元素可以包含其他元素、文本、属性
Element root=document.getRootElement;
//获取根元素下面全部子元素
List<Element>  elements=root.elements();
//获取当前元素指定名字的属性
//Attribute对象 属性对象用于描述一个元素中的某个属性
Attribute attribute(String name);
//获取当前属性中的属性值
String getValue();
//获取元素中的文本元素
String elementText(String name);
```

写入XML

```java
//创建并返回Document对象
Document document=DocumentHelper.createDocument();
//向当前文档中添加根元素并返回此元素，此方法只调用一次
Element root=document.addElement(String name);
//向当前元素中添加指定名字的子元素
Element addElement(String name);
//向当前元素中添加指定的属性及属性值，返回当前元素
Element addAtrribute(String name,String value);
//向当前元素中添加指定的文本内容
Element addText(String text);
//通过XMLWriter将内容输出生成XML文件
XMLWriter writer=new XMLWriter();
writer.setOutputStream(new FileOutputStream(""));
writer.writer(document);
writer.close;
```

