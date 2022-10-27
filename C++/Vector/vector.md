
迭代器类似于指针
`.begin() `返回第一个元素迭代器
`.end() `返回尾部，最后一个元素 + 1
`.clear()` 清空数组
`.begin `和`.end` 加上  * 可以解除引用
相当于`a[0].end`同理

`.front() `返回`a[0]`
`.back()` 返回`a[a.size() - 1]`

`.push_back(a)` 数组尾部再接上一个值a
`.pop_back()` 删除最后一个元素
`.resize(length, num) `length为指定长度，num如果扩容后新元素的初始值
