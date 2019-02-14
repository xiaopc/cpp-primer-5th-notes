# STL 容器

# 顺序容器

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

# 关联容器

有序关联容器 `map multimap set multiset` 

必须定义关键字类型的 `<` 的运算符, 定义一个“严格弱序”（“小于等于”）

使用自定义比较函数：`multiset<type, decltype(comp) *> ms(comp);`

```cpp
pair<utility>
pair<T1, T2> p(v1, v2);
pair<T1, T2> p = {v1, v2};
make_pair(v1, v2);
p.first
p.second
p1 relop p2 //（关系运算符按字典序, <）
```

**C++11** 返回 pair 的函数:
```
pair<T1, T2>
func(…){
  return {v1, v2};
  return pair<T1, T2>(v1, v2); // 原, 也可 make_pair
}
```

## 关联容器额外类型别名

+ `key_type`
+ `mapped_type`（只有 `map multimap unordered_map unordered_multimap`）
+ `value_type`（ set 与 `key_type` 相同, map 为 `pair<const key_type, mapped_type>`）


## 关联容器 insert
```cpp
c.insert(value_type) // 返回 pair, 包含一个指向给定关键字元素迭代器 , 以及指示插入是否成功 bool （不允许重复关键字容器）
c.emplace(args) // 同上
c.insert(b, e) // c::value_type, 返回 void
c.insert(p, v) // 同上
c.emplace(p, args) // 从 p 开始搜索新元素存储位置, 返回指向给定关键字元素迭代器
```

## 桶

无序容器在存储上组织为一组桶

```cpp
// 桶接口
c.bucket_count() // 正在使用桶数
c.max_bucket_count() // 最大桶数
c.bucket_size(n) // 第 n 桶有多少元素
c.bucket(k) // k 在哪个桶
// 桶迭代
(const_)local_iterator // 可用来访问桶中元素的迭代器类型
c.(c)begin, c.(c)end // 桶 n 的首元素/尾后元素迭代器
// 哈希策略
c.load_fractor() // 每桶平均元素数，float
c.max_load_fractor() // 试图维护平均桶大小，float
c.rehash(n) // 重组存储， 使 bucket_count>=n，bucket_count>size/max_load_factor
c.reserve(n) // 重组存储，使 c 可以保存 n 个元素且不必 rehash
```

## 对关键字类型要求

默认使用`==`比较元素，还使用 `hash<key_type>` 类型对象生成每个元素 hash 值

自定义类型(不提供 hash 模板版本)：
```cpp
size_t hasher(const MyType &sd) {
    return hash<built_in_type>()(...);
}
bool eq(const MyType &lhs, const MyType &rhs){
    return ... == ...;
}
using MyType_multiset = unordered_multiset<MyType, decltype(hasher)*, decltype(eq)*>;
MyType_multiset instance(BUCKET_SIZE, hasher, eq);

// 若已定义 ==，则直接：
unordered_set<MyType, decltype(hasher)*> instance(BUCKET_SIZE, hasher);
```
