---
title: 将本地变量的地址返回给main函数是有风险的。
updated: 2022-08-20T14:45:31.0000000+08:00
created: 2022-08-08T15:58:04.0000000+08:00
---

将本地变量的地址返回给main函数是有风险的。
因为本地变量的内存空间会被接下来其他函数使用。
全局变量和静态变量是安全的
尽量不要使用全局变量或静态变量传递参数

结构：
struct date
{
int day ;

int month;

int year;
}; //声明一个结构类型
struct date today; 声明该结构类型的变量
struct date today = {0,1,2}; // 初始化
today.day = 1;
today.month = 2;
today.year = 3;
![image1](../../resources/image1-3.png)
记住一切都要括号
宏定义也可以带多个参数,如 #define cube(x,y)

宏定义 超过一行 要加上\\
