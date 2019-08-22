# C++基于Linux

## 库的使用

### 库分类

1. 静态库：静态库的代码在编译过程中已经被载入可执行程序，因此体积较大
2. 动态库（共享库）：代码不会连接到目标文件之中，只有当动态库可访问时，应用程序才能正确执行动态库函数。执行动态库的方式有隐式调用和显式调用
   1. 隐式调用：也称共享库的静态加载，动态库在应用开始执行时会自动载入内存，进程结束时又自动卸载。隐式调用的编译方式与静态库一致
   2. 显式调用：也称共享库的动态加载，编译时可以不显式的提供原动态库文件及名称，但是必须遵循dlopen等函数的规则实现调用

### 静态库

1. 静态库生成：设计源码->编译`.o`文件->链接静态库，命名规则`libxxx.a`
2. 静态库的应用模型
   1. 调用库函数代码
   2. 编译链接选项

     ```shell
     # cc -O -o main.c ./libxxx.a
     ```

3. 执行目标程序`# ./main`

### 动态库

1. 动态库生成：
   1. 设计源码（exp：d1.c & d2.c）
   2. Linux和其它使用gcc编译器的Unix

     ```c++
     gcc -fpic -c d1.c d2.c /*编译.o为扩展名的中间目标文件*/
     gcc -shared -o d1.so d1.o /*创建动态库文件d1.so*/
     gcc -shared -o d2.so d2.o /*创建动态库文件d2.so*/
     ```

     或者可以一步到位

     ```c++
     gcc -O -fpic -shared -o d1.so d1.c/*创建动态库文件d1.so*/
     gcc -O -fpic -shared -o d2.so d2.c/*创建动态库文件d2.so*/
     ```

2. 动态库的隐式调用
   1. 调用库函数代码（main程序 main.c）
   2. 编译链接选项

      ```cmd
      # cp d1.so dll.so
      # cc -O -o main main.c ./dll.so
      # ./main  /*运行程序*/
      ```

   3. 动态库查找：动态库文件变更位置后程序无法正常运行，解决方法：带路径编译或更改环境变量
   4. 动态库更换：动态链接库取代静态库的好处之一是随时升级库的内容

      ```cmd
      # cp d2.so dll.so
      # ./main
      ```

3. 动态库的显式调用
   1. 函数族：显式调用动态库，编译时无需库文件，执行时动态库可存储于人艺文志，库里共享对象必须先申请后使用，不同版本的动态库，只要其共享对象接口相同，就可以直接动态加载。
      1. 打开动态库

          ```c
          #include <dlfcn.h>
          void *dlopen(const char *pathname, int mode);     //加载动态库
          ```

          - pathname：带路径的动态库名
          - mode：动态库加载方式
            - RTLD_LAZY：动态库的对象符号在被调用时解析
            - RTLD_NOW：动态库对象的所有符号在函数dlopen返回前被解析

      2. 获取动态库对象地址

          ```c
          #include <dlfcn.h>
          void *dlsym(const char *handle, const char *name);    //dlsym在动态库中搜索与字符串name同名的对象
          ```

          - handle：由函数dlopen返回成功加载动态库的句柄
          - name：待使用对象的名称（动态库中包含的函数名或变量名）
      3. 错误检查

          ```c
          #include <dlfcn.h>
          char *dlerror(void);  //获取显示动态库操作中的错误信息
          ```

      4. 关闭动态库

          ```c
          #include <dlfcn.h>
          void *dlclose(char *handle);  //动态库使用完必须关闭
          ```

   2. 应用模型：打开动态库->获取对象地址->执行动态对象（可回到上一步）->关闭动态库

### 小结

- 三种库调用对比

     | 对比项         | 静态库     | 隐式调用   | 显式调用 |
     | -------------- | ---------- | ---------- | -------- |
     | 编译参数       | 传递编译器 | 传递编译器 | 不需要   |
     | 链接到目标文件 | 是         | 否         | 否       |
     | 库存储位置     | 不需要     | 特定位置   | 任意位置 |
     | 载入时间       | 进程启动   | 进程启动   | 任意时刻 |

