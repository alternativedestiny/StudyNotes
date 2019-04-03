# libsvm安装python

1. 下载安装包，根据自己的系统和Python版本选择[https://www.lfd.uci.edu/~gohlke/pythonlibs/#libsvm]
2. 安装包
    ```cmd
    pip install 安装包名
    ```
3. 测试
    ```python
    from svmutil import *
    from svm import *
    y, x = [1, -1], [{1: 1, 2: 1}, {1: -1, 2: -1}]
    prob = svm_problem(y, x)
    param = svm_parameter('-t 0 -c 4 -b 1')
    model = svm_train(prob, param)
    yt = [1]
    xt = [{1: 1, 2: 1}]
    p_label, p_acc, p_val = svm_predict(yt, xt, model)
    print(p_label)
    ```
4. 能正常运行不报错就是安装成功
