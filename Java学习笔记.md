# Java笔记

<!-- TOC -->

1. [基本语法](#基本语法)
    1. [字符&字符串](#字符字符串)
        1. [字符Character](#字符character)
        2. [字符串](#字符串)
    2. [数组](#数组)

<!-- /TOC -->

## 基本语法

### 字符&字符串

#### 字符Character

1. 创建字符&字符数组

    ```java
    // 字符
    char ch = 'a';
    System.out.println(ch);  // a
    // 字符数组
    char[] ch = {'a', 'b', 'c'};
    System.out.println(ch);  // abc
    ```

2. 方法

    方法|功能
    --|--
    isLetter()|是否是一个字母
    isDigit()|是否是一个数字
    idWhitespace()|是否是一个空白字符
    isUpperCase()|是否是大写字母
    isLowerCase()|是否是小写字母
    toUpperCase()|转换成大写字母
    toLowerCase()|转换成小写字母
    toString()|转换成字符串，长度为1

#### 字符串

1. 创建字符串

    ```java
    String he = "hello";
    System.out.println(s.length());  // 5
    ```

2. 方法

    ```java
    // 连接字符串
    string1.concat(string2)
    string1 + string2

    // 格式化字符串
    String s;
    s = String.format("abc %f %d", 3.14, 5);  // abc 3.140000 5
    ```

### 数组

1. 创建数组

    ```java
    // 声明数组
    dataType[] arrayRefVar = new dataType[arraySize];  // 方法1
    dataType[] arrayRefVar = {value0, value1, ..., valuek};  // 方法2

    // eg1
    int[] x = new int[5]
    x[0] = 0;
    x[1] = 1;
    ...
    x[4] = 4;

    // eg2
    int[] x = {1, 2, 3};

    ```

2. 遍历

    ```java
    // 基本循环
    int[] x = {1, 2, 3};
    for (int i = 0; i < x.length; i++){
        System.out.println(x[i]);
    }
    // for-each循环
    for (int value : x) {
        System.out.println(value);
    }
    ```
