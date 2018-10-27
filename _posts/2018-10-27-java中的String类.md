---
layout: post
title: java中的String类
date: 2018-10-27

tag: Java
--- 

### String类

- String的两种实例化方式

a.直接赋值

```java
String string = "hello";
```



b.通过构造方法构造实例化对象

```java
String string = new String("hello");
```

- 字符串相等比较

```java
String str1 = "hello";
String str2 = new String("hello");
System.out.println(str1 == str2);
```

输出结果为：false

“==”是对两个数据的值进行比较，则语句3其实是str1的内容与str2的地址进行比较的，因此结果为false。

若要对两个String类进行比较，应该使用：

```java
str1.equals(str2);
```

- 字符串的常量是String类的匿名对象

"hello"是一个String类的匿名对象

请看一下两个案例：

```java
String str = null;
System.out.println("hello".equals(str));
```

结果输出为：false

因为str没有指向的变量，也就和"hello"不相等了

```java
String str = null;
System.out.println(str.equals("hello"));
```

输出结果为：空指针异常

**在使用equals方法时需注意：**

判断String类匿名对象与实例化对象是否相等时，需使用案例一，即将字符串常量写在前面

- String类使用共享设计模式

在JVM底层自动维护一个字符串对象池（对象数组）

如果采用直接赋值的模式进行String类的对象实例化操作，此对象将自动保存到对象池中，如果下次继续采用直接赋值的模式声明String对象，先去对象池中找是否有指定内容，如果有，直接引用；如果没有，开辟新的空间而后将其保存到对象池中，以供下次使用

```java
String str1 = new String("hello");
String str2 = new String("hello");
String str3 = new String("hello");
System.out.println(str1 == str2);
System.out.println(str == str2);
System.out.println(str1 == str);
```

运行结果为：

ture

ture

ture

- 字符串的手工入池操作

```java
public native String intern();

例：
String str = new String("hello").intern();
```

- String类中两种对象实例化的区别

**直接赋值：**只会开辟一块堆内存空间，并且该字符串对象可以自动保存在对象池中以供下次使用

**构造方法：**会开辟两块堆内存空间，其中一块成为垃圾空间，不会自动保存到对象池中，但可以使用``intern()``方法手工入池

- 字符串常量不可变更

字符串一旦定义后不可改变

- 字符串使用原则

1.字符串使用就采用直接赋值

2.字符串比较就使用equals()实现

3.字符串改变别太多

- 字符与字符串

1.字符数组转为字符串

```java
public String (int []value);
```

2.将字符串按照索引转为单个字符

String -> char

```java
public char charAt(int index) //返回指定索引下标的字符
```

3.将字符串转为字符数组

```java
public char[] toCharArray();
```

转载请注明原地址：[Lucky-pxx的博客](http://www.bingoxin.top) » [点击阅读原文](http://www.bingoxin.top/2018/04/%E5%88%A4%E6%96%AD%E4%B8%A4%E4%B8%AA%E6%97%A0%E5%A4%B4%E7%BB%93%E7%82%B9%E7%9A%84%E5%8D%95%E9%93%BE%E8%A1%A8%E6%98%AF%E5%90%A6%E7%9B%B8%E4%BA%A4/),谢谢！