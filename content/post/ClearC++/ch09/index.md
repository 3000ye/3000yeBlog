---
title: "Clear C++ Ch09: Function application"
description: "Clear C++ Ch09: Function application"
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

