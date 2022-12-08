# SG函数

假设现有状态为x ， 在一步的操作内可变成 $y_1,y_2,y_3$

那么$SG(x)=mex\{SG(y_1),SG(y_2),SG(y_3)\}$

$mex$为在集合中取最小的没有出现过的自然数

---
### 定义终点的SG值为0
- 某个点的SG值为0，只能走向$SG!=0$的状态
- 某个点的SG值非0，那么可以走向$SG=0$的状态

故先手$SG!=0$ 先手必胜，反之必败
---
### 对于多张状态图而言
#### 初始状态 $SG(x_1)\wedge SG(x_2)...\wedge SG(x_n)!=0$  先手必胜，反之必败

#### 证明方法与NIM游戏类似
$SG(a_i)\wedge x<SG(a_i)$

比$SG(a_isd)$小的SG值都是合法操作，因为SG取的就是不能变化到的状态的最小值

[click](https://www.acwing.com/problem/content/895/)
![图 2](/images/132412ef72b63869055f8c9a211b40f5ac66110770c802445a80e767d360ad79.png)  
把每一堆石头抽象为一个状态图
```cpp
#include<unordered_set>
#include <iostream>
#include <cstring>
const int N = 110,M=10010;
int s[N]; int SgValue[M];
using namespace std;
int n;
int k;
int SG(int q) {
	if (SgValue[q] != -1)return SgValue[q];
	unordered_set<int> S;
	for (int i = 0; i < k; i++) {
		int sum = s[i];
		if (q>= sum) S.insert(SG(q- sum));
	}
	for (int i = 0;; i++)
		if (!S.count(i)){
			return SgValue[q]=i;
		}
}
int main() {
	cin >> k;
	for (int i = 0; i < k; i++)cin >> s[i];
	cin >> n;
	memset(SgValue, -1, sizeof(SgValue));
	int res = 0;
	for (int i = 0; i < n; i++) {
		int x;
		cin >> x;
		res ^= SG(x);
	}
	if (res)cout << "Yes";
	else cout << "No";
}

```
## 拆分NIM
![图 3](/images/af9cae62cee98ae74e17bb292f7e775bba937cf5934f6ca0729c6f0b2e65f83c.png)  
[click](https://www.acwing.com/problem/content/896/)

把一个堆拆分为两个，那么这个堆的SG值就等于拆分为两个的堆的SG异或值
```cpp
#include <iostream>
#include <unordered_set>
#include <cstring>
using namespace std;
const int N = 110;
int s[N];
int sg(int x) {
	if (s[x] != -1)return s[x];
	unordered_set<int> S;
	for (int i = 0; i < x; i++) {
		for (int j = 0; j <= i; j++) {
			S.insert(sg(i) ^ sg(j));
		}
	}
	for (int i = 0;; i++)
		if (!S.count(i))return s[x] = i;
}
signed main() {
	int n;
	cin >> n;
	int res = 0;
	memset(s, -1, sizeof(s));
	while (n--) {
		int q;
		cin >> q;
		res ^= sg(q);
	}
	if (res)cout << "Yes";
	else cout << "No";
}

```
