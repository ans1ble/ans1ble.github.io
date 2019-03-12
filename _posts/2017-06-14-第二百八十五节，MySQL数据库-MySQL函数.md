
---
layout: post
title: " 第二百八十五节，MySQL数据库-MySQL函数 "
author: "Ans1ble"
header-style: text
tags:
      - Python
---


**MySQL数据库-MySQL函数**



**1、 **MySQL内置函数****

****SELECT执行函数，后面跟要执行的函数****



****CHAR_LENGTH(str)函数：返回字符串的字符长度****

[code]

     -- CHAR_LENGTH(str)函数：返回字符串的字符长度
    
    SELECT CHAR_LENGTH('欢迎光临');
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614212732462-1014976948.png)



**LENGTH(str)函数：返回字符串的字节长度**

[code]

     -- LENGTH(str)函数：返回字符串的字节长度
    
    SELECT LENGTH('欢迎光临');
[/code]



**CONCAT(str1,str2,...)函数：拼接字符串**

[code]

     -- CONCAT(str1,str2,...)函数：拼接字符串
    
    SELECT CONCAT('你好','欢迎光临');
[/code]



**CONCAT_WS(链接符,str1,str2,...)函数：自定义链接符，拼接字符串**

[code]

     -- CONCAT_WS(链接符,str1,str2,...)函数：自定义链接符，拼接字符串
    
    SELECT CONCAT_WS('_','你好','欢迎光临');
[/code]



**CONV(N,from_base,to_base)函数：进制转换**

[code]

     -- CONV(N,from_base,to_base)函数：进制转换
    
    SELECT CONV('a',16,2); -- 表示将 a 由16进制转换为2进制字符串表示
[/code]



**FORMAT(X,D)函数：将数字X 的格式写为'#,###,###.##',以四舍五入的方式保留小数点后 D 位， 并将结果以字符串的形式返回。若
D 为 0, 则返回结果不带有小数点，或不含小数部分。**

[code]

    -- FORMAT(X,D)函数：将数字X 的格式写为'#,###,###.##',以四舍五入的方式保留小数点后 D 位， 并将结果以字符串的形式返回。若  D 为 0, 则返回结果不带有小数点，或不含小数部分。
    
    SELECT FORMAT(12332.1,4); -- 结果为： '12,332.1000'
[/code]



**INSERT(原始字符串,替换起始位置,替换长度,替换的新字符串)函数：在str的指定位置插入字符串**

[code]

     -- INSERT(原始字符串,替换起始位置,替换长度,替换的新字符串)函数：在str的指定位置插入字符串
    
    SELECT INSERT('欢迎光临官方网站',5,2,'我们'); -- 返回：欢迎光临我们网站
[/code]



**其他函数**

