# 将寻找S集合外的距离最短节点用堆实现

# 同时因为是稀疏图，所以用邻接表来存储
```cpp
#include <iostream>
#include <algorithm>
#include <cstring>
#include <algorithm>
#include <queue>
using namespace std;
typedef pair<int, int> PII;
const int N = 1e6;
const int INF = 0x3f3f3f3f;
int s[N], d[N];
int e[N], ne[N], h[N],w[N],idx;
int n, m;
void add(int a, int b,int d) {
	e[idx] = b, ne[idx] = h[a],w[idx] = d, h[a] = idx++;
}
int dijkstra() {
	//优先队列，每次弹出最小距离的节点,底层由堆实现
	priority_queue<PII, vector<PII>, greater<PII>> heap;
	memset(d, 0x3f, sizeof(d));
	d[1] = 0;
	heap.push({ 0,1 });
	while (heap.size()) {
		auto t = heap.top();
		heap.pop();
		//拿出该节点的节点编号和离源点的距离
		int ver = t.second, distance = t.first;
		//存在重边，所以存在冗余
		if (s[ver])continue;
		s[ver] = true;
		for (int i = h[ver]; i != -1; i = ne[i]) {
			int j = e[i];
			if (d[j] > distance + w[i])d[j] = distance + w[i],heap.push({d[j],j});
		}
	}
	return d[n];
}
signed main() {
	cin >> n >> m;
	memset(h, -1, sizeof(h));
	while (m--) {
		int x, y, z;
		cin >> x >> y >> z;
		add(x, y, z);
	}
	if (dijkstra() == 0x3f3f3f3f)cout << -1;
	else cout << d[n];
}
```