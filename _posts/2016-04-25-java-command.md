---
layout: post
title: java command-- java常用命令
---
#### 目录
* [jvm (jvm相关)](#jvm) 


<h5 id="jvm">jvm (jvm相关)</h5> 
    
    1. jmap (memroy map 内存映象图)
       
       -head pid :  查看jvm内存参数（permSize,等）
       
    2. jstat (java虚拟机静态监控工具)
      
       --gccapacity  pid   显示 vm内存中的三代（yound,old,perm）,如
                           PGCMN :permsize
                           PGCMX :maxpermsize
                           PGC:  当前新生成的perm内存大小
                           PC: 当前perm内存占用量
                           
                           
    
    
    3. jps (显示执行的java进程和Pid)
       无参： 
       jps 显示执行的java进程和Pid
    
    4. jconsole (jvm图形化监控工具)
       命令行执行jconsole.
    
        