[code]

      INSERT(str,pos,len,newstr)
            在str的指定位置插入字符串
                pos：要替换位置其实位置
                len：替换的长度
                newstr：新字符串
            特别的：
                如果pos超过原字符串长度，则返回原字符串
                如果len超过原字符串长度，则由新字符串完全替换
        INSTR(str,substr)
            返回字符串 str 中子字符串的第一个出现位置。
    
        LEFT(str,len)
            返回字符串str 从开始的len位置的子序列字符。
    
        LOWER(str)
            变小写
    
        UPPER(str)
            变大写
    
        LTRIM(str)
            返回字符串 str ，其引导空格字符被删除。
        RTRIM(str)
            返回字符串 str ，结尾空格字符被删去。
        SUBSTRING(str,pos,len)
            获取字符串子序列
    
        LOCATE(substr,str,pos)
            获取子序列索引位置
    
        REPEAT(str,count)
            返回一个由重复的字符串str 组成的字符串，字符串str的数目等于count 。
            若 count <= 0,则返回一个空字符串。
            若str 或 count 为 NULL，则返回 NULL 。
        REPLACE(str,from_str,to_str)
            返回字符串str 以及所有被字符串to_str替代的字符串from_str 。
        REVERSE(str)
            返回字符串 str ，顺序和字符顺序相反。
        RIGHT(str,len)
            从字符串str 开始，返回从后边开始len个字符组成的子序列
    
        SPACE(N)
            返回一个由N空格组成的字符串。
    
        SUBSTRING(str,pos) , SUBSTRING(str FROM pos) SUBSTRING(str,pos,len) , SUBSTRING(str FROM pos FOR len)
            不带有len 参数的格式从字符串str返回一个子字符串，起始于位置 pos。带有len参数的格式从字符串str返回一个长度同len字符相同的子字符串，起始于位置 pos。 使用 FROM的格式为标准 SQL 语法。也可能对pos使用一个负值。假若这样，则子字符串的位置起始于字符串结尾的pos 字符，而不是字符串的开头位置。在以下格式的函数中可以对pos 使用一个负值。
    
            mysql> SELECT SUBSTRING('Quadratically',5);
                -> 'ratically'
    
            mysql> SELECT SUBSTRING('foobarbar' FROM 4);
                -> 'barbar'
    
            mysql> SELECT SUBSTRING('Quadratically',5,6);
                -> 'ratica'
    
            mysql> SELECT SUBSTRING('Sakila', -3);
                -> 'ila'
    
            mysql> SELECT SUBSTRING('Sakila', -5, 3);
                -> 'aki'
    
            mysql> SELECT SUBSTRING('Sakila' FROM -4 FOR 2);
                -> 'ki'
    
        TRIM([{BOTH | LEADING | TRAILING} [remstr] FROM] str) TRIM(remstr FROM] str)
            返回字符串 str ， 其中所有remstr 前缀和/或后缀都已被删除。若分类符BOTH、LEADIN或TRAILING中没有一个是给定的,则假设为BOTH 。 remstr 为可选项，在未指定情况下，可删除空格。
    
            mysql> SELECT TRIM('  bar   ');
                    -> 'bar'
    
            mysql> SELECT TRIM(LEADING 'x' FROM 'xxxbarxxx');
                    -> 'barxxx'
    
            mysql> SELECT TRIM(BOTH 'x' FROM 'xxxbarxxx');
                    -> 'bar'
    
            mysql> SELECT TRIM(TRAILING 'xyz' FROM 'barxxyz');
                    -> 'barx'
[/code]



**文本函数**

函数

|

用法

|

描述  
  
---|---|---  
  
CONCAT()

|

CONCAT(x,y,...)

|

创建形如xy的新字符串  
  
LENGTH()

|

LENGTH(column)

|

返回列中储存的值的长度  
  
LEFT()

|

LEFT(column,x)

|

从列的值中返回最左边的x个字符  
  
RIGHT()

|

RIGHT(column,x)

|

从列的值中返回最右边的x个字符  
  
TRIM()

|

TRIM(column)

|

从存储的值删除开头和结尾的空格  
  
UPPER()

|

UPPER(column)

|

把存储的字符串全部大写  
  
LOWER()

|

LOWER(column)

|

把存储的字符串全部小写  
  
SUBSTRING()

|

SUBSTRING(column, start, length)

|

从column中返回开始start的length个字符（索引从0开始）  
  
MD5()

|

MD5(column)

|

把储存的字符串用MD5加密  
  
SHA()

|

SHA(column)

|

把存储的字符串用SHA加密  
  


**数字函数**

函数

|

用法

|

描述  
  
---|---|---  
  
ABS()

|

ABS(x)

|

返回x的绝对值  
  
CEILING()

|

CEILING(x)

|

返回x的值的最大整数  
  
FLOOR()

|

FLOOR(x)

|

返回x的整数  
  
ROUND()

|

ROUND(x)

|

返回x的四舍五入整数  
  
MOD()

|

MOD(x)

|

返回x的余数  
  
RNAD()

|

RNAD()

|

返回0-1.0之间随机数  
  
FORMAT()

|

FORMAT(x,y)

|

返回一个格式化后的小数  
  
SIGN()

|

SIGN(x)

|

返回一个值，正数(+1)，0，负数(-1)  
  
SQRT()

|

SQRT(x)

|

返回x的平方根  
  


**日期和时间函数**

函数

|

用法

|

描述  
  
---|---|---  
  
HOUR()

|

HOUR(column)

|

只返回储存日期的小时值  
  
MINUTE()

|

MINUTE(column)

|

只返回储存日期的分钟值  
  
SECOND()

|

SECOND(column)

|

只返回储存日期的秒值  
  
DAYNAME()

|

DAYNAME(column)

|

返回日期值中天的名称  
  
DAYOFMONTH()

|

