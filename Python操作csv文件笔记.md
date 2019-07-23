# Python操作csv文件笔记

## 创建csv文件
- 利用csv包中的writer函数，如果文件不存在，会自动创建，需要注意的是，文件后缀一定要是.csv，这样才会创建csv文件

## 读写csv文件
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
    data = np.loadtxt(file, delimiter=",", skiprows=1) # 读取csv文件，以逗号为间隔，跳过第一行
    a = data[行起始:终止, 列起始:终止]
    ```


## 备注
- w：以写方式打开， 
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
