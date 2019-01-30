# STL 容器

`vector` 可变大小数组 支持快速随机访问, 在除尾部外插删慢

`deque` 双端队列  支持快速随机访问, 在头尾部插删快

`list` 双向链表 只支持双向数据访问, 插删快

**C++11** `forward_list` 单向链表 只支持单向数据访问, 插删快

**C++11** `array` 固定大小数组 支持快速随机访问

`string` 与 `vector` 类似


## 类型别名

`(const_)iterator`

`difference_type`（迭代器之间距离）

`size_type` `value_type` 

`(const_)reference`（==`value_type&`）


## 构造函数

```cpp
C c;
C c1(c2); // 需为相同元素同类型, array 还需同大小
C c(b, e); // 将迭代器 b,e 范围内元素拷贝构造, array 不支持
C c{a, b, …};
// 只有顺序容器（除 array ）构造函数接受大小参数
C seq(n); // explicit, string 不适用
C seq(n, t);
```


## 赋值 交换

```cpp
c1 = c2;
c1 = {a, b, …}; // array 不支持
// 赋值会导致指向左边容器内部的迭代器 引用 指针失效
a.swap(b); //（== swap(a, b) C++11）
// 而 swap 不会, 除 array string 外
// 除 array 外,  O(1)
```


## `assign` （仅除 `array` 外的顺序容器）

```cpp
seq.assign(b, e); // 替换为迭代器 b,e 范围内元素, b e 不能指向 seq
seq.assign(il); // 替换为初始化列表 il 中的元素
seq.assign(n, t);
```


## 大小

```cpp
c.size(); // forward_list 不支持
c.max_size();
c.empty()
```


## 增删（`array` 不支持）, 不同容器接口不同

`insert emplace erase clear`


## 比较运算

无序关联容器不支持大于小于比较运算

需元素支持 `<` 运算符


## 获取迭代器

`(c)begin`, `(c)end`


## 反向容器成员（`forward_list` 不支持）

`(const_)reverse_iterator`

`(c)rbegin, (c)rend`

**C++11** c 开头的 const 版本


## 顺序容器添加元素

`forward_list` 有专有版本 `insert` `emplace`, 不支持 `push_back` `emplace_back`

`vector` `string` 不支持 `push_front` `emplace_front`

```cpp
c.insert(p, n, t) // 迭代器 p 指向的元素前插入 n 个 t, 返回指向新添加的第一个元素的迭代器 **C++11**
c.insert(p, b, e) // 将迭代器 b e 范围内元素插入到迭代器 p 指向的元素前,返回…
c.insert(p, il) // il 是 {} 包围的元素列表
```

> 容器元素是拷贝

**C++11** `emplace`（`front back`）构造而不是拷贝元素（将参数传给构造函数）


## forward_list 操作

```cpp
(c)before_begin() 首前迭代器
insert_after(p, t) (p, n, t) (p, b, e) (p, il)
emplace_after(p, args)
erase_after(p) (b, e) // 从b之后到e(不含)之前
```


## list forward_list 特定算法

```cpp
lst1.merge(lst2) // 都必须有序, 将清空 lst2
lst1.merge(lst2, comp)
lst.remove(val)
lst.remove_if(predicate)
lst.reverse()
lst.sort()
lst.sort(comp)
lst.unique()
lst.unique(predicate)
lst.splice(args)
lst.splice_pafter(args)
// (p, lst2) p 是 指向 lst 中元素的迭代器或指向 flst 首前位置迭代器,  将 lst2 全部内容移动到 p 前或 flst 后, 清空 lst2
// (p, lst2, p2) p2 是指向 lst2中元素迭代器, 将 p2 指向的元素移动到 lst 中, 或将 p2 后移动到 flst 中, lst2 可以与 lst flst 相同
// (p, lst2, b, e) b e 表示 lst2 中合法范围, lst2 可以相同 但 p不能指向给定范围内元素
```


## 大小管理

```cpp
shrink_to_fit() // vector string deque, 并不保证退还
capacity() // vector string, 下同
reserve(n) // 分配至少能容纳 n 个元素的空间
```


## 修改 string

```cpp
insert(pos, args) // pos 可以为下标或迭代器, 接受下标的版本返回引用, 接受迭代器的版本返回指向第一个插入字符的迭代器
erase(pos, len) // 返回引用,下同
assign(args)
append(args)
replace(range, args) // range 是一个下标或一个长度或一对迭代器
```

args 形式

    append assign 可以使用所有形式
    str 不能相同, b,e 不能指向原 string

+ str
+ str, pos, len
+ cp, len 字符数组 cp
+ cp
+ n, c
+ b, e
+ 初始化列表


## string 搜索

失败返回 `string::npos` （-1） 是 **unsigned** 类型

```cpp
find(args)
rfind(args)
find_first_of(args)
find_last_of(args)
find_first_not_of(args)
find_last_not_of(args)
```

args：
+ c, pos=0
+ str, pos=0
+ cp, pos C风格字符串
+ cp, pos, n

## 字符串数字转换

```cpp
to_string(val)
stoi(s, p=0, b=10) // b 表示转换所用基数, p 是 size_t 指针,用来保存第一个非数字字符下标
stol(s, p=0, b=10)
stoul(s, p=0, b=10)
stoll(s, p=0, b=10)
stoull(s, p=0, b=10)
stof(s, p=0)
stod(s, p=0)
stold(s, p=0)
```

## 适配器 

stack(deque) queue(deque) priority_queue(vector)