DAYOFMONTH(column)

|

返回日期值中当月第几天  
  
MONTHNAME()

|

MONTHNAME(column)

|

返回日期值中月份的名称  
  
MONTH()

|

MONTH(column)

|

返回日期值中月份的数字值  
  
YEAR()

|

YEAR(column)

|

返回日期值中年份的数字值  
  
CURDATE()

|

CURDATE()

|

返回当前日期  
  
CURTIME()

|

CURTIME()

|

返回当前时间  
  
NOW()

|

NOW()

|

返回当前时间和日期  
  




**格式化日期和时间(DATE_FORMAT()** **和TIME_FORMAT())**

名词

|

用法

|

示例  
  
---|---|---  
  
%e

|

一月中的某天

|

1~31  
  
%d

|

一月中的某天，两位

|

01~31  
  
%D

|

带后缀的天

|

1st~31st  
  
%W

|

周日名称

|

Sunday~Saturday  
  
%a

|

简写的周日名称

|

Sun-Sat  
  
%c

|

月份编号

|

1~12  
  
---|---|---  
  
%m

|

月份编号，两位

|

01~12  
  
%M

|

月份名称

|

January~December  
  
%b

|

简写的月份名称

|

Jan~Dec  
  
%Y

|

年份

|

2002  
  
%y

|

年份，两位

|

02  
  
%l

|

小时

|

1~12  
  
%h

|

小时,两位

|

01~12  
  
%k

|

小时，24小时制

|

0~23  
  
%H

|

小时，24小制度，两位

|

00~23  
  
%i

|

分钟

|

00~59  
  
%S

|

秒

|

00~59  
  
%r

|

时间

|

8:17:02 PM  
  
%T

|

时间，24小时制

|

20:17:02 PM  
  
%p

|

上午或下午

|

AM或PM  
  
**更多函数：[中文猛击这里](http://doc.mysql.cn/mysql5/refman-5.1-zh.html-
chapter/functions.html#encryption-functions) OR
[官方猛击这里](https://dev.mysql.com/doc/refman/5.7/en/functions.html)**





**2、自定义函数**

**create function 创建函数**

[code]

     -- create function 创建函数
    
    -- create function 函数名称 (形式参数名称,形式参数类型)
    -- returns int  返回整数类型
    -- BEGIN 函数内容开始
            -- 函数内容
    -- END 函数内容结束
    
    
    delimiter $$
    DROP function if EXISTS f1; -- 判断这个函数如果存在删除
    
    create function f1(  -- 创建函数，接收两个整数类型参数
        i1 int,
        i2 int)
    returns int  -- 返回整数类型
    BEGIN
        declare num int;  -- 定义num变量，整数类型
        set num = i1 + i2;  -- 将传值相加后，赋值给num变量
        return(num);  -- 返回num变量
    END $$
    delimiter ;
[/code]

**函数以创建**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614222854868-438014669.png)**



**执行自定义函数**

[code]

     -- 执行自定义函数
    
    SELECT f1(5,6); -- 返回11
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614223924353-1879639351.png)



**将函数放在查询语句里，将函数返回结果与查询语句返回结果组合**

[code]

     -- 执行自定义函数
    
    SELECT f1(5,6),id,yhm,xb,nl FROM usr; 
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614223845665-521085147.png)





**将函数放在查询语句里，函数的参数如果是写的某个字段，那么这个字段的值将传入函数里执行**

[code]

     -- 执行自定义函数
    
    SELECT f1(5,nl),id,yhm,xb,nl FROM usr; -- 函数的参数如果是写的nl字段，那么这个字段的值将传入函数里执行
[/code]

![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614224616431-192230983.png)





**删除函数**

**drop function 删除函数，后面跟要删除的函数名称**

[code]

     -- drop function 删除函数，后面跟要删除的函数名称
    
    drop function f1;
[/code]



**pymysql模块，执行函数**

**![](https://images2015.cnblogs.com/blog/955761/201706/955761-20170614225746603-666014317.png)**





**注意：函数与存储过程的区别**

**存储过程是：CREATE PROCEDURE 创建的**

**函数时：create function 创建的**

****存储过程是：CALL  执行的****

****函数时：SELECT 执行的****

****函数里：不支持SQL语句【重点】****

****存储过程里：支持SQL语句【重点】****



