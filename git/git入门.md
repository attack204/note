# git

## git

先来个总领，也是我心底里的一个疑惑，为什么不用文件上传按钮上传而要用一个破命令行

原因有2

1. http协议需要经过多次握手等操作，而ssh协议不需要，因此ssh协议更高效
2. 用命令行虽然繁琐，但是能应对更加复杂的业务场景

## git常用命令

### clone 

```git
git clone <地址> //即可将<地址>内的文件传到本地
```

notice：
1. git clone是一个很nb的操作，不仅可以clone用户的文件，还可以clone用户已经执行的remote操作

2. clone与pull的区别：pull时已经有仓库了，而clone时没有仓库


### add

```git
git add . //将所有新增文件添加到缓存区
git add <FileName> //将FilaName文件添加到缓存区

```

每次add操作都会把需要更新的文件提交到缓存区，这个过程非常复杂。但是可以知道的是，每次add操作都是增量更新，也就是只更新与原文件的diff。并且这个diff是通过LCS算法来完成的。我在这里做了一个测试：输出2e8个1，然后git add，发现用时2s左右，但是在源文件的末尾添加一个2，再执行git add，即刻便能完成

 这里不妨再提一点add的原理类的内容，add操作在进行时是生成一个40位的hash，其中前两位作为文件夹的名称，后38为作为文件夹内文件的名称。每次的更新都会以这种方式进行储存。

![](http://cdn.attack204.com/20200803192411.png)

![](http://cdn.attack204.com/20200803192657.png)

(两张图的对比说明31和93两个文件是新加入的，此文件在目录.git/object下)


### status

```git
git status //查看自上次提交之后有无更改
git status -s //功能与上类似，但只显示简略信息
```

### commit

git为每次提交都会记录名字与邮箱，因此在提交之前需要先进行配置，其实不提前配置也可以，因为会报错。。。。

```git
git commit -m '提交注释'
```

注意：这个-m命令建议写上，如果不写，git会开启一个vim窗口来让你写。。。。

to do 
1. 当目前状态与仓库状态有冲突时如何处理

### remote

remote命令可以对远程仓库进行重命名

```git
git remote add origin git@address
```

执行完这句话后，原本的`git@address`会被我们重命名为`origin`

因此原来的
```git
git push git@address master
```

可以改为
```git
git push origin master
```

### push

基本用法
```git
git push 仓库地址 分支名称
```

#### -u实现记忆功能

每次填写仓库地址和分支名称是一件很麻烦的事情

可以用一次
```git
git push -u 仓库地址1 分支名称1
```

这样再使用
```git
git push
```
即可自动提交到仓库地址1、分支名称1

notice:注意一个细节，即使文件没有更新，使用git push -u不会成功进行提交，但也可以实现记忆功能

### log

可以查看提交记录

```git
git log
```

![](http://cdn.attack204.com/20200929205623.png)

## git的撤销操作

1. 从暂存区恢复文件 

```git
git checkout 文件名
```

notice: 

* 该操作会覆盖当前的文件
* 执行该操作的前提是checkout之后的文件已经被执行过add操作，并不需要被执行commit操作
   
2. 删除暂存区的文件

```git
git rm --cached 文件名
```

3. 版本回退

```git
git reset --hard commitid
```

notice: 
4
* 该操作需要之前有过commit
* commit记录可以用`git log`查看

## git的分支操作

git的分支是一个list而不是tree

```git
git branch //查看分支
git branch 分支名称 //创建分支
git checkout 分支名称 //切换分支
git branch -d 分支名称 //删除分支，将-d改为-D可以强制删除(正常情况下需要把分支merge到主分支后才能删除)
git merge 被合并分支//一般此操作都是在master分支下进行的，被合并分支需要保证执行过commit操作
git branch -M oldbranch newbranch //-M表示强制命名
```

notice:

1. 执行checkout命令时，需要确保之前的分支已经进行过commit操作

## git暂时保存更改

```git
git stash //保存当前分支上所做的更改
git stash pop //恢复分支上所作的更改
```

这玩意儿的应用场景比较奇怪，比如当前我正在开发一个分支，但是并没有commit，而此时又必须去另一个分支开发，这样就可以用git stash保存一下

也可以选择直接commit，但commit的内容是一个尚未开发完的内容，可能不太好

也可以直接把工作目录复制出来，，，但是比较zz。。


## git常用组合操作操作

1. 将文件夹内的文件上传到某个仓库]

抄袭自github官方指南

```cpp
git init
git add .
git commit -m "first commit"
git branch -M master
git remote add origin git@github.com:attack204/BlogIndex.git
git push -u origin master
```

## git忽略文件

在本地添加文件`.gitignore`，里面输入需要被忽略的文件的名称即可

## github相关操作

### 冲突解决

1. git不能自动解决冲突，需要其中一个人把仓库事前pull到本地，修改之后再进行提交

### 非团队程序员提交代码

1. 首先将代码fork一份
2. 对已经fork完的代码进行修改
3. 提交pull request

### ssh免登陆

1. 在本地生成ssh
2. 在github添加ssh

## 注意事项

### add与commit的区别

问题由来：

在git中经常组合执行以下命令

```git
git add .
git commit -m 'update'
```
解释：

首先add命令与commit命令的功能

add命令是将本地文件提交到缓存区，整个操作都是在本地的。

commit命令是在建立本机与远程主机的联系，这也是为什么之前提到在执行此命令前需要设置用户身份和提交注释

我觉得形象一点可以这么理解：add相当于收拾行李，commit相当于买票，push相当于出发






