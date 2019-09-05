# Python 笔记

<!-- TOC -->

1. [安装插件](#安装插件)
2. [字符串操作](#字符串操作)
3. [csv文件读写](#csv文件读写)
    1. [创建csv文件](#创建csv文件)
    2. [读写csv文件](#读写csv文件)
    3. [备注](#备注)
4. [Excel（xls/xlsx）文件读写](#excelxlsxlsx文件读写)
    1. [使用xlrd/xlwt](#使用xlrdxlwt)
    2. [使用openpyxl](#使用openpyxl)
5. [Pandas](#pandas)
    1. [Pandas使用](#pandas使用)
    2. [pandas读csv文件](#pandas读csv文件)
6. [Python命名规则](#python命名规则)
    1. [命名约定](#命名约定)
    2. [应避免的命名](#应避免的命名)

<!-- /TOC -->

## 安装插件

```cmd
pip install
psutil  电脑监控信息读取
matplotlib  绘图
pillow->PIL  图片处理
pyserial  串口
scipy  科学计算库
pymysql  MySQL数据库
django  django网站框架
pandas 数据分析工具

```

## 字符串操作

## csv文件读写

### 创建csv文件

- 利用csv包中的writer函数，如果文件不存在，会自动创建，需要注意的是，文件后缀一定要是.csv，这样才会创建csv文件

### 读写csv文件

1. 读取csv文件的两种写法

    ```py
    with open('filename.csv', 'w', newline='') as file:
    ```

    ```py
    file = open('filename.csv', 'rb')
    ```

2. 用numpy处理csv数据的方法
   1. 读取数据

    ```py
    file = open("filename.csv", "rb")
    # 读取csv文件，以逗号为间隔，跳过第一行
    data = np.loadtxt(file, delimiter=",", skiprows=1)
    a = data[行起始:终止, 列起始:终止]
    ```

### 备注

- w：以写方式打开
- a：以追加模式打开 (从 EOF 开始, 必要时创建新文件)
- r+：以读写模式打开
- w+：以读写模式打开 (参见 w )
- a+：以读写模式打开 (参见 a )
- rb：以二进制读模式打开
- wb：以二进制写模式打开 (参见 w )
- ab：以二进制追加模式打开 (参见 a )
- rb+：以二进制读写模式打开 (参见 r+ )
- wb+：以二进制读写模式打开 (参见 w+ )
- ab+：以二进制读写模式打开 (参见 a+ )

## Excel（xls/xlsx）文件读写

### 使用xlrd/xlwt

1. 安装库文件

    ```cmd
    pip install xlrd
    pip install xlwt
    ```

2. 读取文件

    ```py
    import xlrd

    # 打开文件
    data = xlrd.open_workbook('filename.xlsx')
    # 获取第一个工作表
    table = data.sheets()[0]
    # 行列数
    rows = table.nrows
    cols = table.ncols
    # 行列值
    table.row_values(i)
    table.row_values(i)[0]
    table.col_values(i)
    table.col_values(i)[0]
    # 单元格
    table.cell(x,y).value
    ```

3. 日期处理

    ```py
    import xlrd
    from xlrd import xldate_as_datetime
    from xlrd import xldate_as_tuple

    xldate_as_datetime(table.row_values(i)[0], 0)  # 2019-06-01 00:00:00
    *xldate_as_tuple(table.row_values(i + 1)[0], 0)  # 2019 6 1 0 0 0
    ```

- 参考[Python操作excel的几种方式--xlrd、xlwt、openpyxl](http://wenqiang-china.github.io/2016/05/13/python-opetating-excel/)
- 参考[python xlrd模块处理excel日期变成浮点型的解决方法](https://my.oschina.net/zhangyangyang/blog/737072)
- 参考[用python读写excel（xlrd、xlwt）](https://www.cnblogs.com/MrLJC/p/3715783.html)

### 使用openpyxl

1. 安装库文件

    ```cmd
    pip install openpyxl
    ```

2. 读取文件

    ```py
    import openpyxl
    # 打开文件
    wb = openpyxl.load_workbook("filename.xlsx")
    # 以只读方式打开
    wb = openpyxl.load_workbook("st_data/官甲红.xlsx",read_only=True)

    # 读取sheet页
    sheet = wb['sheetname']
    # or
    sheet = wb.worksheets[0]

    # 行列数
    sheet.max_column
    sheet.max_row
    # 行列值
    sheet.cell(x,y).value
    ```

- 参考[Python 玩转 Excel](https://mp.weixin.qq.com/s?__biz=MjM5NjMyMjUzNg==&mid=2448130701&idx=1&sn=10919f10f4006a18579d6bbc13a3f15c&chksm=b2f42f0a8583a61c9421711b7a542f2a1c8cfe114ace3ea1ba8cefc26bdde8eb36755a7404ae&scene=0#rd)

## Pandas

### Pandas使用

1. pandas数据结构
   | 维数 | 名称      | 描述                                                           |
   | ---- | --------- | -------------------------------------------------------------- |
   | 1    | Series    | 可以看作有标签的一维数组，是scalars的集合，也是DataFrame的元素 |
   | 2    | DataFrame | 一般是二维标签，尺寸可变的表格结构，具有潜在的异质型列         |
2. 对象创建

    ```py
    In [5]: dates = pd.date_range('20130101', periods=6)

    In [6]: dates
    Out[6]:
    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                '2013-01-05', '2013-01-06'],
                dtype='datetime64[ns]', freq='D')

    In [7]: df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list('ABCD'))

    In [8]: df
    Out[8]:
                    A         B         C         D
    2013-01-01  0.469112 -0.282863 -1.509059 -1.135632
    2013-01-02  1.212112 -0.173215  0.119209 -1.044236
    2013-01-03 -0.861849 -2.104569 -0.494929  1.071804
    2013-01-04  0.721555 -0.706771 -1.039575  0.271860
    2013-01-05 -0.424972  0.567020  0.276232 -1.087401
    2013-01-06 -0.673690  0.113648 -1.478427  0.524988

    ```

3. 查看数据

    ```py
    df.head()  # 顶部数据，个数可选，默认5行
    df.tail()  # 尾部数据，个数可选
    df.index  # 显示索引、列和底层numpy数据

    df.describe()  # 显示数据的快速统计摘要
    df.T  # 转置数据
    df.sort_index(axis=1, ascending=False)  # 按轴排序
    df.sort_values(by='B')  # 按值排序
    ```

4. 选择数据

    ```py
    # 获取
    df['A']  # 获取A列数据
    df.A  # 同上
    df['20130102':'20130104']  # 通过[]选择，对行切片

    # 按位置索引
    df.iloc[3]  # 显示第四行数据
    df.iloc[0:3, 1:]  # 类似numpy
    df.iloc[[1, 2, 4], [0, 2]]  # 类似numpy

    # 布尔索引
    df[df.A > 0]
    ```

### pandas读csv文件

1. 打开文件

    ```py
    # header:告诉pandas那些是数据的列名，没有则设为None
    # encoding='gbk'防止出现乱码
    df = pd.read_csv('filename.csv', header=0, encoding='gbk')
    ```

## Python命名规则

### 命名约定

1. 所谓”内部(Internal)”表示仅模块内可用, 或者, 在类内是保护或私有的.
2. 用单下划线(_)开头表示模块变量或函数是protected的(使用from module import *时不会包含).
3. 用双下划线(__)开头的实例变量或方法表示类内私有.
4. 将相关的类和顶级函数放在同一个模块里. 不像Java, 没必要限制一个类一个模块.
5. 对类名使用大写字母开头的单词(如CapWords, 即Pascal风格), 但是模块名应该用小写加下划线的方式(如lower_with_under.py). 尽管已经有很多现存的模块使用类似于CapWords.py这样的命名, 但现在已经不鼓励这样做, 因为如果模块名碰巧和类名一致, 这会让人困扰.

### 应避免的命名

1. 单字符名称, 除了计数器和迭代器.
2. 包/模块名中的连字符(-)
3. 双下划线开头并结尾的名称(Python保留, 例如__init__)
