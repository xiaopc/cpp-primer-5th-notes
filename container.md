# STL 容器

`vector` 可变大小数组 支持快速随机访问, 在除尾部外插删慢

`deque` 双端队列  支持快速随机访问, 在头尾部插删快

`list` 双向链表 只支持双向数据访问, 插删快

**C++11** `forward_list` 单向链表 只支持单向数据访问, 插删快

**C++11** `array` 固定大小数组 支持快速随机访问

`string` 与 `vector` 类似


## 容器操作

### 类型别名

`(const_)iterator`

`difference_type`（迭代器之间距离）

`size_type` `value_type` 

`(const_)reference`（==`value_type&`）

### 构造函数

```cpp
C c;
C c1(c2); // 需为相同元素同类型, array 还需同大小
C c(b, e); // 将迭代器 b,e 范围内元素拷贝构造, array 不支持
C c{a, b, …};
// 只有顺序容器（除 array ）构造函数接受大小参数
C seq(n); // explicit, string 不适用
C seq(n, t);
```

### 赋值 交换

```cpp
c1 = c2;
c1 = {a, b, …}; // array 不支持
// 赋值会导致指向左边容器内部的迭代器 引用 指针失效
a.swap(b); （== swap(a, b) C++ 11）
// 而 swap 不会, 除 array string 外
// 除 array 外,  O(1)
```

### `assign` （仅除 `array` 外的顺序容器）

```cpp
seq.assign(b, e); // 替换为迭代器 b,e 范围内元素, b e 不能指向 seq
seq.assign(il); // 替换为初始化列表 il 中的元素
seq.assign(n, t);
```

### 大小

```cpp
c.size(); // forward_list 不支持
c.max_size();
c.empty()
```

### 增删（`array` 不支持）, 不同容器接口不同

`insert emplace erase clear`

### 无序关联容器不支持大于小于比较运算, 元素支持 `<` 运算符

### 获取迭代器

`(c)begin, (c)end`

### 反向容器成员（`forward_list` 不支持）

`(const_)reverse_iterator`

`(c)rbegin, (c)rend`

**C++11** c 开头的 const 版本
