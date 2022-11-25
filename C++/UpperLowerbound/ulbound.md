**c++二分查找内置函数**:

升序：

`upper_bound(arr.begin(),arr.end(),a)`查找数组第一个**大于**a的元素，返回迭代器

`lower_bound(arr.begin(),arr.end(),a) `查找数组中第一个**大于等于**a的元素，返回迭代器

降序数组要加个cmp函数，和sort同理，都是默认小于<


`upper`**小于**


`lower`**小于等于**