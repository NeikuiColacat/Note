# Sort 函数 cmp使用方法
在用sort对结构体进行排序的时候
我们需要进行
定义一个cmp函数
```c++
Bool cmp(struct a,struct b){
    //默认是升序
    return a>b;//这是降序
}
signed main(){
    sort(a,a+n,cmp);
    sort(a,a+n,greater<int>);//降序
    sort(a,a+n,less<int>);//升序
}
```