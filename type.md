# 类型


## 字符串

| 类型        | 用途      | 大小      | 字面字符串前缀 |
| ------      | -----    | -----     | -----         |
| wchar_t     | 宽字符   | 16bit      | L         |
| char16/32_t | Unicode  | 16/32bit  | u/U       |

前缀 `u8` 仅用于字符串字面常量.

较大的 `char` 类型（`wchar_t char16_t char32_t`）提升成 `int, unsigned int, long, unsigned long,  ll, unsigned ll` 中能容纳的最小类型.


## 整型

无符号溢出取模，带符号溢出未定义.

表达式中同时有无符号和带符号会转为无符号（不混用）.

无符号与带符号运算,无符号不小于带符号,那么带符号转为无符号.（大于时依赖机器）

十进制字面值为带符号数，八进制十六进制都可能.

\三个八进制数，\x后面所有十六进制数


## 变量声明 初始化

**C++11** 列表初始化所有变量：
```cpp
int price = {0};
int price{0};
int price(0);
```
有丢失精度风险时有编译器报错.

`extern` 且不显式初始化变量 -> 声明.

标识符（变量名）不能 `__` 开头，不能 `_[A-Z]` 开头，函数体外不能 `_` 开头.

复合类型由基本数据类型和声明符组成.（声明符只适用于邻近的变量）

**C++11** 别名声明：using Myint = int;


## 指针 引用 

引用一般指左值引用.

赋值表达式的类型是左值类型的引用.

`int *&r = p;` 表示 r 是对 p 的引用（从右向左）.

**C++11** nullptr 可转为任意指针类型.

NULL 在 cstdlib 定义为 0.


## 数组

数组声明由内向外.

**C++11** begin(数组) end(数组) （函数定义位于 `<iterator>`）

内置类型的下标运算符索引值是有符号数，而标准库类型下标索引是无符号数.

用数组初始化 vector：`vector<type> name(begin(arr), end(arr));`


## const

一般，const 只在一个文件内有效（solution: `extern`）.

初始化常量引用只需结果可转为匹配类型.（绑定不同类型非常量非法）

常量引用可绑定非常量.

底层 const：指向常量的指针 `const type *`

顶层 const：const 指针 `type *const`


## **C++11** 新增类型说明/指示符

### `constexpr` 类型由编译器检查是否是常量表达式.

### `auto` 类型说明符

+ 一般忽略顶层 const，保留底层 const.

+ 数组作为初始值推断为指针.（多维数组循环中，外层应声明为引用，避免转为指针）

### `decltype` 类型指示符

+ 保留 const 及引用.

+ `decltype((var))` 的结果永远是引用.

+ 数组推断仍为数组.

+ 左值推断为引用。


## 强制类型转换

强制类型转换：`cast-name<type>(expression)`

type 是引用类型时返回左值.

+ `static_cast` 只要不含底层 const

+ `dynamic_cast`

+ `const_cast` 只能加/去掉底层 const

+ `reinterpret_cast` 在位上重新解释

