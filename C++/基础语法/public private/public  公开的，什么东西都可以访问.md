
public : 公开的，什么东西都可以访问
private : 只有这个类的成员函数能够访问,属于同一个类的不同对象可以互相访问private中的成员。

struct 默认为 public
class 默认为 private

friend关键字可以授权给一个函数访问这个类中的private成员
friend一定要在定义类的时候给出

初始化列表:
用于函数初始化类中的成员,在大括号中给值，不是初始化，相当于给这个变量初始化垃圾内存，再在函数大括号中赋值

而初始化列表是在一开始就初始化指定的数值
用法：
```c++
class A
{
private:
int i;

int j;
public:
void function(void):i(0),j(0){};

}
```
