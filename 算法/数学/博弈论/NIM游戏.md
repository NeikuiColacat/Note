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
假设最后异或结果为x且$x!=0$ x的最高位为第k位

那么存在非0$a_i$ , $a_i$的第k位为1

则$a_i \wedge x<a_i$

那么我们可以从$a_i$中拿出$a_i-a_i\wedge x$个石头

那么$a_i$就变成$a_i-(a_i-a_i\wedge x)$

$a_1 \wedge a_2 \wedge a_i...\wedge a_n$

变成

$a_1 \wedge a_2 \wedge (a_i\wedge x)...\wedge a_n$

又有

$a_1 \wedge a_2 \wedge a_i...\wedge a_n=x$

则最终结果为x^x=0
---
那么先手拿到的结果总是为异或不为0，先手总是将其变为异或为0

后手拿到的结果总是异或为0

而$FinalStanding$则为全0，全0异或为0

则后手会拿到全0结果



```cpp
#include<bits/stdc++.h>
using namespace std;
int n;
void solve() {
	//任何数字与0异或结果都等于这个数字它本身
    int res = 0;
	while (n--) {
		int x;
		cin >> x;
		res ^= x;
	}
	if (res)cout << "YES\n";
	else cout << "NO\n";
}
int main() {
	cin >> n;
	solve();
}

```


