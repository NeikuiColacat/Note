# prim 稠密图
[click](https://www.acwing.com/problem/content/860/)
![图 1](/images/018903d32a7b54782ba2048bf29bad816cf8aa10130ca65e8844ded7b4961b5f.png)  


#### 设集合s，每次寻找不在集合s中的离生成树最近的节点，将其加入集合，并且用这个节点更新所有节点到生成树的距离

```cpp
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int INF = 0x3f3f3f3f;
const int N = 510;
int g[N][N];
//d存的是节点到生成树的距离
int d[N];
int st[N];
int n, m;
int prim() {
	memset(d, 0x3f, sizeof(d));
	int res = 0;
	for (int i = 0; i < n; i++) {
		int t = -1;
		for (int j = 1; j <= n; j++) {
			if (!st[j]&&(t == -1 || d[j] < d[t]))t = j;
		}
		if (i && d[t] == INF)return INF;
        //存在自环的时候，要先加res，再用该节点更新
		if (i)res += d[t];
		for (int j = 1; j <= n; j++) {
			d[j] = min(d[j], g[t][j]);
		}
		st[t] = 1;
	}
	return res;
}
signed main() {
	memset(g,0x3f,sizeof(g));
	cin >> n >> m;
	while (m--) {
		int u, v, w;
		cin >> u >> v >> w;
		g[v][u]= g[u][v] = min(g[u][v], w);
	}
	int ans = prim();
	if (ans == INF) cout << "impossible";
	else cout << ans;
}
```