# STL 泛型

谓词 predicate:可调用的表达式, 一元谓词/二元谓词


## 泛型算法

```cpp
find(begin, end, value);
//找到返回指向它的迭代器, 找不到返回 end()
find_if(begin, end, predicate);

accumulate(begin, end, initial);  // (<numeric>)
//第三个参数的类型决定了使用哪个加法运算符 

equal(a_begin, a_end, b_begin);
//假定了第二个序列与第一个一样长

fill(begin, end, value);
fill_n(begin, length, value);

copy(source_begin, source_end, dest);
//返回值是 dest.end

replace(begin, end, search_for, replace_as);
replace_copy(begin, end, dest_begin, search_for, replace_as);

sort(begin, end);
sort(begin, end, predicate);
stable_sort(...);
unique(begin, end); // 返回指向不重复范围末尾的迭代器

for_each(begin, end, predicate);

transform(begin, end, dest_begin, predicate);

auto newCallable = bind(callable, arg_list);  // **C++11** <functional>
// arg_list 中可包括 _n 作为占位符, n 表示参数位置（从 1 开始）在 std::placeholder 中
//是拷贝传递, 需要引用传递 c(ref) 函数
```

泛型算法命名规范：传递谓词重载形式, `_if` 版本将 `val` 换为谓词, `_copy` 版本

作用在链表上泛型算法行为可能不同


## 迭代器

特殊迭代器：

* 插入迭代器 `back_inserter` `front_inserter` `inserter`（接受第二个迭代器参数, 插入到给定位置前, + 等等操作无作用）

    ```cpp
    back_inserter(container&);  // (<iterator>)
    //返回一个与容器绑定的插入迭代器, 通过其赋值时会调用 push_back()
    ```

* 流迭代器 `istream_iterator`（一参数版本绑定流, 无参版本尾后迭代器, 需模板实例化, 懒惰求值）`ostream_iterator`（可选第二参数 在每次输出后输出 C 风格字符串, + 等操作无作用）

* 反向迭代器（`forward_list` 和流迭代器没有, `base()` 成员返回相邻位置正向迭代器）

* 移动迭代器

迭代器类别：

* 输入迭代器：必须支持 相等不等运算, 前置后置递增运算, 解引用（右值）, 箭头

* 输出迭代器：必须支持 前置后置递增运算, 解引用（左值）

* 前向迭代器

* 双向迭代器：还支持前置后置递减运算

* 随机访问迭代器：还支持 位置比较关系运算符, 和整数值加减运算, 两迭代器减法运算, 下标运算

不要保存 `end()` 返回的迭代器



## `C++11` lambda 表达式

`[capture list] (parameter list) -> return type { function body }`

必须包括捕获列表和函数体

如果包含除单一 return 以外的内容且未指定返回类型, 返回 void

不能拥有默认参数

当定义 lambda 时, 生成一个与之对应的新未命名类类型

捕获变量是在 lambda 创建时发生

隐式捕获：编译器自动推断 `[&]` 引用捕获  `[=]` 值捕获

可以混合使用隐式捕获和显式捕获, 隐式捕获在前, 显式捕获必须使用不同方式

可变 lambda：mutable 关键字, 值拷贝时改变被捕获变量的值

