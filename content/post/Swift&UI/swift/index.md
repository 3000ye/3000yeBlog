---
title: Swift Tutorial
description: Swift Tutorial
date: 2024-04-25T00:28:05+08:00
image: assets/swift.png
math: true
toc: true
categories:
    - Swift
tags:
    - Swift
---

# Swift 教程

## Swift 基础
### 常量和变量
#### 声明常量和变量

在 Swift 中，常量使用 `let` 进行声明，变量使用 `var` 进行声明：

```swift
let MAX = 10;
var intVar = 20;
```

#### 类型注解

在 Swift 中，程序会根据声明的值来自动分析标识符的类型，同时也提供了显示指定类型的方法：

```swift
var intVar:int = 10;
var doubleVar:double = 10;

print("intVar = \(intVar)");
print("doubleVar = \(doubleVar)")

// --------------- 输出 --------------------
// intVar = 10
// doubleVar = 10.0
```

需要注意的是，若只不在声明时定义标识符的值，则必须指定类型：

```swift
var testVar: String;
testVar = "test var";
print(testVar)

// --------------- 输出 --------------------
// test var
```

### 整数

Swift 提供了8、16、32和64位的有符号和无符号整数类型。

#### 整数范围

可以访问不同整数类型的 `min` 和 `max` 属性来获取对应类型的最小值和最大值：

```swift
let minValue = UInt8.min  // minValue 为 0，是 UInt8 类型
let maxValue = UInt8.max  // maxValue 为 255，是 UInt8 类型
```

