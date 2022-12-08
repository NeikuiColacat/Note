# bellman ford
![图 1](/images/e1283d5c7d87e65d651ac2cdb0b64a65379021bbb45a67e038be08721276857b.png)  
[click](https://www.acwing.com/problem/content/855/)

### n个节点，迭代n次，每次遍历所有边，复杂度$O(N*M)$

#### 第k次更新后，从1号节点走向所有节点的最短路径的边数不超过k
---

### 用于判负环

如果在第n次迭代有某个点被更新了

那么就存在一条最短路径，边数为n

那么这个路径就有n+1个点

已知只有n个点

那么至少有2个点编号一样

该路径就一定存在环，且因为更新过，所以是负环


---

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <cstring>
using namespace std;
const int M=1e4+10,N=510;
struct {
	int a, b, w;
}edge[M];
//backup用来每次迭代，使用的信息都是上一次的，保证边数严格小于等于迭代次数
int dis[N],backup[N];
int n, m, k;
int bf() {
	memset(dis, 0x3f, sizeof(dis));
	dis[1] = 0;
	for (int i = 1; i <= k; i++) {
		memcpy(backup, dis, sizeof(dis));
		for (int j = 1; j <= m; j++) {
			int a = edge[j].a, b = edge[j].b, w = edge[j].w;
			dis[b] = min(dis[b], backup[a] + w);
		}
	}
    //若1节点无法到n节点，但n节点可以被其他节点更新，边权可能为负
    //所以要特判一下，边权最小负一万，最多500个节点，最多减500万
	if (dis[n] > 0x3f3f3f3f / 2)return 0x3f3f3f3f;
	return dis[n];
}
signed main() {
	cin >> n>>m>>k;
	for (int i = 1; i <= m; i++)cin >> edge[i].a >> edge[i].b >> edge[i].w;
	int d = bf();
	if (d == 0x3f3f3f3f)cout << "impossible";
	else cout << d;
}
```



