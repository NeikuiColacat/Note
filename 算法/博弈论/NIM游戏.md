#  NIM 游戏
[click](https://www.acwing.com/problem/content/893/)]
![图 1](/images/851fd70ce1185d10ae2d646a1f07b63a32432d34f92b1aadbed69d363f74b2e4.png)  

## RULE 
1. 每人一次挑选第i堆石子 ， 从中拿n个石子
2. 如果轮到某个人的轮次，无石子可拿，那么LOST

## 定理
所有堆中石子的异或值为 0 ， 先手必败  ，反之先手必胜

## 证明
## 1. 如果初始状态$a_1 \wedge a_2 \wedge a_3...\wedge a_n = 0$
#### 那么无论如何取 ， 最终异或的结果都不为0
### 证：
假设使$a_i$变成$a_{i1}$够使表达式为0

$a_1 \wedge a_2 \wedge a_i...\wedge a_n = 0$  

$a_1 \wedge a_2 \wedge a_{i1}...\wedge a_n = 0$

两个式子同时异或，右边0^0 == 0,左边相同数值异或为0，$a_i \wedge a_{i1}$也要为0，那么$a_i = a_{i1}$ , 产生矛盾。
## 2. 如果初始状态$a_1 \wedge a_2 \wedge a_3...\wedge a_n != 0$
#### 那么一定存在一种取法，使最终异或的结果为0
### 证：
假设最后异或结果为x
那么存在非0$a_i$ , 
