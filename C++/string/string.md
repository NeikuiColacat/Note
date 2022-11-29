# string

### 成员函数find
参数为子串 ， 查找成功返回子串开始的下标位置，查找失败返回-1

## 成员函数substr
`a.substr(pos)` 返回pos开始的字符串，下标从0开始
`a.substr(st,len)` 返回st开始，长度为len的字符串，前闭后开

### string数组排序

sort中的参数不能够填写 `a.begin() , a.end()` 这样是针对一维

## 正确写法:
```cpp
string s[100];
sort(s,s+100);
```
