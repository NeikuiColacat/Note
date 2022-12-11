# floyd
## 基于dp实现

### 状态转移方程
---
#### 状态表示 ： 只经过1到k个节点，从i到j的最短路径

#### 状态计算 ： 等于不经过第k个节点，和经过第k个节点的最小值

$f[k,i,j] = min(f[k - 1,i, j], f[k - 1,i, k] + f[k - 1,k,j]$

#### 迭代的时候，第k层的信息由第k-1层获得，所以k要放在最外层

---
压缩维数正确性：
`dis[i][j] = min(dis[i][j], dis[i][k] + dis[k][j])`

- dis[i][j]
        
        显然在计算的时候其仍是上一层信息
- dis[i][k] 
        
        当j=k
        dis[i][k] = min(dis[i][k], dis[i][k] + dis[k][k])
        显然是无效更新
- dis[k][j]

        当i=k
        dis[k][j] = min(dis[k][j], dis[k][k] + dis[k][j])
        显然是无效更新

---

```cpp
#include <algorithm>
#include <iostream>
#include <cstring>
using namespace std;
const int N = 210;
int dis[N][N];
int n, m, k;
void floyd() {
	for (int k = 1; k <= n; k++) {
		for (int i = 1; i <= n; i++) {
			for (int j = 1; j <= n; j++) {
				dis[i][j] = min(dis[i][j], dis[i][k] + dis[k][j]);
			}
		}
	}

}
signed main() {
	cin >> n >> m >> k;
	for (int i = 1; i <= n; i++)
		for (int j = 1; j <= n; j++)
			if (i == j)dis[i][j] = 0;
			else dis[i][j] = 0x3f3f3f3f;
	while (m--) {
		int x, y, z;
		cin >> x >> y >> z;
		dis[x][y] = min(dis[x][y], z);
	}
	floyd();
	while (k--) {
		int x, y;
		cin >> x >> y;
		if (dis[x][y] > 0x3f3f3f3f / 2)cout << "impossible\n";
		else cout << dis[x][y]<< '\n';
	}
	return 0;
}

```