# KMP
[原题](https://www.acwing.com/problem/content/833/)
![图 5](../../images/a7d66bc08c046853f09dda15b51f63911dce3ab6ffffb6b10c308001c264d80d.png)  

> ### 引言 : 关于子串的前后缀

假设子串长度为i

前缀`P[1,j]` = 后缀`P[i-j+1,i]` 

前缀长度为`j`，那么后缀长度也是`j`,`i-j`（非后缀部分的末尾元素下标）再加1就是后缀起点

>对于kmp来说，我们要满足**前缀**等于**后缀**,这样每次匹配时，若匹配到某一个元素不等，此时前面的元素都相等，那么由于前缀等于后缀，我们只需要把字串挪到后缀起点重新开始匹配即可

>注意：我们要贪心的做，确保每种情况都能覆盖到，那么后缀的长度要达到尽可能地大，确保每次挪动步长最小。

>另外的，子串和源字符串下标从1开始，方便实现

---
### 关于next数组
>next 数组存的是：

当我的j+1不匹配的时候，`1~j`是匹配的, `1~j`此时是P的子串，找出`1~j`中最大的前缀和后缀相等,然后把整个P串挪到后缀的开头，再重新开始比较。
那么只需要把j变成j+1，即 前缀末尾的后一个元素再开始比较。
#### 那么next数组存储的就是每个P串子串`最大前缀长度`,即下次开始比较的位置

![图 2](../../images/fcedef47ee6f254d0fca1252313bad0b8a1e1f0cd4e77eebe0e02e89c79d6438.png)  

---
```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 1e6;
int n, m;
char p[N], s[N];
int ne[N];
signed main(void) {
	cin >> n >> p + 1 >> m >> s + 1;
	//求next数组
	for (int i = 2, j = 0; i <= n; i++) {
		while (j && p[i] != p[j + 1])j = ne[j];
		if (p[i] == p[j + 1])j++;
		ne[i] = j;
	}
	//和s[i] 匹配的永远是 p[j+1] 方便实现
	for (int i = 1, j = 0; i <= m; i++) {
		//j还没有退出起点
		while (j && s[i] != p[j + 1])j = ne[j];
		//如果匹配，则继续下一位
		if (s[i] == p[j + 1])j++;
		if (j == n) {
			//匹配成功
			cout << i - n<<' ';
			j = ne[j];
		}
	}


}

```
