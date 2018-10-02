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
public char[] toCharArray()
```

- 字节数组与字符串

用String类的构造方法将字节数组转成字符串

```java
public String(byte[] bytes)
```

将字符串转为字节数组

```java
public byte[] getBytes(String charset);
```

- 字符串比较

**相等比较**

```java
str1.equals(str2)
```

**不区分大小写的比较**

```java
public boolean equalsIgnoreCase(String str2)
```

**两个字符串的关系**

\>0：表示本字符串大于目标字符串

<0：表示本字符串小于目标字符串

=0：表示本字符串等于目标字符串

```java
public int compareTo(String str2)
```

- 字符串查找

从一个完整的字符串之中判断指定内容是否存在

```java
public boolean contains(String str)//对象方法
```

判断是否以指定的字符串开头

```java
public boolean startsWith(String str)//起始位置
public boolean startsWith(String prefix,int offset)//偏移量为offset的位置开始
```

判断是否以指定字符串结尾

```java
public boolean endsWith(String str)
```

- 字符串替换

```java
public String replaceAll(String regex,String replacement)
例：
str.replaceAll("l","_"):将str中的所有l换成_
```

- 字符串拆分

```java
public String[] split(String regex)
public String[] split(String regex,int limit)//将字符串拆分成数组长度为limit的子字符串数组
```

请看下面的程序：

```java
String str = "129.168.1.1";
String result = str.split(".");
for(str temp:result){
    System.out.print(temp+"、");
}
```



其输出结果为：

即没有输出。

而我们想要的的结果是：129、168、1、1

在这里我们要注意，"."在Java语言中表示类的引用，其为特殊字符，因此需要转义

如一下程序：

```java
String str = "129.168.1.1";
String result = str.split("\\.");
for(str temp:result){
    System.out.print(temp+"、");
}
```

接下来请看两次截取的一段程序：

```java
public static void main(String[] args) {
        String str = "Lisa:18|Tom:20";
        String[] result = str.split("\\|");
        for(String temp:result){
            String name = temp.split(":")[0];
            String age = temp.split(":")[1];
            System.out.println("姓名："+name);
            System.out.println("年龄:"+age);
        }
    }
```



**特殊字符需要转义后拆分**

- 字符串截取

```java
public String substring(int beginIndex)//从指定索引截取到结尾
public String substring(int beginIndex,int endIndex)//从指定索引截取部分内容,左闭右开
```

- 去除字符串的左右空格，保留中间空格

```java
public String trim()
```

- 字符串转大小写

```java
public String toUpperCase();//字符串全部转为大写
public String toLowerCase();//字符串全部转为小写
```

- 判断字符串是否为空字符串，不判断null

```java
public boolean isEmpty()
```

### StringBuffer和StringBuilder

- 字符串拼接方法

```java
public synchronized StringBuffer append(各种数据类型)
```

- StringBuffer与String类的相互转换

**StringBuffer->String**

调用StringBuffer的构造方法 

```java
new StringBuffer("str");
```

**String->StringBuffer**

调用

```java
StringBuffer.toString()
```

- 字符串反转

```java
reverse():StringBuffer
```

- 删除（修改）指定范围的数据

```java
delete(int start,int end):StringBuffer
insert(int offset,各种数据类型):StringBuffer
```

- String、StringBuffer、StringBuilder的区别

1.String内容不可改变，StringBuffer、StringBuilder内容可以改变

2.StringBuffer JDK1.0，采用同步处理，线程安全，效率较低

StringBuilder(JDK1.5)，采用同步处理，线程不安全，效率高，当在String对象进行“+”，编译时会将String类变成StringBuilder进行append()处理

欢迎交流~

转载请注明原地址：[Lucky-pxx的博客](http://www.bingoxin.top) » [点击阅读原文](http://www.bingoxin.top/2018/10/java%E4%B8%AD%E7%9A%84String%E7%B1%BB/),谢谢！