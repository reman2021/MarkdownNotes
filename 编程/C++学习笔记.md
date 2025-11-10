## 什么是对象

> 对象是类的实例，类定义了对象的属性和方法。

### 面向过程——C语言

在C中，需要先定义结构体存储属性，然后写函数（方法）来操作这些结构体。

```c
typedef struct point3d (
    float x;
    float y;
    float z;
} Point3d;

void Point3d_print(const Point3d* pd);
    
Point3d a;
a.x = 1; a.y = 2; a.z=3;
Point3d_print(&a);
```

### 面向对象——C++

在C++中，可以定义一个拥有这些属性和方法的对象，并直接调用。

```cpp
class Point3d (
public:
    Point3d(float X,float y,float z);
    print（）;
private:
    float x;
    float y;
    float z;
};
    
Point3d a(1,2,3);
a.print（）;
```

## 头文件

- #include：将文件内容插入到所在地方
- 头文件（`.h`）通常用 `extern` 声明全局变量或函数，供多个源文件（`.c`）共享。

> `extern` 的三大核心用途：
>
> 1. **跨文件共享全局变量**
>
>    ```cpp
>    // file1.c
>    int global_var = 42; // 定义全局变量
>    
>    // file2.c
>    extern int global_var; // 声明变量（不分配内存）
>    printf("%d", global_var); // 输出 42
>    ```
>
> 2. **在头文件中声明函数或变量**
>
>    ```cpp
>    // utils.h
>    extern int MAX_SIZE; // 声明变量
>    void print_message(); // 声明函数（函数默认是 extern 的）
>    
>    // utils.c
>    int MAX_SIZE = 100; // 定义变量
>    void print_message() { /* 实现 */ }
>    ```
>
> 3. **在 C++ 中链接 C 代码（`extern "C"`）**
>
>    C++ 支持函数重载，编译器会修改函数名（名称修饰），而 C 语言不会。用 `extern "C"` 告诉 C++ 编译器：“这段代码按 C 的规则编译”。
>
>    ```cpp
>    // C++ 文件
>    extern "C" {
>        #include "c_library.h" // 包含 C 语言库的头文件
>        void c_function();     // 按 C 规则编译函数
>    }
>    ```

标准头文件结构：

```
#ifndef HEADER_FLAG
#define HEADER_FLAG
...
//Type declaration here
...
#endif
```

## 抽象

**抽象（Abstraction）** 是一种编程技术，它的核心思想是 **隐藏复杂的实现细节，只暴露必要的接口给用户**。

抽象的实现：

1. **类（Class）的封装**

   通过将数据（属性）和操作（方法）封装在类中，隐藏内部实现细节，只暴露必要的接口。

2. **抽象类（Abstract Class）和纯虚函数**

   抽象类是一种特殊的类，它不能被实例化，只能作为基类。通过定义纯虚函数（`= 0`），强制派生类实现这些函数，从而实现接口的抽象。

   ```cpp
   class Shape {
   public:
       virtual void Draw() = 0; // 纯虚函数，强制派生类实现
   };
   
   class Circle : public Shape {
   public:
       void Draw() override {
           std::cout << "Drawing a circle!" << std::endl;
       }
   };
   
   int main() {
       Shape* shape = new Circle();
       shape->Draw(); // 通过基类指针调用派生类的实现
       delete shape;
   }
   ```

## 构造（Constructor）和析构（Destructor）

```Cpp
//
class X{
private:
	int i;
public:
	X(int i);//Constructor
	~X();//Destructor
};

class Y{
private:
	int i;
public:
	Y();//Default Constructor
	~Y();//Destructor
};

void main(){
    //进入scope，分配内存
    X x(1);//构造
    X x2[2]={X(1)};//会报错，因为类X没有默认构造函数
    Y y[2]={Y(1)};//不会报错
}
//离开scope，析构
```

## new & delete

> 在 C++ 中，`new` 和 `delete` 是用于动态内存管理的关键字。它们分别用于在堆（heap）上分配和释放内存。
>
> **`new` 的作用：**
>
> 1. **动态分配内存**：在堆上分配一块内存，并返回指向这块内存的指针。
> 2. **调用构造函数**：如果分配的是对象，`new` 会自动调用对象的构造函数。
>
> **`delete` 的作用：**
>
> 1. **释放内存**：将之前分配的内存归还给系统，避免内存泄漏。
> 2. **调用析构函数**：如果释放的是对象，`delete` 会自动调用对象的析构函数。

```cpp
#include <iostream>
using namespace std;

class A{
private:
    int i;
public:
    A(){ i = 0; cout << "A::()" << endl;}
    ~A{ cout << "A::~A()" << endl; }
    void set(int i){ this->i = i; } //当变量名相同时，会取最近的定义，这里用 this 指针说明是该对象的成员 i ，并将 set 函数参数 i 的值赋给该成员
}

void main(){
    int* p = new int; // 分配一个 int 类型的内存
	*p = 10;         // 在这块内存中存储值 10

	int* arr = new int[5]; // 分配一个包含 5 个 int 的数组
	arr[0] = 1;            // 访问数组元素
    
    delete p;   // 释放单个 int 的内存
	delete[] arr; // 释放数组的内存
    
    A* p = new A[10];//分配内存，调用构造函数
    for( int i=0; i<10; i++)
    {
        p[i].set(i);
    }
    delete[] p;//调用析构函数，释放内存
}
//注意：new 和 delete、new[] 和 deltee[] 配对使用；new 完记得 delete 避免内存泄漏；避免重复释放同一块内存；可以 delete 一个空指针。
```

## 