## 标准文件编程库

### 文件的创建、打开、关闭和删除

- filename：打开文件的名称（带路径）
- type：打开文件的方式，由权限和类型两部分组成
- stream：已经打开的文件指针

1. fopen函数：打开或创建一个文本

    ```c
    fopen(const char *filename, const char *type)
    ```

    | 方式 | 描述                                                                 |
    | ---- | -------------------------------------------------------------------- |
    | r    | 以只读方式打开，不能更改内容，若文件不存在则报错                     |
    | w    | 以只写方式打开，若文件已存在，清空原文件内容，否则创建新文件         |
    | a    | 以追加方式打开，若文件已存在，则在文件末尾增加内容，否则创建新文件   |
    | r+   | 以读写方式打开，若文件不存在则报错                                   |
    | w+   | 以读写方式打开，若文件已存在，清空原文件内容，否则创建新文件         |
    | a+   | 以读取和追加模式打开文件，全文读取，文末追加，若文件不存在创建新文件 |
    | b    | 以二进制模式打开或创建文件，否则以文本文件打开或创建文件             |

2. freopen函数：实现文件流的替换。它首先关闭一个文件流，再创建新的文件流

    ```c
    FILE *freopen(const char *filename, const char *type, FILE *stream)
    ```

    | FILE标识符 | 文件         |
    | ---------- | ------------ |
    | stdout     | 标准输出     |
    | stdin      | 标准输入     |
    | stderr     | 标准错误输出 |

3. fclose函数

    ```c
    // 关闭文件流，成功时返回0，否则返回EOF
    int fclose(FILE *stream);
    ```

4. remove函数

    ```c
    // 删除指定文件或目录
    int remove(const char *filename);
    ```

5. rename函数

    ```c
    // 重命名
    int rename(const char *oldname, const char *newname);
    ```

6. 二进制文件与文本文件
   1. 文本文件又称为ASCII码文件，可以用vi等文本编辑器编辑其中任意字符，也可以直接操作以空额、制表符或换行符分割的单词和文本。C语言源代码是典型的文本文件。
   2. 二进制文件中可以包含任意字符，没有固定格式，文本编辑器无法正常阅读，所有对文件的解析都由应用程序完成。C语言编译后的可执行文件就是二进制文件。

### 文件的无格式读写

1. 字符读写：每次之操作一个字符
   1. 字符输入函数族

        ```c
        #include<stdio.h>
        // getc以unsigned char类型读取文件输入流stream中的一个字符，并将该无符号字符转化为整型后返回，同时移动文件指针到下一个字符处
        int getc(FILE *stream);
        // getchar实际上是关于getc的宏定义“getc(stdin)”
        int getchar(void);
        // fgetc功能类似于getc，但是执行速度远低于getc
        int fgetc(FILE *stream);

        // 错误时都返回EOF，EOF一般定义为int型-1
        ```

   2. 字符输出函数族

        ```c
        #include<stdio.h>
        // 函数putc先将int型参数c自动转换为unsigned char类型，然后写入文件流stream中，同时移动文件指针到下一个字符处
        int putc(int c, FILE *stream);
        int putchar(int c);
        int fputc(int c, FILE *stream);
        ```

2. 行读写
   1. 行输入函数族

        ```c
        #include<stdio.h>
        //
        char *gets(char *s);
        char *fgets(char *s, int n, FILE *stream)

        ```

## linux命令

1. grep 文件搜索
   1. 常用命令
      1. grep：在没有参数的情况下，只输出符合RE（Regular Expression）字符。
      2. egrep：等同于grep -E，和grep最大的区别就是表现在转义符上比如grep 做次数匹配时\{n,m\}egrep则不需要直接{n，m}。egrep方便，简介。
      3. fgrep：等同于grep -f，但是不能使用正则表达式。所有的字符匹配功能均已消失。
   2. 参数说明 `grep [OPTIONS] PATTERN(模式) [file]`
