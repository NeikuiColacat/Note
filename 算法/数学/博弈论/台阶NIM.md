# 定理 
## 先手必胜 : 奇数台阶上的石子异或数值不为0
## 先手必败 ；奇数台阶上的石子异或数值为0

### 证 ：
#### 若奇数台阶上的石子异或数值不为0
先手能够让$a_1\wedge a_3\wedge ....\wedge a_{2n-1}=0$

后手若移动奇数台阶上的石子，那么奇数台阶上的石子异或值一定不为0,先手再次将其变为0。

后手若移动偶数台阶上的石头，那么只要先手再移动偶数台阶下一级的奇数台阶上的石子，就能保证奇数台阶上的石子不变,下一轮到后手的时候，奇数台阶上的石子异或值仍然为0

所以奇数台阶上异或值全为0的情况总是被后手遇到

而奇数台阶异或值全为0的情况属于全部台阶全为0情况的一种，所以台阶全为0的情况总是会被后手遇到

```cpp
#include <iostream>
int n;
using namespace std;
signed main(){
    cin>>n;
    int res =0;
    for(int i =1;i<=n;i++){
        int x;
        cin>>x;
        if(i&1)res^=x;
    }
    if(res) cout<<"Yes\n";
    else cout <<"No\n";
}
```