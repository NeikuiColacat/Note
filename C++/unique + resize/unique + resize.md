##  unique 参数前闭后开 
##  unique只能用于排好序的数组,升序降序都可以
去重后的数组长度 ： `int length = unique(a.begin(),a.end())-a.begin()`返回去重后开区间的端点
## 删除重复元素
`a.resize(length)`