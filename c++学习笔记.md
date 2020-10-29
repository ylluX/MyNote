# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
* [目录](#目录)
* [基础知识点](#基础知识点)
   * [1. 指针](#1-指针)
   * [2. 变量](#2-变量)
   * [3. typedef 和 #defind](#3-typedef-和-defind)
* [define只是作简单的字符串替换，不表达 任何含义。如：](#define只是作简单的字符串替换不表达-任何含义如)
* [define是一个宏定义命令，用来定义一个常量(包括无参常量和有参常量)，它本身并不在编译过程中执行，而是在预处理阶段就已经完成了，](#define是一个宏定义命令用来定义一个常量包括无参常量和有参常量它本身并不在编译过程中执行而是在预处理阶段就已经完成了)
* [特殊场景](#特殊场景)
   * [1. 两个类相互调用](#1-两个类相互调用)
<!--te-->

----

# 基础知识点

## 1. 指针

**指针与C++基本原理**

面向对象编程与传统的过程性编程的区别在于，OOP强调的是在运行阶段（而不是编译阶段）进行决策。
运行阶段指的是程序正在运行时，编译阶段指的是编译器将程序组合起来时。运行阶段决策就好比度假
时，选择参观那些景点取决于天气和当时的心情；而编译阶段决策更像不管在什么条件下，都坚持预先
设定的日程安排。

运行阶段决策提供了灵活性，可以根据当时的情况进行调整。例如，考虑为数组分配内存的情况。传统
的方法是声明一个数组。要在C+中声明数组，必须指定数组的长度。因此，数组长度在程序编译时就设
定好了；这就是编辑阶段决策。虽有可能在80%的情况下，一个包含20个元素的数组足够了，但程序有
时需要处理200个元素。为了安全起见，使用了一个包含200个元素的数组。这样，程序在大多数情况下
都浪费了内存。OOP通过将这样的决策推迟给运行阶段进行，使程序更灵活。在程序运行后，可以这次
告诉它只需要20个元素，而且还可以下次的时候告诉它需要205个元素。

总之，使用OOP时，您可以在运行阶段确定数组的长度。为了使用这种方法，语言必须允许在程序运行时
创建数组。C++采用的方法是，使用关键字new请求正确数量的内存以及使用指针来跟踪新分配的内存的
位置。

在运行阶段作决策并非OOP独有的，单使用C++编写这样的代码比使用C语言简单。

* 在C++中创建指针时，计算机将分配用来存储地址的内存，但不会分配用来存储指针所指向的数据的内存。


**数组的地址**

对数组取地址时，数组名不会被解释为其地址。等等，数组名难道不被解释为数组的地址吗？不完全如
此：数组名被解释为其第一个元素的地址，而对数组名应用地址运算符（即&）时，得到的是整个数组
的地址：

```
short tell[10];        //声明一个长度为20字节的数组（short型变量大小为2字节）
cout << tell << endl;  //显示&tell[0]
cout << &tell << endl; //显示整个数组的地址
```

从数字上说，这两个地址相同；但从概念上说，&tell[0]（即tell）是一个2字节内存块的地址，而&tell
是一个20字节内存块的地址。因此，表达式tell+1将地址值加2，而表达式&tell+1将地址值加20。换句话
说，tell是一个short指针（short*），而&tell是一个指向包含10个元素的short数组的指针
（short(*) [10]）。

您可能会问，前面有关&tell的类型描述是如何来的呢？首先，您可以这样声明和初
始化这种指针：

```
short (*pas) [10] = &tell; //pas指向一个有10个short元素的数组
```

如果省略括号，优先级规则将使pas先与[10]结合，导致pas是一个包含10个short型指针的数组，因此括
号是必不可少的。其次，如果要描述变量的类型，可将声明中的变量名删除。因此，pas的类型为
short(*) [10]。另外，由于pas被设置为tell，因此*pas与tell等价，所以(\*pas) [0]为tell数组的第一
个元素。

* short  * p  [20] : 有20个元素的short指针数组
* short (* p) [20] : 指向包含20个元素的short数组的指针


**chr\*指针**

```
int a = 10;
int * p1 = &a;
cout << p1 << endl;  //打印变量a的地址

chr * b[10] = "bear";
chr * p2 = b;
cout << p2 << endl;  //打印字符串"bear"
count << (int *) p2 << endl;  //打印字符串数组的地址
```

一般来说，如果给cout提供一个指针，它将打印地址。但如果指针的类型为 chr \*, 则cout将显示指向的
字符串。如果要显示的是字符串的地址，则必须将这种指针强制转换为另一种指针类型，如 int \* （上面
的代码就是这样做的）。因此，p2显示为字符串"bear"，而(int \*) p2 显示为该字符串的地址。


**指针常量和常量指针**

在面试中我们经常会被面试官问到什么是常量指针，什么又是指针常量。可能第一次被问到都会有些懵逼。

***指针常量***

指针常量：顾名思义它就是一个常量，但是是指针修饰的, 格式为：

```
int * const p //指针常量
```

在这个例子下定义以下代码：

```
int a，b；
int * const p=&a //指针常量

//那么分为一下两种操作
*p=9;  //操作成功
p=&b;  //操作错误
```

因为声明了指针常量，说明指针变量不允许修改。如同次指针指向一个地址**该地址不能被修改，但是该地址里的内容可以被修改**

***常量指针***

常量指针：如果在定义指针变量的时候，数据类型前用const修饰，被定义的指针变量就是指向常量的指针变量，指向常量的指针变量称为常量指针，格式如下

```
const int *p = &a; //常量指针
```

在这个例子下定义以下代码：

```
int a，b；
const int *p=&a   //常量指针

//那么分为一下两种操作
*p=9;  //操作错误
p=&b;  //操作成功
```

因为常量指针本质是指针，并且这个指针是一个指向常量的指针，**指针指向的变量的值不可通过该指针修改，但是指针指向的地址可以改变**。


**指向常量的指针常量**

```
const int * const b = &a;//指向常量的指针常量
```


## 2. 变量

| 变量 | 存储类型 | 生命周期 | 作用域 | 连接性 |
| ---- | ---- | ---- | ---- | ---- |
| 全局变量 | 静态 |   整个程序周期内   | 所有源文件 | 外部连接性 |
| 全局变量 | 静态 |   整个程序周期内   |  本源文件  | 内部连接性 |
| 局部变量 | 静态 |   整个程序周期内   |   函数内   |     无     |
| 局部变量 | 自动 | 函数周期或代码块内 |   函数内   |     无     |

*概念直接的联系*
* 存储类表明变量在哪里存储，生命周期表明什么时候为变量分配、收回内存，作用域表明变量起作用的范围
（代码块，函数域，文件域）；
* 存储类决定了生命周期，作用域决定了链接属性。
* 作用域表明变量起作用的范围（代码块，函数域，文件域）；
* 链接属性有外链接、内链接、空链接（不参与链接）。

*说明符*
* 声明引用外部全局变量，需要extern
* 对外部全局变量使用const，会将其外部连接性改成内部连接性，即该变量相当于内部全局变量
* 定义内部全局变量，需要static
* 定义静态局部变量，需要static
* 函数内存在同名局部变量，要使用外部全局变量需要 ::变量名

*规则*
* 外部全局变量要服从单定义规则(整个程序内只能有一处定义, 其它地方用extern来引用) 


## 3. typedef 和 #defind

`typedef` 用来为一个已有的数据类型起一个别名，而`#define`是用来定义一个宏定义常量。下面谈谈两者在实际使用中应当注意的地方。

**1.typedef关键字**

在C/C++中，我们平时写程序可能经常会用到typedef关键字和#define宏 定义命令，在某些情况下使用它们会达到相同的效果，
但是它们是有实质性的区别，一个是C/C++的**关键字**，一个是C/C++的**宏定义命令**，typedef是用来声明类型别名的，在
实际编写代码过程使用typedef往往是为了增加代码的可读性。它可以为一串很长的类型名起一个别名，那么使用这个别名可以
达到与原类型名相同的效果。如：

```
typedef int INT;
typedef char CHAR;
```

就为int和char分别起了一个别名，那么在程序中使用INT a;和int a;达到的效果是等同的。在使用typedef时应注意一下几点：

1) typedef是为一个数据类型起一个新的别名，如typedef int INT;那么要告诉我的是INT表示整型，
typedef int* INTPTR;则告诉我们INTPTR是一个指向整型变量的指针类型，这点与#define是决然不同的，
#define只是作简单的字符串替换，不表达 任何含义。如：

```
#define INTPTR1 int*
typedef int* INTPTR2;

INTPTR1 p1,p2;
INTPTR2 p3,p4;
```

INTPTR1 p1,p2;和INTPTR2 p3,p4;这两句的效果决然不同。INTPTR1 p1,p2;进行字符串替换后变成int* p1,p2;要表达的意义是声明
一个指针变量p1和一个整型变量p2；而INTPTR2 p3,p4;由于INTPTR2是具有含义的，告诉我们是一个指向整型数据的指针，那么p3和
p4都为指针变量，这句相当于int* p1,*p2;从这里可以看出，进行宏替换是不含任何意义的替换，仅仅为字符串替换；而用typedef
为一种数据类型起的别名是带有一定含义的。

再看下面这个例子：

```
#define INTPTR1 int*
typedef int* INTPTR2;

int a=1;
int b=2;
int c=3;
const INTPTR1 p1=&a;
const INTPTR2 P2=&b;
INTPTR2 const p3=&c;
```

上述代码中，const INTPTR1 p1表示p1是一个常量指针，即不可以通过p1去修改p1指向的内容，但是p1可以指向其他内容；
而对于const INTPTR2 p2，由于INTPTR2表示是一个指针类型，因此用const去限定，表示封锁了这个指针类型，
因此p2是一个指针常量，不可使p2再指向其他的内容， 但可以通过p2修改其当前指向的内容，INTPTR2 const p3同样声明的是一个指针常量。

2) 对于宏定义：

```
#define INT int
unsigned INT a;
```

这种用法是可行的；而

```
typedef int INT;
unsigned INT a;
```

是绝对错误的用法。

**2.#define宏定义**

#define是一个宏定义命令，用来定义一个常量(包括无参常量和有参常量)，它本身并不在编译过程中执行，而是在预处理阶段就已经完成了，
因此不作任 何正确性检查，只进行不关含义的字符串替换。在使用宏定义时，如果稍不注意就会发生错误，而且这个错误往往是你意想不到的。如：

```
#define ADD(a,b) a+b

int i=1;
int j=2;
int k=3;
int s=ADD(i,j)*k;
```

程序可能想求算的是(i+j)*k的结果，然而这段程序并没有达到这种效果，由于宏替换只是进行简单的字符串替换，那么ADD(i,j)*k相当于i+j*k，
并不是想象中的(i+j)*k。



# 特殊场景

## 1. 两个类相互调用

[C++两个类互相调用彼此的方法](https://blog.csdn.net/wuchuanpingstone/article/details/52384933?utm_source=app)

两个类A和B实现互相调用彼此的方法，如果采用彼此包含对方头文件的方式会出现循环引用，所以采用了类的前置声明的方式

1，class A采用前置声明的方式声明class B

2，在ClassB的头文件中包含class A 的头文件

3，在class A中只能声明class B类型的指针或者引用

具体代码如下：

A.h:

```c++
#pragma once
 
class B;
class A
{
public:
	A();
	A(class B* pB);
	~A();
 
public:
	void displayA();
	void invokeClassBInClassA();
private:
	class B *mB;
};
 
```

A.cpp

```c++
#include "A.h"
#include "B.h"
#include <iostream>
using namespace std;
 
 
A::A()
{
}
 
A::A(B * pB)
{
	mB = pB;
}
 
 
A::~A()
{
}
 
 
void A::displayA()
{
	cout << "this is A" << endl;
}
 
 
void A::invokeClassBInClassA()
{
	cout << "class A invoke class B starts>>" << endl;
	mB->displayB();
}
```

B.h

```c++
#pragma once
#include "A.h"
 
class B
{
public:
	B();
	~B();
 
public:
	void displayB();
	void invokeClassAInClassB();
private:
	class A * mA;
};
 
```

B.cpp

```c++
#include "B.h"
#include <iostream>
using namespace std;
 
 
B::B()
{
	mA = new A();
}
 
 
B::~B()
{
}
 
void B::displayB()
{
	cout << "this is the B" << endl;
}
 
void B::invokeClassAInClassB()
{
	cout << "class B invoke class A starts >>" << endl;
	mA->displayA();
}
```

main.cpp

```c++
 
#include <iostream>
#include "A.h"  
#include "B.h"
using namespace std;
 
 
 
int main()
{
	cout << "----------main starts---------------" << endl;
	class B* pB = new B();
	class A* pA = new A(pB);
 
	pA->displayA();
	pA->invokeClassBInClassA();
 
	
	pB->displayB();
	pB->invokeClassAInClassB();
 
	cout << "----------main  ends----------------" << endl;
	return 0;
}
```
