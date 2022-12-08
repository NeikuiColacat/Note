# spfa
[click](https://www.acwing.com/problem/content/description/853/)
![图 1](/images/479de97710f1f42358c82b1d42c2826db87cf44fb9055d0e7c3565c844a42284.png)  

#### bellman ford的优化
#### 若一个节点被更新为更小路径，那么就用这个节点去尝试更新它的出边节点
---

```cpp
//若一个节点被更新就将其塞入队列，用队列里的节点去更新其他节点
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
const int N = 1e5 + 10;
int wt[N], dis[N];
//st表示当前节点是否在队列中，如果是，无需再入队
int st[N];
int h[N], e[N], ne[N], idx;
int n, m;
void add(int a, int b, int w) {
	e[idx] = b, ne[idx] = h[a], wt[idx] = w, h[a] = idx++;
}
bool spfa() {
	memset(dis, 0x3f, sizeof(dis));
	dis[1] = 0;
	queue<int> q;
	q.push(1);
    st[1] = 1;
	while (q.size()) {
		int t = q.front();
		q.pop();
		st[t] = false;
		for (int i = h[t]; i != -1; i = ne[i]) {
			int j = e[i];
			if (dis[j] > dis[t] + wt[i]) {
				dis[j] = dis[t] + wt[i];
				if (!st[j]) {
					st[j] = 1;
					q.push(j);
				}
			}
		}
	}
    //因为是开的邻接表，不存在节点n若不连通能被负权边更新的情况，直接判等于
	if (dis[n] == 0x3f3f3f3f)return false;
	else return true;
}
signed main() {
	memset(h, -1, sizeof(h));
	cin >> n >> m;
	for (int i = 0; i < m; i++) {
		int x, y, z;
		cin >> x >> y >> z;
		add(x, y, z);
	}
	if (spfa()) cout << dis[n];
	else cout << "impossible";
}

```
## 判负环

设一个cnt数组，存储到该节点最短路径的边数，如果边数大于等于n，那么就存在负环

要找的是负环，所以初始化需要将所有节点都入队

```cpp
#include <iostream>
#include <algorithm>
#include <cstring>
#include <queue>
using namespace std;
const int N = 1e5 + 10;
int wt[N], dis[N];
int st[N];
int h[N], e[N], ne[N], idx;
int cnt[N];
int n, m;
void add(int a, int b, int w) {
	e[idx] = b, ne[idx] = h[a], wt[idx] = w, h[a] = idx++;
}
bool spfa() {
	memset(dis, 0x3f, sizeof(dis));
	cnt[1] = 0;
	dis[1] = 0;
	queue<int> q;
	for (int i = 1; i <= n; i++)q.push(i),st[i] = 1;
	while (q.size()) {
		int t = q.front();
		q.pop();
		st[t] = false;
		for (int i = h[t]; i != -1; i = ne[i]) {
			int j = e[i];
			if (dis[j] > dis[t] + wt[i]) {
				dis[j] = dis[t] + wt[i];
				cnt[j] = cnt[t] + 1;
				if (cnt[j] >= n) return 1;
				if (!st[j]) {
					st[j] = 1;
					q.push(j);
				}
			}
		}
	}
	return 0;
}
signed main() {
	memset(h, -1, sizeof(h));
	cin >> n >> m;
	for (int i = 0; i < m; i++) {
		int x, y, z;
		cin >> x >> y >> z;
		add(x, y, z);
	}
	if (spfa()) cout << "Yes";
	else cout << "No";
}

```