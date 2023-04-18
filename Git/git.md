token：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

# 一、利用Git连接远程仓库步骤及常见问题

## 1.先创建一个文件夹，名字为远程仓库的名称

## 2.在该文件目录下打开Git Bash

## 3.输入git init,进行初始化

## 4.连接远程仓库（初次连接，下一次进入该文件夹就不用了）
输入下列命令

~~~bash
git remote add origin git@github.com:yourName/repositoryname.git
git remote add origin https://github.com/yourName/repositoryname.git
~~~


yourName是用户名，repositoryname是仓库名字

## 5.从远程仓库拉取文件
~~~bash
git pull origin "分支名"
~~~


## 6.查看工作目录状态

~~~bash
git status
~~~

## 7.添加文件，提交更改，添加备注信息

~~~bash
git add 文件名
git commit -m "备注信息"
~~~



> 注意：若第6步的信息中有以下情况：
> 1.Untraked Files
> 使用git add .解决该问题
> 2.Changes not staged for commit
> 使用 git commit -am "备注信息" 解决



## 8.将本地文件push到远程仓库
```bash
git push origin "分支名"
```

