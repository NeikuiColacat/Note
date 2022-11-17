# n皇后问题
```cpp
#include <iostream>
using namespace std;
int n;
const int N = 100;
int dg[N], udg[N], col[N];
char ans[N][N];
void dfs(int D) {
	if (D == n) {
		for (int i = 0; i < n; i++) {
			puts(ans[i]);
		}
		puts("");
		return;
	}
	for (int i = 0; i < n; i++) {
		if (!col[i] && !dg[D+i] && !udg[D-i+n]) {
			ans[D][i] = 'Q';
			col[i] = dg[D+i] = udg[D-i+n] = 1;
			dfs(D + 1);
			col[i] = dg[D+i] = udg[D-i+n] = false;
			ans[D][i] = '.';
		}
	}
	return;
}
signed main() {
	cin >> n;
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			ans[i][j] = '.';
		}
	}
	dfs(0);
	return 0;
}
```