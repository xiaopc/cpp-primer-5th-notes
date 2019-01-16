# 语句

**C++11** range for:

`for (declaration : expression)`

`expression` 必须为一个序列, 有能返回迭代器的 `begin end`. 语句体内不应改变遍历序列的大小.

`case` 标签必须为整型常量表达式.

从作用域之外初始化变量之处跳转到作用域之内处为非法.

**C++11** 模板实例化 `template<template<type>>` 不需要在 `>` 间加空格。 C++ 11 前 VC++ 也不用
