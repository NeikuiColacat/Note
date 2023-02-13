## c++二分查找内置函数**:

---
### 升序排列
`upper_bound(arr.begin(),arr.end(),a)`查找数组第一个**大于**a的元素，返回迭代器

`lower_bound(arr.begin(),arr.end(),a) `查找数组中第一个**大于等于**a的元素，返回迭代器

---
### 降序排列
`upper_bound(arr.begin(),arr.end(),a,greater<int>())`查找数组第一个**小于**a的元素，返回迭代器

`lower_bound(arr.begin(),arr.end(),a,greater<int>()) `查找数组中第一个**小于等于**a的元素，返回迭代器