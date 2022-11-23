# lambda 表达式

`[捕获列表]  (参数列表)  函数选项 -> 返回类型{函数体}`
- 一般来说不需要返回类型，但是有多个return的时候需要
- 捕获列表有按值捕获和引用捕获，`&`  `=` 
- 函数选项一般是`mutable`通常来说按值捕获都是const，加上该关键字后就可修改


```cpp
vector<pair<int,int>> costs;//costs的每个元素是由价值与编号组成的pair
sort(costs.begin(), costs.end(), [&](const auto & a, const auto & b)
    {
        if (a.first != b.first)
            return a.first > b.first;//价值不同时，价值大的优先
        else
            return a.second < b.second;//价值相同时，标号小的优先
    });

vector<pair<int,int>> costs;
auto compare = [&](const auto& a,const auto& b ){
        if (a.first != b.first)
            return a.first > b.first;//价值不同时，价值大的优先
        else
            return a.second < b.second;//价值相同时，标号小的优先
}
sort(costs.begin(),costs.end(),compare);
```
