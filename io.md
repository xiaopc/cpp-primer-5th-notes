# I/O

## 缓冲刷新

退出，缓冲区满，`endl flush ends` 操纵符显式刷新，`unitbuf` 操纵符设置流内部状态（`cerr` 默认置位），读写关联流（`cin/cerr->cout`）

异常终止时输出缓冲区不会被刷新.


## string

string.size() 返回的是无符号整型（不与 int 一起用）.

string 相加时保证每个加号两侧至少有一个 string.（从左至右）

string.c_str() 返回的数组在 string 改变后可能失效.


## iostream

wcin wcout wcerr 是宽字符版对象.
