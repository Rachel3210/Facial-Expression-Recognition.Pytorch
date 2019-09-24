# Git

标签（空格分隔）： tools

---
[TOC]

#可以将操作分为两类，一类为从远程到本地的下拉操作，一类为从本地到远程的上传操作，第三方操作/本地操作，目前按照我学习路线记录过程中遇到的学的东西

##1.git常用命令
https://www.w3cschool.cn/git/git-cheat-sheet.html
![git常用命令][1]
##2.相关教程
###git菜鸟教程
http://www.runoob.com/git/git-create-repository.html
###其他教程
https://www.yiibai.com/git

https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000 

##2.ubuntu下pycharm 使用github/git
http://www.linuxdiyf.com/linux/25983.html 



##4.**怎么用git clone 远程的所有分支，以及分支间切换！！！！！**超级有用
https://www.jianshu.com/p/0fe715a7fbb3

##5.修改文件后，先commit保存到本地，在push提交到远程仓库（本地操作+上传操作）
```
1.git status 查看git是否有修改内容需要提交
2.git add 指向需要提交的内容文件
3.git commit 提交到本地库，只是本地改变了，github上还每没改变
4.git push origin master/或者要提交的本地分支的名字 提交到远程仓库 push之后，github上才有改变，
```
```
git add -A
它能stages所有文件，
而之前用的
git add .
只能stages新文件和被修改文件，没有被删除文件
```
![git分布式版本控制][2]

##6.删除git库中untracked files（未监控）的文件
在编译git库拉下来的代码时，往往会产生一些中间文件，这些文件我们根本不需要，尤其是在成产环节做预编译，检查代码提交是否能编译通过这种case时，我们往往需要编译完成后不管正确与否，还原现场，以方便下次sync代码时不受上一次的编译影响。
```
删除 untracked files
git clean -f

连 untracked 的目录也一起删掉
git clean -fd

连 gitignore 的untrack 文件/目录也一起删掉 （慎用，一般这个是用来删掉编译出来的 .o之类的文件用的）
git clean -xfd

在用上述 git clean 前，强烈建议加上 -n 参数来先看看会删掉哪些文件，防止重要文件被误删
git clean -nxfd
git clean -nf
git clean -nfd
```
原文：https://blog.csdn.net/RonnyJiang/article/details/53507306 

##7.git 退出 git log
经常输入 git log 后， 即使按ctrl+c (z) 都无法完全退出
要输入q 

##8.Git 里面的 origin 到底代表啥意思?
默认情况下的远端库的名字。
你可以用 git remote 进行相关操作。
远端库也可以用其他名字，用 origin 只是因为他是默认的。

Git 的origin和master分析
https://blog.csdn.net/abo8888882006/article/details/12375091 


##9.拉取远程库的更新-注意区别git pull 和git fetch
**git fetch和git pull的区别**
1.`git fetch`：相当于是从远程获取最新版本到本地，不会自动合并。
```
git fetch origin master
git log -p master..origin/master
git merge origin/master
```
>以上命令的含义：
 1.首先从远程的`origin`的`master`主分支下载最新的版本到`origin/master`分支上
 2.然后比较本地的`master`分支和`origin/master`分支的差别
 3.最后进行合并
 
上述过程其实可以用以下更清晰的方式来进行：
```
git fetch origin master:tmp
git diff tmp 
git merge tmp
```
2.`git pull`：相当于是从远程获取最新版本并`merge`到本地
```
git pull origin master
```
上述命令其实相当于`git fetch` 和` git merge`
在实际使用中，`git fetch`更安全一些，因为在`merge`前，我们可以查看更新情况，然后再决定是否合并。
##10.Git删除文件操作提交
https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013758392816224cafd33c44b4451887cc941e6716805c000 


##11.git删除远程分之后，本地同步问题
```
git pull --h和git fetch --h都发现了一个-p参数，可以用来删除远程已删除的分支本地git pull --rebase/git fetch后仍可见的远程在本地的镜像分支。如下

git pull --h/git fetch --h

    ......

     -p, --prune  prune remote-tracking branches no longer on remote.

    ......

经验证执行git pull/fetch -p后远程已删除的分支，本地的镜像不在了。
```

  [1]: https://7n.w3cschool.cn/attachments/image/20170206/1486348362884912.jpg
  [2]: https://blog.cnbluebox.com/images/gitlab_git.png