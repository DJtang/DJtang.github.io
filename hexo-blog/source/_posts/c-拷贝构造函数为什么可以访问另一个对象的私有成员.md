---
title: c++拷贝构造函数为什么可以访问另一个对象的私有成员
categories: [c++]
tags: [c++对象]
---



-----------------------------------------





-------------------------------------------------------------

```c++
class Test{
public:
    /* 默认构造函数 */
    Test(int _value = 0):value(_value){}

    /* 复制构造函数 */
    Test(const Test& rhs){
        this->value = rhs.value;
    }

    void print(const Test& rhs){
        cout<<rhs.value<<endl;
    }

private:
    int value;
};

int main(){
    Test t(1);
    Test t2(t);
    Test t3(2);
    /* 通过对象public函数访问另一个对象的私有变量 */
    t3.print(t2); 
    // cout<<t2.value<<endl; // 通过对象访问私有成员变量，编译出错
    return 0;
}
```

​        **封装是编译期的概念，是针对类型而非对象的，在类的成员函数中可以访问同类型实例对象的私有成员变量**

具体的解析如下：**从变量value的符号是怎么解析的分析**．

**1.确定符号的查找域**

当编译器发现value变量时，它会在value变量所属的对象rhs的类域中寻找该符号．

**2.确定当前域中哪些符号可以访问**

由第1步可知，当前查找的域是类域，而print函数在Test类体中，所以print可以访问Test类中的所有变量(包括私有成员变量)，因而value符号在Test类域中被找到．

main函数不在Test类体中，所以main函数不可以访问Test类域中的私有成员变量．

**3.符号已查找到，编译通过**

类成员变量的访问权限是编译器强加的，编译器可以找到value，通过编译，自然就可以访问到value变量的值．

**直觉上，我们会以为代码中value符号的查找域应该是对象rhs对应的作用域，然而C++编译器的实现却是在对象rhs的类域查找value符号．**



参考文献：

1. [c++私有成员变量的理解](https://www.cnblogs.com/dwdxdy/archive/2012/07/17/2595741.html)
