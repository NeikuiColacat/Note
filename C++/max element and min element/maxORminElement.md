### 前闭后开，求一段区间中的最大或最小值，返回地址

`max_element()`

`min_element()`


###  需要解引用使用
`*max_element()` 


### 求下标的时候
`int *pos = max_element(a,a+n) - a  `

#include <iostream>
#include <algorithm>
#include <vector>
#define int long long
using namespace std;
void solve() {
}
signed main() {
	int t;
	cin >> t;
	while (t--) {
		string s;
		cin >> s;
		int i = 0, j = i + 1, ans = 0;
		while (j + 1 < s.size()) {
			if (s[i] == s[j]) {
				i+=2, j+=2;
				continue;
			}
			else {
				ans++;
				if (s[j + 1] == s[j]) {
					i = j + 1;
					j = i + 1;
				}
				else if (s[i] == s[j + 1]) {
					i += 3;
					j = i + 1;
				}
				else {
					ans++;
					i += 2;
					j = i + 1;
				}
			}
			int len = s.size() - ans;
			if (len & 1)ans++;
		}
		cout << ans << '\n';
	}
	return 0;
}