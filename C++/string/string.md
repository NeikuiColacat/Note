# string

### 成员函数find
参数为子串 ， 查找成功返回子串开始的下标位置，查找失败返回-1

### string数组排序

sort中的参数不能够填写 `a.begin() , a.end()` 这样是针对一维

## 正确写法:
```cpp
string s[100];
sort(s,s+100);
```
