---
title: "Clear C++ Ch09: Function application"
description: "template, build, compile"
date: 2024-03-21T23:12:32+08:00
image: assets/clearcpp.jpg
math: true
toc: true
categories:
    - Clear C++
tags:
    - CPP
    - Clear C++
---

# 函数的应用

## 函数模板

### 函数模板和模板函数

当我们在编写函数时，若两个函数如下所示，只存在变量类型的差异：

```cpp
int intSolve(int a, int b) { return a > b ? a : b; }

double doubleSolve(double a, double b) { return a > b ? a : b; }
```

此时我们当然可以直接复制其中一个函数，然后修改其中的类型来实现我们的需求，但是这样会增加代码的冗余和出错的可能性。

我们可以发现，如果不管变量是任何类型，函数都可以正常运行就好了。
在 `CPP` 中可以使用 **泛型** （genericity）函数来实现，基于泛型实现的函数称为 **泛型函数** ：

```cpp
template <class T>
T solve(T a, T b) { return a > b ? a : b; }
```

其中前缀 `template <class T>` 表明接下来声明的是 **函数模板**（function template），而不是普通函数，接收的 **类型** 要赋给函数的形参 `T`（`T` 可以取任意名称）。

调用时直接使用函数模板即可：

```cpp
long a = 2, b = 3;
cout << solve(a, b) << endl;
```

在使用函数模板时，编译器会自动查找传入参数的类型，并将函数模板的 `T` 修改为对应类型，这样创建的函数实体称为 **模板函数**（template function）。

在创建模板函数时，如果传入的参数类型错误，则会引发报错：

```cpp
long a = 2, b = 3;
short c = 4;
cout << solve(a, c) << endl;

error generated: 
candidate template ignored: deduced conflicting types for parameter 'T' ('long' vs. 'short')
```

### 显式实例化

在上文中我们提到，在创建模板函数时如果传入的参数类型错误则会引发报错，那么有没有方法可以解决这种报错呢？

`CPP` 提供了 **显式实例化** 的方法来创建模板函数：

```cpp
long a = 2, b = 3;
short c = 4;
cout << solve<long>(a, c) << endl;
```

使用显式实例化的方式创建模板函数，函数会使用指定的类型进行实例化。

### 显式特例化

虽然函数模板可以对任意类型的变量起作用，但是对于例如 `string` 类型的变量：

```cpp
cout << solve("ABC", "EFG") << endl;
```

这样实例化的模板函数在功能上来说是没有意义的，因为实际比较的是两个字面量的地址而非 `string` 的实际大小。因此，对于这种情况，我们需要特例化一个模板函数：

```cpp
template <> const char* solve<const char*> (const char* a, const char* b) {
    return strcmp(a, b) ? a : b;
}

int main() {
    cout << solve<const char*>("EFG", "ABC") << endl;
    return 0;
}
```

显式特例化的定义一般为：

```cpp
template <> 返回值类型 func<T> (入参) { 函数体 }
```

## 大规模程序的开发

### 分离式编译和链接

在大型项目开发中，我们常常会使用多个源文件来管理和开发不同模块，如下面所示：

```cpp
// test1.cpp
#include "iostream"
using namespace std;

const int MAX = 10;  // 定义常量
int solve(int a, int b);  // 声明函数

int main() {
    int a = 2, b = 3;
    cout << solve(a, b) << endl;

    return 0;
}

// ---------------------------------------
// test2.cpp
extern int MAX;  // 声明变量的使用

// 定义函数
int solve(int a, int b) {
    return a > b ? MAX : a - b;
}
```

在编译时分别对不同源文件进行编译，然后链接在一起：

```shell
clang++ -c test1.cpp -o test1.o
clang++ -c test2.cpp -o test2.o
clang++ test1.o test2.o -o test
```

在 `CPP` 程序中，需遵循 **单一定义规则**（One Definition Rule, ODR）：对象和函数只能定义一次。

因此，当我们在 `A.cpp` 中定义了某个对象或函数，想在 `B.cpp` 中使用时，就必须使用 `extern` 关键字进行声明。

同时，如果我们在 `A.cpp` 中定义了某个对象或函数，不想让其他文件使用该对象或函数，可以使用 `static` 关键字进行声明和定义：

```cpp
// test1.cpp
static const int MIN = 10;

// ---------------------------------------
// test2.cpp
extern const int MIN;
// clang++: error: linker command failed with exit code 1
```

如上所示，使用 `static` 声明和定义的对象和函数只能在其源文件中使用的情况，称为 **内部链接**（internal linkage）。此外，对于该程序中没有使用的以下函数或对象，即时没有 `static`，也会被自动赋予内部链接：

- 内联函数
- `const` 定义的常量对象

### 头文件

当源文件数量增加时，为了方便管理和维护，我们使用头文件来集中管理具有外部链接的变量和函数等的声明。

```cpp
// test.hpp
const int MAX = 10;
int solve(int a, int b);
```

注意：使用自定义的头文件时，要用 `"..."` 而不是 `<...>`，其区别在于：

- `#include <...>` 会优先查找存储编译器提供标准库的地方。
- `#include "..."` 会优先查找源文件所在目录。

## 命名空间

### 命名空间的定义

作用域依赖于源文件中的声明的物理位置，名称的通用范围依赖于源文件这样的物理单元，这些都是从 `C` 语言继承过来的性质。

`CPP` 对此进行了改良，使用 **命名空间**（namespace）来控制每个标识符的通用范围：

```cpp
#include <iostream>

namespace en {
    int x = 1;
    void print() {
        std::cout << "en: " << x << std::endl;
    }
}

namespace zh {
    int x = 3;
    void print() {
        std::cout << "zh: " << x << std::endl;
    }
}

int main() {
    en::print();
    zh::print();
}
```

### 命名空间成员的声明和定义

属于命名空间的变量和函数等叫作 **命名空间成员**（namespace member）。可以在命名空间定义中只 **声明** 命名空间成员，在其他地方 **定义** 成员。

```cpp
// 声明
namespace jp {
    extern int x;
    void print();
}

// ---------------------------------------
// 定义
int jp::x = 4;
void jp::print() {
    std::cout << "jp: " << x << std::endl;
}
```

### 嵌套命名空间

```cpp
namespace Outer {
    int x;

    namespace Inner {
        int x;
    }
}
```

在命名空间 `Outer` 中定义的 `x` 使用 `Outer::x` 访问，在命名空间 `Inner` 中定义的 `x` 使用 `Outer::Inner::x` 访问。

### 无名命名空间

