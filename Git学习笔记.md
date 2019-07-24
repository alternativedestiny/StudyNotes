# Git 学习笔记

## 前言

Git分区：工作区—暂存区—Git仓库

## 环境

- Windows10

## 初始化

- git config --global user.name "xx"
- git config --global user.email "xxxx"

## 基础语法

1. 新文件初始化

    ```git
    git init
    ```

2. 把工作目录的文件添加到暂存区域

    ```git
    git add xxx
    ```

3. 把暂存区域提交到Git仓库

    ```git
    git commit -m "声明"
    ```

    合并添加和提交

    ```git
    git commit -am "声明 "
    ```

4. 把Git仓库文件还原到暂存区域

    ```git
    git reset
    ```

    --mixed（默认）：快照回滚到暂存区域
    --soft选项：只移动head指向
    --hard选项：不仅移动head，还把暂存区文件还原到工作目录

5. 查询Git状态

    ```git
    git status
    ```

6. 查看记录

    ```git
    git log
    ```

7. 文件比较

    ```git
    git diff
    ```

8. 更正最近一次提交

    ```git
    git commit --amend
    ```

    如果需要提交新的说明

    ```git
    git commit --amend -m
    ```

9. 文件被删后，把暂存区文件还原到工作目录

    ```git
    git checkout -- xxx
    ```

    注意--前后各有一个空格
10. 删除文件

    ```git
    git rm xxx
    ```

    然后执行

    ```git
    git reset --soft HEAD~
    ```

11. 重命名文件

    ```git
    git mv name1 name2
    ```

## 进阶

1. 创建分支

    ```git
    git branch 分支名
    ```

2. 切换分支

    ```git
    git checkout 分支名
    ```

3. 显示分支

    ```git
    git log --decorate --all --graph --oneline
    ```

4. 合并分支

    ```git
    git merge 分支名
    ```

    将选定分支合并到HEAD所在分支
5. 删除分支

    ```git
    git branch -d 分支名
    ```

## 老瓶装新酒（新设备在已有项目的基础上继续更新）

1. 克隆项目到本地，在目标文件下

    ```git
    git clone xxx.git
    ```

2. 在git配置好的情况下直接使用即可
