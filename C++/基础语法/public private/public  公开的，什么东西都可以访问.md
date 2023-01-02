
public : 公开的，什么东西都可以访问
private : 只有这个类的成员函数能够访问,属于同一个类的不同对象可以互相访问private中的成员。

struct 默认为 public
class 默认为 private

friend关键字可以授权给一个函数访问这个类中的private成员
friend一定要在定义类的时候给出

