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

int a[] = {1, 2, 3, 4}; // 数组
sizeof(a)/ sizeof(a[0]);

```

- [参考链接](https://blog.csdn.net/z_qifa/article/details/77744482)

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

- [参考链接](https://blog.csdn.net/tengfei461807914/article/details/52203202)

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

- [参考链接](https://blog.csdn.net/shuzfan/article/details/53115922)

## 类&对象

1. 类的定义

    ```c++
    class Box{
        // 除了public还可以定义成private或protect
        public:
            double length;
            double breadth;
            double height;
    }
    ```

2. 访问数据成员

    ```c++
    Box Box1;  // 声明Box1，类型为Box

    // 定义box1的长宽高
    Box1.length = 10.0;  
    Box1.breadth = 12.0;
    Box1.height = 9.0；

    // 访问变量
    double volume = Box1.length * Box1.bredth  * Box1.height;
    ```

3. 类的成员函数

    ```c++
    // 类内定义
    class Box(){
        public:
            double length;
            double breadth;
            double height;

            double getVolume(void){
                return length*breadth*height;
            }
    }

    // 类外定义
    class Box(){
        public:
            double length;
            double breadth;
            double height;
            // 成员函数声明
            double getVolume(void);
    }
    double Box::getVolume(void){
        return length * breadth * height;
    }

    // 访问函数
    Box Box1;
    double volume  = Box1.getVolume();
    ```

4. 类访问修饰符
   1. public公有成员：类的外部可以访问
   2. private私有成员：类的外部不可访问，不可查看，默认情况下，类的所有成员都是私有的。可以使用成员函数对数据进行初始化。
   3. protected保护成员：与私有成员类似，但是保护成员在派生类（子类）中可以访问。

5. 构造函数&析构函数
   1. 构造函数
      - 是一类特殊的成员函数，他会在每次创建类的新对象时执行
      - `构造函数的名称与类的名称是完全相同`的，并且不会返回任何类型，也不会返回 void
      - 构造函数可用于为某些成员变量设置初始值
      - 默认的构造函数没有任何参数，但如果需要，构造函数也可以带有参数

   2. 析构函数
        - 类的析构函数是类的一种特殊的成员函数，它会在每次删除所创建的对象时执行
        - 析构函数的名称与类的名称是完全相同的，只是在前面加了个波浪号（~）作为前缀，它不会返回任何值，也不能带有任何参数。析构函数有助于在跳出程序（比如关闭文件、释放内存等）前释放资源

    ```c++
    class Line
    {
        public:
            void setLength( double len );
            double getLength( void );
            Line();   // 这是构造函数声明
            ~Line();  // 这是析构函数声明
    };

    // 成员函数定义，包括构造函数
    Line::Line(void)
    {
        cout << "Object is being created" << endl;
    }
    Line::~Line(void)
    {
        cout << "Object is being deleted" << endl;
    }
    ```

## 链表

1. 单向链表：链表中最简单的一种是单向链表，它包含两个域，一个信息域和一个指针域。这个链接指向列表中的下一个节点，而最后一个节点则指向一个`空值`。
2. 双向链表：一种更复杂的链表是“双向链表”或“双面链表”。每个节点有两个连接：一个指向前一个节点，（当此“连接”为第一个“连接”时，指向空值或者空列表）；而另一个指向下一个节点，（当此“连接”为最后一个“连接”时，指向空值或者空列表）。
3. 优点：
   1. 使用链表结构可以克服数组链表需要预先知道数据大小的缺点，链表结构可以充分利用计算机内存空间，实现灵活的内存动态管理。
   2. 相比数组结构，对于元素的插入和删除操作来说，链表的效率要比数组高，因为每个节点都有链域存储指向下一个节点的指针，因此进行插入和删除的操作时不需要频繁的移动其他的元素，只需要修改对应位置附近节点的链域的值即可。
4. 缺点
   1. 查询链表只能通过指针顺序访问，效率相对低下，查询可能需要O(n)的时间复杂度。
   2. 因为链表的每个节点都含有链域，所占用的空间较多。
5. 链表操作

    ```c++
    #include <stdio.h>
    #include <iostream>

    using namespace std;

    // 创建链表
    typedef struct student {
        int score;  // 数据域
        struct student *next;  // 链域
    } LinkList;

    // 初始化链表，n为节点个数
    LinkList *creat(int n) {
        LinkList *head, *node, *end;  // 定义头节点，普通节点，尾节点
        head = (LinkList *) malloc(sizeof(LinkList));  // 分配地址
        end = head;  // 若是空链表则头尾节点一样
        printf("请输入 %d 个链表值: \n", n);
        for (int i = 0; i < n; i++) {
            node = (LinkList *) malloc(sizeof(LinkList));
            scanf("%d", &node->score);
            end->next = node;
            end = node;
        }
        end->next = NULL;  // 结束创建
        return head;
    }

    // 修改链表节点值，n为第n个值
    void change(LinkList *list, int n) {
        LinkList *t = list;
        int i = 0;
        n++;
        // 先查询
        while (i < n && t != NULL) {
            t = t->next;
            i++;
        }
        // 再修改
        if (t != NULL) {
            puts("输入要修改的值");
            scanf("%d", &t->score);
        } else {
            puts("节点不存在");
        }
    }

    // 删除节点
    void delet(LinkList *list, int n) {
        LinkList *t = list, *in;
        int i = 0;
        while (i < n && t != NULL) {
            in = t;
            t = t->next;
            i++;
        }
        if (t != NULL) {
            in->next = t->next;
            free(t);  // 放出被删除节点的空间
        } else {
            puts("节点不存在");
        }
    }

    // 插入链表节点
    void insert(LinkList *list, int n) {
        LinkList *t = list, *in;
        int i = 0;
        while (i < n && t != NULL) {
            t = t->next;
            i++;
        }
        if (t != NULL) {
            in = (LinkList *) malloc(sizeof(LinkList));
            puts("要插入的值");
            scanf("%d", &in->score);
            in->next = t->next;  // 填充in节点的指针域指向下一个节点
            t->next = in;  // t节点的指针域指向in
        } else {
            puts("节点不存在");
        }
    }

    // 输出链表
    void plot(LinkList *list) {
        LinkList *t = list;
        int i = 0;
        while (t->next != NULL) {
            t = t->next;
            printf("%d", t->score);
            i++;
        }
        printf("长度%d \n", i);
    }

    int main() {
        LinkList *li = creat(5);  // 创建5个长度的链表
        insert(li, 0);
        plot(li);
        change(li, 1);
        delet(li, 5);
        plot(li);

    }

    ```

- [链表操作](https://blog.csdn.net/Endeavor_G/article/details/80552680)

## 备注
