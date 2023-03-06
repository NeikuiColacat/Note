# 当p为质数有
# $C_a^b\equiv C_{a\%p}^{b\%p}*C_{a/p}^{b/p}(mod\space p)$

## 证明：
![图 1](/images/c4a3c1c35a8f7d6516412bdbd64148ab64f9f3b26dc8d223c002f48954bc8595.png)  

#### 相当于将a，b进行p进制分解,然后递归求解p进制下a，b每一位的组合数连乘积
#### 特有： 当a与b按p进制展开的时候若有bi>ai,则$C_a^b\% p=0$

```cpp
#include <iostream>
using namespace std;
typedef long long ll;
int p;
int fp(int a, int n) {
	int res = 1;
	while (n) {
		if (n & 1)res = (ll)res * a % p;
		a =(ll)a * a % p;
		n >>= 1;
	}
	return res;
}
int C(int a,int b) {
	if (b > a)return 0;
	int res = 1;
	for (int i = 1, j = a; i <= b; i++, j--) {
		res = (ll)res * j % p;
		res = (ll)res * fp(i, p - 2) % p;
	}
	return res;
}
int lucas(ll a, ll b) {
	if (a < p && b < p)return C(a, b);
	return (ll)C(a % p, b % p) * lucas(a / p, b / p) % p;
}
signed main() {
	int n;
	cin >> n;
	while (n--) {
		ll a, b;
		cin >> a >> b >> p;
		cout << lucas(a, b)<<endl;
	}
	return 0;
}
```
