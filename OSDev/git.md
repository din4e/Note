# Git的基础知识

## 简单介绍

Git是分布式版本控制系统，SVN是集中式版本控制系统。

### Git工作流程

1. 在工作目录中修改某些文件
2. 对修改后的文件进行快照，然后保存到暂存区域
3. 提交更新，将保存在暂存区域的文件快照永久转储到Git目录中

### SVN优缺点

#### SVN优点

1. 管理方便，逻辑明确，符合一般人思维习惯。
2. 易于管理，集中式服务器更能保证安全性。
3. 代码一致性非常高。
4. 适合开发人数不多的项目开发。  

#### SVN缺点  

1. 服务器压力太大，数据库容量暴增；
2. 如果不能连接到服务器上，基本上不可以工作，看上面第二步，如果服务器不能连接上，就不能提交，还原，对比等等；
3. 不适合开源开发（开发人数非常非常多，但是Google app engine就是用svn的）。但是一般集中式管理的有非常明确的权限管理机制（例如分支访问限制），可以实现分层管理，从而很好的解决开发人数众多的问题。

### git优缺点

#### git优点

1. 适合分布式开发，强调个体；
2. 公共服务器压力和数据量都不会太大；
3. 速度快、灵活；
4. 任意两个开发者之间可以很容易的解决冲突；
5. 离线工作；

#### git缺点

1. 学习周期相对而言比较长；
2. 不符合常规思维；
3. 代码保密性差，一旦开发者把整个库克隆下来就可以完全公开所有代码和版本信息；

## 基本操作区别：```reset```与```rebase```，```pull```与```fetch```，```rebase```和```merge```的区别

### ```reset```与```rebase```的区别

```reset```不修改commit相关的东西，只会去修改.git目录下的东西。  
```rebase``` 会试图修改你已经commit的东西，比如覆盖commit的历史等，但是不能使用rebase来修改已经push过的内容，容易出现兼容性问题。rebase还可以来解决内容的冲突，解决两个人修改了同一份内容，然后失败的问题。  

### ```pull```与```fetch```的区别

```pull``` 使用```git fetch```是取回远端更新，不会对本地执行```merge```操作，不会去动你的本地的内容。而是用```git pull```会更新你本地代码到服务器上对应分支的最新版本

### ```rebase```和```merge```的区别

```git merge```把本地代码和已经取得的远程仓库代码合并。
```git rebase```是复位基底的意思，gitmerge会生成一个新的节点，之前的提交会分开显示，而rebase操作不会生成新的操作，将两个分支融合成一个线性的提交。

### ```rebase```深入介绍

[rebase](https://www.codercto.com/a/45325.html)有两种用处合并分支以及合并commit。

## 基本操作

### 常见操作

```bash
git init # 使用之前需要先初始化
git show # 显示某次提交的内容 git show $id
git add <file> # 将工作文件修改提交到本地暂存区 
git add .
git commit -m ' ' #  
git rm <file> # 从版本库中删除文件
git reset <file> # 从暂存区恢复到工作文件
git reset HEAD^ # 恢复最近一次提交过的状态，即放弃上次提交后的所有本次修改
git diff <file> # 比较当前文件和暂存区文件差异 git diff
git log -p <file> # 查看每次详细修改内容的diff
git log # 按q退出
git branch -r # 查看远程分支
git merge <branch> # 将branch分支合并到当前分支
git stash # 暂存
git stash pop #恢复最近一次的暂存
git pull # 抓取远程仓库所有分支更新并合并到本地
git push origin master # 将本地主分支推到远程主分支
```

### git如何解决代码冲突

```bash
git stash
git pull
git stash pop
```

这个操作就是把自己修改的代码隐藏，然后把远程仓库的代码拉下来，然后把自己隐藏的修改的代码释放出来，让git自动合并。

### 如果要代码库的文件完全覆盖本地版本

```bash
git reset –hard
git pull
```

## 参考资料

[Gitbook中文版](http://gitbook.liuhui998.com/)  
[git rebase使用场景](https://www.jianshu.com/p/4079284dd970)
