# 朴素版本 稠密图 ，边数数量级大于节点数 $O(N^2)$
[click](https://www.acwing.com/problem/content/851/)
![图 1](/images/2cb75225c7f3cb150262592dd8be8f15791f680e4e1b8c4c4d89f6580b892ba3.png)  
### 算法思路
1. 按题目要求建立邻接矩阵或者邻接表，将start放入S。

2. 将所有结点在经过S中的结点到达start的距离放入d数组（用于存放最短路径的长度）。

3. 在d数组中找到距离start最近且未在S中的结点Vi，将Vi收录进S，并更新和Vi有直接边相连的结点的d的值（如果经过Vi离start更近，则更换d为经过Vi的路径）。

4. 重复步骤2,3,直到所有的的结点被收录进S。
![图 2](/images/23b15f3f813d30080a4ae7fce07e6b55fc504c081ded04ef0e434742e3e4214e.png)  

![图 3](/images/0543611187329e9e35865e8ba6a44a0f4a5ea9a3087a523ba3d05c7a4226bd52.png)  
![图 4](/images/122a676bfdd7fd7138d583722f9d9c936f050ee72f7e68d23396c510d0ab52b5.png)  
![图 5](/images/ae90228344d19b684d2ec27ca6513a91206561e7ab5d672916121d6d06144aaf.png)  

![图 6](/images/89f07328c3523a4474add47373ed89302b662387faeaea25c38a8440b7b997c8.png)  
![图 7](/images/8fb04546c4f52f9ee3791be533cfee510e5df871e11160a245f13223feb3aede.png)  
![图 8](/images/74773d82fb7f79cf37c2bf65464d8ef9984af9f68cf187841fa71c7857752afd.png)  
---
# 证明
![图 9](/images/63a5f99b8d608860e54201de325e86a2779404aa7506e5c7ca1c87da27662172.png)  
![图 10](/images/4ba272d059eed0221a1872ea824619052f38736da20fa3b992ae4469b97b729c.png)  

![图 11](/images/1bd39842b94c47a76094d50dd9efc9aecf77e1ce3c49a7d5b055c34955bd8282.png)  
![图 12](/images/e64b8840ca3d9226ac79250715fb83c531817832c605b686801145a5d7958674.png)  

![图 13](/images/e94c2c33bf071c62a362f19bc734092b22b4b305b5539f6f1e222ccab627afe4.png)  

```cpp
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
const int N = 600;
const int INF = 0x3f3f3f3f;
int g[N][N], s[N], d[N];
int n, m;
int dijkstra() {
	memset(d, 0x3f, sizeof(d));
	d[1] = 0;
	for (int i = 1; i <= n; i++) {
		//t为没有在s集合中的离起点最短的点
		int t = -1;
		for (int j = 1; j<= n; j++) {
			if (!s[j] && (t == -1 || d[t] > d[j])) {
				t = j;
			}
		}
		s[t] = true;
		for (int i = 1; i <= n; i++) {
			d[i] = min(d[i], d[t] + g[t][i]);
		}
	}
	return d[n];
}
signed main() {
	memset(g, 0x3f, sizeof(g));
	cin >> n >> m;
	while (m--) {
		int x, y, z;
		cin >> x >> y >> z;
		//考虑重边的问题
		g[x][y] = min(g[x][y], z);
	}
	if (dijkstra() == 0x3f3f3f3f)cout << -1;
	else cout << d[n];
}
```
