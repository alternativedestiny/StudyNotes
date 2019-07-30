# c++学习笔记

## 哈希表

1. 优点：编码容易，存储查找消耗的时间大大降低；缺点：内存消耗多。


## 获取长度的几种方法

```c++
#include<iostream>
#include<string>

using namespace std;

xx.size()
xx.length()
sizeof(xx)  // 运算符，返回所占空间的字节数
strlen(xx)  // 函数，返回字符数组或字符串所占的字节数

```

[参考链接](https://blog.csdn.net/z_qifa/article/details/77744482)


## string操作

```c++
#include <string>
string s1 = "put your string here";

// 截取
s1.substr(int a, int b) // 起始位a，长度b
s1.substr(int a)  // 截取第a个之后的字符串

// 插入
s1.insert(int num, string s)  // 在num位置插入s

// 擦除
s1.erase(int a, int b)  // 删除a之后的b个字符

// 添加
s1.append(string s)  // 追加字符串

// 替换
s1.replace(int num1, int num2, string s)  // 用s替换num1后面的num2-1个字符
s1.replace(int num1, int num2, string s, int num3, int num4)  // 用s的第num3后面的num4-1个字符替换num1后面的num2-1个字符

```

[参考链接](https://blog.csdn.net/tengfei461807914/article/details/52203202)

## map操作

- 有点类似python3的字典

```c++
// 头文件
#include<map>

// 创建
map<string,int> MapName = {
    {"a", 1},
    {"b", 2},
    {"c", 3}
};

// 插入
//查询
MapName.at();  // 返回对应值

// 查找
MapName.find();  // 返回的是被查找元素的位置，没有则返回map.end()
MapName.count();  // 返回的是被查找元素的个数。如果有，返回1；否则，返回0。注意，map中不存在相同元素，所以返回值只能是1或0。

```

[参考链接](https://blog.csdn.net/shuzfan/article/details/53115922)

## 备注

