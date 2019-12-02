# Python 笔记

<!-- TOC -->

1. [Python 环境](#python-环境)
    1. [更换国内镜像](#更换国内镜像)
    2. [Python 创建虚拟环境](#python-创建虚拟环境)
        1. [Windows 平台](#windows-平台)
        2. [linux 平台](#linux-平台)
2. [数据处理](#数据处理)
    1. [数字处理](#数字处理)
    2. [字符串处理](#字符串处理)
3. [OS](#os)
    1. [文件处理](#文件处理)
4. [文件读写](#文件读写)
    1. [csv 文件](#csv-文件)
    2. [Excel(xls/xlsx) 文件读写](#excelxlsxlsx-文件读写)
5. [Numpy](#numpy)
    1. [ndarray](#ndarray)
6. [Pandas](#pandas)
    1. [Pandas 数据处理](#pandas-数据处理)
    2. [pandas 读写文件](#pandas-读写文件)
    3. [pandas 其他](#pandas-其他)
    4. [pandas 错误处理](#pandas-错误处理)
7. [Matplotlib 绘图](#matplotlib-绘图)
    1. [绘图种类](#绘图种类)
    2. [坐标轴处理](#坐标轴处理)
    3. [图中点、文字处理](#图中点文字处理)
    4. [图片输出设置](#图片输出设置)
8. [Seaborn 数据可视化](#seaborn-数据可视化)
9. [python 多线程](#python-多线程)
10. [SQL 使用 (MySQL)](#sql-使用-mysql)
11. [Python 命名规则](#python-命名规则)
    1. [命名约定](#命名约定)
    2. [应避免的命名](#应避免的命名)

<!-- /TOC -->

## Python 环境

### 更换国内镜像

1. 管理员模式下

    ```cmd
    pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
    ```

2. 安装库

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
    virtualenv 虚拟环境

    ```

3. 升级库

```cmd
pip list --outdate  // 显示可升级库
pip install --upgrade xxx  // 升级库
```

### Python 创建虚拟环境

#### Windows 平台

1. 安装virtualenv库
2. 在目标文件夹下进入cmd
3. `virtualenv venv`创建虚拟环境venv
4. 在`venv/Scripts`下执行`activate`开启虚拟环境
5. `deactivate`退出虚拟环境

#### linux 平台

1. 安装virtualenv库
2. 创建虚拟环境
3. 添加环境变量

## 数据处理

### 数字处理

1. 保留4位小数位

```python
# 百分号
print('%.4' % num)

# round
num = round(num, 4)

```

### 字符串处理

```python
# 1. 类型转换:
str2 = str(str1)

# 2. 字符串拼接：
str3 = str1 + str2

# 3. 字符串截取：
str4 = str1[m:n]  # 符号表示从后算起

# 4. 创建全0数组
import numpy as np
list1 = np.zeros(25, dtype=int)

# 5. 字符串转代码
str1 = "print('hello')"
eval(str1)  # hello

# 6. 字符串替换
str1.replace('a', 'b')

# 7.查询字符位置
str1.find('a')  # 返回a所在位置

```

## OS

### 文件处理

```python
import os

# 获取文件列表
sources_path = "./substation"  # 路径
file_name = os.listdir(sources_path)  # 所有文件名

# 创建文件夹
path = 'abc/'
# 检测文件夹是否存在，不存在就创建该文件夹
if not os.path.exists(path):
    print('folder not exist')
    os.makedirs(path)
else:
    print('folder exist')
```

## 文件读写

### csv 文件

1. 读取csv文件的两种写法

    ```python
    with open('filename.csv', 'w', newline='') as file:
    ```

    ```python
    file = open('filename.csv', 'rb')
    ```

2. 用numpy处理csv数据的方法
   1. 读取数据

    ```python
    file = open("filename.csv", "rb")
    # 读取csv文件，以逗号为间隔，跳过第一行
    data = np.loadtxt(file, delimiter=",", skiprows=1)
    a = data[行起始:终止, 列起始:终止]
    ```

3. 用pandas读写csv文件

4. 备注

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

### Excel(xls/xlsx) 文件读写

1. 使用 xlrd/xlwt

   1. 安装库文件

       ```cmd
       pip install xlrd
       pip install xlwt
       ```

   2. 读取文件

       ```python
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

       ```python
       import xlrd
       from xlrd import xldate_as_datetime
       from xlrd import xldate_as_tuple

       xldate_as_datetime(table.row_values(i)[0], 0)  # 2019-06-01 00:00:00
       *xldate_as_tuple(table.row_values(i + 1)[0], 0)  # 2019 6 1 0 0 0
       ```

   - 参考[Python操作excel的几种方式--xlrd、xlwt、openpyxl](http://wenqiang-china.github.io/2016/05/13/python-opetating-excel/)
   - 参考[python xlrd模块处理excel日期变成浮点型的解决方法](https://my.oschina.net/zhangyangyang/blog/737072)
   - 参考[用python读写excel（xlrd、xlwt）](https://www.cnblogs.com/MrLJC/p/3715783.html)

2. 使用 openpyxl

   1. 安装库文件

       ```cmd
       pip install openpyxl
       ```

   2. 读取文件

       ```python
       import openpyxl
       # 打开文件
       wb = openpyxl.load_workbook("filename.xlsx")
       # 以只读方式打开
       wb = openpyxl.load_workbook("st_data/官甲红.xlsx", read_only=True)

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

## Numpy

### ndarray

1. [增删改查](https://blog.csdn.net/Tyro_java/article/details/81052638)

    ```python
    import numpy as np
    # 增
    data = np.append(data, a)  # 将a添加到data中
    # 删
    data = np.delete(data, [0])
    ```

## Pandas

### Pandas 数据处理

1. pandas数据结构

   | 维数 | 名称      | 描述                                                           |
   | ---- | --------- | -------------------------------------------------------------- |
   | 1    | Series    | 可以看作有标签的一维数组，是scalars的集合，也是DataFrame的元素 |
   | 2    | DataFrame | 一般是二维标签，尺寸可变的表格结构，具有潜在的异质型列         |

   1. DataFrame信息

        ```python
        df.info()  # 信息
        len(df)  # 行数
        len(df.columns)  # 列数

        # 设置index标题
        df3.index.name = 'index_name'

        # 列重命名
        df.columns = ['new_col1', 'new_col2']
        ```

   2. Series信息

        ```python
        len(s)  # 长度
        ```

2. 数据格式转换：数据格式不对可能会造成多种问题，比如计算、绘图(这些操作均不会改变原数据)
   1. astype 转换成其他类型

        ```python
        # 由其他类型转换成float
        a = df.iloc[:, 0].astype('float')
        ```

   2. to_numeric 转换成数字

        ```python
        s = pd.Series(['1.0', '2', -3])
        s = pd.to_numeric(s)
        ```

   3. to_datetime 转换成日期

        ```python
        tm = pd.to_datetime(df.iloc[:, 0])
        ```

   4. to_timedelta 相对日期
   5. tolist() Series转list(DataFram)

        ```python
        list1 = Series.tolist()
        ```

3. 检测数据是否有空值(Nan)

   ```python
   # 含空数据true，不含空数据false
   df.isnull().any()
   # 判断数据是否为nan，不能用==
   if df[] is np.nan
   ```

4. 创建DataFrame

    ```python
    # 创建DataFrame
    title = ['a', 'b', 'c']  # 列名
    index = [1, 2, 3, 4]  # 行名
    df = pd.DataFrame(index=index, columns=title)

    # 创建IndexName
    df.index.name = 'num'

    # 增加一行数据
    df.loc['0'] = [1, 2, 3]
    # 增加一列数据
    df['d'] = [1, 2, 3]
    ```

5. 查看数据

    ```python
    df.head()  # 顶部数据，个数可选，默认5行
    df.tail()  # 尾部数据，个数可选
    df.index  # 显示索引、列和底层numpy数据
    df.info()  # 显示数据的类型

    df.describe()  # 显示数据的快速统计摘要
    df.T  # 转置数据
    df.sort_index(axis=1, ascending=False)  # 按轴排序
    df.sort_values(by='B')  # 按值排序

   ```

6. 选择、查询数据(数据截取)

    ```python
    # 获取
    df['A']  # 获取A列数据
    df.A  # 同上
    df['20130102':'20130104']  # 通过[]选择，对行切片

    # 按位置索引
    df.iloc[3]  # 显示第四行数据
    df.iloc[0:3, 1:]  # 类似numpy
    df.iloc[[1, 2, 4], [0, 2]]  # 类似numpy

    # loc通过标签访问，iloc通过行列号访问
    # 获取a，b列的数据
    new_df = df.loc[:, ['a', 'b']]  # DataFrame
    # 获取第1列的数
    new_df = df.iloc[:, 1]  # Series
    # 还可以直接访问列标签
    new_df = df['a'][0:3000]  # Series

    # 布尔索引
    df[df.A > 0]
    new_df = df[df['tm1'] >= '2018-01-01 00:00:00']
    # 选择并选取指定行
    df.loc[df['tm1'] >= '2019-01-01 00:00:00', ['tm1', 'hv']]
    df[df.tm1 >= '2019-01-01 00:00:00']['tm1', 'hv']
    # 多条件筛选
    df[(df['a'] >= 10) & (df['b'] >= 10)]  # 与
    df[(df.a >= 10) | (df.b >= 10)]  # 或
    ```

7. 生成数据
   1. date_range：生成等间隔时间序列

        ```python
        pd.date_range(start, end, pediods)
        ```

8. 数据排序
   1. Series排序

        ```python
        Series.sort_values()  # 升序排列
        ```

   2. DataFrame排序

        ```python
        DataFrame.sort_values(sub[i], ascending=False)  # 降序排列
        ```

9. DataFrame合并(merge, concat)

    ```python
    # 数据左右合并，合并依据为key
    # how = inner, outer, left, right 默认inner
    # 需要注意，有时合并数据会造成意外的重复
    df3 = pd.merge(df1, df2, how='left', on='key1')  # 单个key
    df3 = pd.merge(df1, df2, how='left', on=['key1','key2'])  # 多key

    # 数据拼接，列不变，行叠加
    df3 = concat([df1, df2])
    ```

### pandas 读写文件

1. python文件

    ```python
    # header:告诉pandas那些是数据的列名，没有则设为None
    # encoding='gbk'防止出现乱码

    # 读取csv文件，表头第0行，文件gbk编码，指定字段的数据类型
    df = pd.read_csv('filename.csv', header=0, encoding='gbk', dtype={'id': int, 'name': string})

    # 读取excel文件，表头第0行，表sheet1，选择第0，1列数据
    df1 = pd.read_excel('filename.xlsx', header=0,sheet_name='Sheet1', usecols=[0, 1])

    # 读取不同的数据类型dtype
    ```

2. 读取设置
   | 关键字                | 功能                          |
   | --------------------- | ----------------------------- |
   | na_values=[5]         | 5和5.0会被认为是NaN           |
   | na_valuede=["Na","0"] | Na和0会被认为是NaN            |
   | true_values=["yes"]   | yes被认为True                 |
   | false_value=["no"]    | no被认为False                 |
   | Skipping line         | 跳过某些行                    |
   | MultiIndex            | 支持双列目录                  |
   | sep=':'               | 支持':'等符号作为分隔符的数据 |
   | chunksize=4           | 每4行数据为一组               |

3. 输出CSV文件

    ```python
    # 将df存储为csv，index表示是否显示行名
    df.to_csv('name.csv', index=False, sep=',')  # 推荐
    # 会给数据添加引号
    df.to_csv('name.csv', index=False, delimiter=',')  # 不要用
    ```

### pandas 其他

1. [pandas类SQL查询](https://juejin.im/post/5b5e5b2ee51d4517df1510c7)

### pandas 错误处理

1. [`read_csv mixed types`问题](https://www.jianshu.com/p/a70554726f26)
2. `cannot convert the series to <class 'float'>`问题
   1. 原因：可能是某处变量调用忘了加限定，比如a[i]写成了a

## Matplotlib 绘图

### 绘图种类

1. scatter 散点图
   1. 带颜色区分的散点图
2. plot 折线图
   1. 一个图里多条折线

        ```python
        plt.plot(x1, y1, x2, y2)
        ```

3. bar 柱状图

### 坐标轴处理

1. 坐标轴反向

    ```py
    ax.invert_xaxis()  # x坐标轴反向
    ```

2. 设置坐标值

    ```python
    # 按照需求设置坐标，坐标一定要有对应的数据
    x_axis = ['2018-09-01', '2018-10-01', '2018-11-01', '2018-12-01', '2018-12-31']
    plt.xticks(x_axis, rotation=15)  # 刻度倾斜
    # 还可以对坐标重命名
    x_axis = ['2018-01-01 00:01:00', '2018-01-02 00:00:00', '2018-01-03 00:00:00']
    plt.xticks(x_axis, ('a', 'b', 'c'), rotation=-15)  # 将横坐标值重命名为a,b,c
    ```

    ```python
    # 按照等间隔数值设置坐标
    plt.xticks(np.arange(0, 25, 4))  # 范围0-25，分度值4
    ```

3. 设置坐标限位

    ```python
    # 数值型
    plt.xlim(0, 24)
    plt.ylim(0, 10)

    # 日期型
    plt.xlim(datetime.strptime('2019-05-12', '%Y-%m-%d'), datetime.strptime('2019-05-15', '%Y-%m-%d'))
    ```

4. 设置轴标签

    ```python
    plt.xlabel("x")
    plt.ylabel("y")
    ```

5. 坐标轴坐标倾斜

    ```python
    plt.xticks(x_axis, rotation=15)  # 刻度倾斜
    ```

### 图中点、文字处理

1. 中文编码问题

    ```python
    plt.rcParams['font.sans-serif'] = ['SimHei']  # 解决plt中文乱码
    plt.rcParams['axes.unicode_minus'] = False  # 用来正常显示负号
    ```

### 图片输出设置

1. 图片大小设置

    ```python
    plt.rcParams['figure.figsize'] = (12, 8)
    ```

2. 图片保存

    ```python
    plt.savefig("Picture.png")  # 不支持jpg
    ```

## Seaborn 数据可视化

## python 多线程

1. 多线程：适用于IO密集型，不适用于CPU密集型。
2. 代码

    ```python
    import threading

    # 创建多线程函数：target目标函数（线程内执行的函数），args目标函数参数
    th = threading.Thread(target=check, args=(a, b, c))
    # 开线程
    th.start()
    ```

## SQL 使用 (MySQL)

1. 读取数据

    ```python
    import pymysql

    # host, user, password, database
    database = pymysql.connect("localhost", "root", "123456", "test1")

    # 创建游标
    cursor = database.cursor()

    # sql语句：从table中抽取10组a，b，按a的降序排列
    sql = "select a,b from table order by a desc limit 10"

    # 执行sql语句
    cursor.execute(sql)

    # 获取数据
    data = cursor.fetchone()  # 获取单条数据
    data = cursor.fetchall()  # 获取全部数据

    # 关闭数据库连接
    database.close()
    ```

2. 写入数据

    ```python
    sql = "insert into table(col1, col2) values (%s, %s) % (num1, num2)"
    cursor.excute(sql)

    # 提交到数据库执行，多数据插入只用执行一次commit
    database.commit()
    ```

3. 更多内容查看MySQL笔记

## Python 命名规则

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
