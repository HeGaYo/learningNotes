# effective c++ 读书笔记
## 条款1
c++的四个主要的次语言：
- c，c++是以C为基础，比如说区块、语句、预处理、内置数据类型、数组、指针等，但是c的局限在于没有重载，没有模板，没有异常
- object-oriented c++：类（构造函数、析构函数）、封装、继承、多态、虚函数等
- template c++：泛型编程
- STL：容器、迭代器、算法以及函数对象的约束

## 条款2
尽量用const、enum、inline来替代define
define是在预处理器中被移走了，define定义的名称有可能没有进入记号表中。一般我们用常量来替代defines，
- #include、#ifdef/ifndef仍很重要
- 对于单纯变量，最好以const对象或者enums替换#defines
- 对于形似函数的宏，最好改用inline函数来替换#defines

## 条款3
尽可能使用const，某个值不能改变，编译器会严格执行
```
const Widget * pw//获得一个指针，指向一个常量（不变）的Widget对象
Widget const * pw
```
