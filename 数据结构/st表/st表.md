# st表

```cpp
int len , mlg = __lg(len);
vector<vector<int>> ST(len + 1, vector<int>(mlg+2));
for (int i = 1; i <= len; i++) ST[i][0] = a[i];
for (int j = 1; j <= mlg; j++) {
    int lenj = 1 << j;
    for (int i = 1; i + lenj - 1 <= len; i++) {
        ST[i][j] = get(ST[i][j - 1], ST[i + (lenj >> 1))][j - 1]);
    }
}

T query(int l, int r) {
    int len = r - l + 1;
    int mlg = __lg(len);
    return op(ST[l][mlg], ST[r - (1 << mlg) + 1][mlg]);
}
```
