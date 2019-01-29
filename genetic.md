# STL 泛型算法

谓词 predicate:可调用的表达式, 一元谓词/二元谓词

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

back_inserter(container&);  // (<iterator>)
//返回一个与容器绑定的插入迭代器, 通过其赋值时会调用 push_back()

copy(source_begin, source_end, dest);
//返回值是 dest.end

replace(begin, end, search_for, replace_as);
replace_copy(begin, end, dest_begin, search_for, replace_as);

sort(begin, end);
sort(begin, end, predicate);
stable_sort(...);
unique(begin, end); // 返回指向不重复范围末尾的迭代器

for_each(begin, end, predicate);
```

## `C++11` lambda 表达式

`[capture list] (parameter list) -> return type { function body }`

必须包括捕获列表和函数体

如果包含除单一 return 以外的内容且未指定返回类型, 返回 void

不能拥有默认参数

当定义 lambda 时, 生成一个与之对应的新未命名类类型
