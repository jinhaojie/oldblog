---
layout: post
title: java -- mysql Basics(基础篇)
---
#### 目录
* [introduction (简介)](#introduction) 
* [install and usage (mysql的安装和使用)](#installAndUsage)
* [new 和 newInstance](#newAndnewInstance)
* [String、StringBuffer、StringBuilder](#String)
* [inner class (内部类)](#innerClass)
* [proxy (代理)](#proxy)

<h5 id="introduction">introduction（简介）</h5> 

```
    mysql: open-source relational database 
    mysql是一个开源的关系型数据库。用c和c++实现。
```
        
<h5 id="installAndUsage">install and usage (mysql的安装和使用) </h5> 
    
```
   install:
   
   1>安装mysql(5.7以后的版本，安装完后会弹出个对话框，里面有root的临时密码记住这个临密
     码)：
   2>mysql的安装目录:  /usr/local/mysql-5,7…..
   3>将bin目录加入环境变量: export PATH=$PATH:/usr/local/my**/bin
   4>修改密码：mysqladmin  -u root -p password
             输入临时密码－》输入新密码
   5>登陆：mysql -uroot -psecret -Ddb -A (说明：-D指定数据库,-A)
   6>退出 : exit; | quit；
   --------------------------------------------------------------------
   
   usage:
   
   1.进入mysql交互命令行:
     show create table user;   // 显示创建表的sql
     show create database db_name;
     show columns from user;   |   desc user;     // 显示user表的列
     edit //进入编辑模式，编写执行的sql脚本
     show engines;  // 显示可用的存储引擎
     show databases; // 显示数据库
     show tables; // 显示所有表
     show tables from db_name
     show index from table //显示表的索引
     show columns from table like ‘c%’   //显示表中以c开头的列
     show tables like ‘c%’ // 显示表名是以c开头的表
     show tables like ’tableName’ //判断表是否存在
     select count(*)from table //在MyIsam中没有where的count(*)语句得到了优化,       
                               //而在InnoDB中要进行全表扫面，效率很多
     select * from table user; //如果执行成功，则表存在
     
   2.在bash命令行
     // 该命令可以不登录mysql就执行sql语句
     mysql -h127.0.0.1 -uroot -pwestos -Dtest_db -P3306 -e  'sql'
   
```

<h5 id="newAndnewInstance">new 和 newInstance </h5> 

```
    简述:
    
    new : 使用构造函数实例化对象，弱类型。低效率。只能调用无参构造
    newInstance :使用类加载机实例化对象。强类型。相对高效。能调用任何public构造。
    ------------------------------------------------------------------
    
    newInstance实现IOC、反射、依赖倒置 等技术方法的必然选择
        Class c = Class.forName(“A”);
        factory = (AInterface)c.newInstance();
    
    从jvm的角度看：
    >使用new的时候，这个要new的类可以没有加载；
    >使用newInstance时候，就必须保证：
      1、这个类已经加载；
      2、这个类已经连接了。
      而完成上面两个步骤的正是class的静态方法forName（）方法，
      这个静态方法调用了启动类加载器（就是加载javaAPI的那个加载器）。
```
    
<h5 id="String">String、StringBuffer、StringBuilder</h5> 

```
    简述：
    
    String : 字符串常量，
    StringBuffer : 字符串变量（线程安全）
    StringBuilder : 字符串变量（非线程安全）
    ------------------------------------
    1.String 和 StringBuffer
      性能差异：
      
      String s1 = "s1",s2 = "s2",s3 = "s3";    
      StringBuffer s = new StringBuffer();
      
      s1 = s2+s3;  /*相当于生成一个新的String存放s2+s3的结果，然后让s1指向他。*/
      s = s.append(s2).append(s3);  /*不生成新对象，因为StringBuffer是变长的 。*/
      
      综上，String 比 StringBuffer 一般情况下效率低。
      
    2.StringBuffer 和 StringBuilder
      性能差异：
      StringBuilder > StringBuffer
      线程安全：
      StringBuilder不保证同步，StringBuffer线程安全，保证同步.
```
   
<h5 id="innerClass">inner class (内部类)</h5>

```
  分类：
  
  1.静态内部类 （static 修饰）
  2.成员内部类 （就像一个实例变量）
  3.局部内部类 （定义在方法中，不能有访问修饰符修饰）
  4.匿名内部类 （无名称，无访问修饰符，常作为方法的参数）
  -----------------------------------------------------
  
  详解：
  
  1.静态内部类。 
  
    可访问对象：
      可以访问外部类的静态成员和静态方法
    实例化：
      OuterClass.InnerClass inner = new OuterClass.InnerClass();
      
  2.成员内部类。
  
    可访问对象：
      可以访问外部类所有成员和方法
      在内部类里访问外部类的成员：Outerclass.this.member
    实例化：
      在外部类里面创建成员内部类的实例：this.new Innerclass();
      在外部类之外创建内部类的实例：(new Outerclass()).new Innerclass();
      
  3.局部内部类
  
    可访问对象：
      可以访问方法内的final类型的局部变量
      可以访问外围类
    实例化：
      只能在方法中实例化对象并使用对象。
      
  4.匿名内部类
  
    >匿名内部类就是没有名字的局部内部类，不使用关键字
     class, extends, implements, 没有构造方法。
    >匿名内部类使用得比较多，通常是作为一个方法参数。
    
    声明与实例化：
    new ClassName(){ ... },通常作为一个方法的参数

      
```

<h5 id="proxy"> proxy 代理 </h5>

```
  简述：
        代理就好比是个转换器，对用户提供一个统一的接口，根据用户的类型去决定给用户提供
     那种服务。
     
  分类：
    1.静态代理：在代理类内部通过重载封装不同实现类所提供的方法。
    2.动态代理：代理类通过反射，动态的生成某个实现类的代理类实例。
    
  区别： 
    > 静态代理通过重载方式，在实现类数量很大时，代理类规模也就很大，对内存的消耗就更多
    > 动态代理动态生成代理实例，代理类的的代码量是不变的，是更节省内存的一种方案
   -----------------------------------------------------------------------
   一个动态代理的例子:

   package test;

   /*接口类*/
   public interface Subject {   
    public void doSomething();   
   }

   /*具体的实现类*/
   public class RealSubject implements Subject {   
      public void doSomething() {   
         System.out.println( "call doSomething()" );   
      }   
   }  

   package proxy;

   import java.lang.reflect.InvocationHandler;  
   import java.lang.reflect.Method;  
   import java.lang.reflect.Proxy;  
 
   public class ProxyHandler implements InvocationHandler{
       private Object tar;
    
       /* 有实现类对象tar生成代理类对象*/
       public ProxyHandler(Object tar){
           this.tar = tar;
           //绑定该类实现的所有接口，取得代理类 
           return Proxy.newProxyInstance(tar.getClass().getClassLoader(),
                                      tar.getClass().getInterfaces(),
                                      this);
       }    
       /*代理类对象通过反射调用实现类的方法*/
       public Object invoke(Object proxy , Method method , Object[] 
                         args)throws Throwable {
        Object result = null;
        //这里就可以进行所谓的AOP编程了
        //在调用具体函数方法前，执行功能处理
        result = method.invoke(tar,args);
        //在调用具体函数方法后，执行功能处理
        return result;
       }
   }

   public class TestProxy{
       public static void main(String args[]){
                     
           /*通过代理类获得实现类的代理*/
           Subject sub = (Subject) new ProxyHandler(new RealSubject());
           sub.doSomething();
       }
   }
    
```

