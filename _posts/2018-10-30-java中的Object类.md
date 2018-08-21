---
layout: post
title: Object类---最高参数统一化
date: 2018-10-30
tag: Java
--- 

Object类是JDK默认提供的一个类。Java中除了Object类，所有的类都存在继承关系，默认会继承Object父类

- toString()-取得对象信息

系统输出默认调用对象的toString方法

Object类中的toString方法只是简单输出当前引用的类名称以及对象地址

如果想在类中取得本类属性信息，需要覆写toString();

String类对该方法进行覆写，若String类调用该方法会返回String类的内容

- 对象比较---equals

- 接受引用数据类型

Object可以接受所有引用数据类型：数组、类、接口

### 包装类---使用Object接受一切数据

- 概念

包装类就是将基本数据类型封装到类中

- 包装类的分类

**数值型包装类**（Number的直接子类）：Byte、Double、Short、Long、Float、Integer

会发生类型转换异常--->NumberFormatException

**对象型包装类**（Object的直接子类）：Boolean、Character（char）

- 装箱与拆箱

**装箱：**将基本数据类型变为包装类对象。利用每个包装类提供的构造方法实现。

**拆箱：**将包装类中包装的基本数据类型取出。利用`xxValue()`

Integer num的值在-128~127范围内赋值，Integer对象在常量池产生，会复用已有对象，这个区间外的所有数据都在堆上产生，不会复用已有对象

```java
Integer i1 = 10;
Integer i2 = 10;
i1 == i2 //true
Integer i3 = 200;
Integer i4 = 200;
i3 == i4 //false
```

- 阿里编码规范

a.强制要求所有POJO类（简单Java类，类中只有成员变量、构造方法、getter/setter方法）属性必须使用包装类

b.强制RPC方法返回值和参数必须使用包装类

c.推荐所有的局部变量使用基本类型

- 包装类与字符串的转换

**String变为基本数据类型**

包装类.`parsexxx`(str)

```java
Integer.parseInt(str);
```

将字符串转换为布尔类型时：true--->true

不是true--->false

**基本数据类型->String**

a.""+基本数据类型

b.String类提供的静态方法valueOf（基本类型），不产生垃圾空间

```java
String str = String.valueOf(10);
```

欢迎交流~

转载请注明原地址：[Lucky-pxx的博客](http://www.bingoxin.top) » [点击阅读原文](http://www.bingoxin.top/2018/10/java%E4%B8%AD%E7%9A%84Object%E7%B1%BB/),谢谢！