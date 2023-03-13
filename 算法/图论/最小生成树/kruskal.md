# kruskal   稀疏图
[click](https://www.acwing.com/problem/content/861/)
![图 1](/images/df28f6156c0ef17e5738b0768621d2ae332b67af81816c9f5808f8e3eb6a16f1.png)  

#### 设置一个并查集来表示生成树
#### 将所有边的权值从小到大排序，遍历所有的边，若某条边连接的两个节点不在同一个生成树中，把其加入到生成树中。

```cpp
//p表示并查集
//cnt表示当前加的边数
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int M = 2e5 + 10;
const int N = 1e5 + 10;
int n, m;
int p[N];
typedef struct {
	int a, b, w;
} eg;
eg edge[M];
void init_ds() {
	for (int i = 1; i <= n; i++)p[i] = i;
}
int find(int x) {
	if (p[x] != x) p[x] = find(p[x]);
	return p[x];
}
int kruskal() {
	int res = 0;
	int cnt = 0;
	for (int i = 0; i < m; i++) {
		int a = edge[i].a, b = edge[i].b, w = edge[i].w;
		a = find(a), b = find(b);
		if (a != b) {
			res += w;
			cnt++;
			p[a] = b;
		}
	}
	if (cnt < n - 1)return  -0x3f3f3f3f;
	else return res;
}
signed main() {
	cin >> n >> m;
	for (int i = 0; i < m; i++) {
		int u, v, we;
		cin >> u >> v >> we;
		edge[i].a = u, edge[i].b = v, edge[i].w = we;
	}
	sort(edge, edge + m, [&](eg a, eg  b) {return a.w < b.w; });
	init_ds();
	int ans = kruskal();
	if (ans == -0x3f3f3f3f)cout << "impossible";
	else cout << ans;
}
```