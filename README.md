# CVS（Concurrent Versions System）与DCVS

![](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384860735706fd4c70aa2ce24b45a8ade85109b0222b000/0)





![](https://cdn.liaoxuefeng.com/cdn/files/attachments/0013848607465969378d7e6d5e6452d8161cf472f835523000/0)

# git安装



# git命令 

1. git add 
2. git commit 
3. git checkout 
4. git head 
5. git reset 
6. git revert
7. git log 
8. git reflog
9. git branch
10. git pull 
11. git fetch
12. git rebase
13. git statsh

# git分区

![](https://raw.githubusercontent.com/DRPrincess/BlogImages/master/qiniu/2429e4d2661e60027537aea0077f6e40.png)



> git diff工作区 vs 暂存区
>
> git diff head工作区 vs 版本库
>
> git diff --cached暂存区 vs 版本库
>
> 

# Stage 赋予 Git 更多灵活性

不知道时，你对它可能毫无所感。知道后，你一定会感动地想哭，并十分之膜拜 Git 的开发者- Linus Torvalds ，stage 就是这么精彩的玩意。以下看起来比较束手无策的场景，只要理解 stage,用好相应命令，都能轻易解决：

- 修改了4个文件，在不放弃任何修改的情况下，其中一个文件不想提交，如何操作？（没add : git add  已经add: git reset --soft ）
- 修改到一半的文件，突然间不需要或者放弃修改了，怎么恢复未修改前文件？ (git checkout)
- 代码写一半，被打断去做其他功能开发，未完成代码保存？(git stash)
- 代码写一半，发现忘记切换分支了？(git stash & git checkout)
- 代码需要回滚了？（git reset）
- git 暂存区设计你本地改到一半，同事跟你说有个紧急的 bug 需要修复。你不想将改到一半的东西 commit 进去。所以先 stash 一下，改掉 bug 并 commit，然后 `stash pop` 出来继续没完成的工作。

------



bug fix



分支



![Git flow](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015122302.png)--

---

![](http://www.softwhy.com/data/attachment/portal/201808/04/001249htotjm4kb8bacj4s.jpg)

**二.分支种类作用介绍：**

**1.master分支：**

此分支通常用来存放项目的稳定版本，主要特点如下：

（1）.内容来源主要是分支合并过来，不推荐开发者直接commit提交。

（2）.由于master分支可以是稳定版本，可以随时上线，所以通常版本标签都是打在master分支各个提交之上。

关于标签的用法可以参阅[Git tag标签用法详解](http://www.softwhy.com/article-8541-1.html)一章节。

**2.develop分支：**

develop开发分支通常和feature特征分支配合使用，它是所有feature特征分支的基础。

当在feature分支中测试完新开发的功能后，可以将其合并到develop分支。

**3.hotfix分支：**

当出现紧急问题，比如master线上分支出现代码问题，可以在此分支中进行修补，修补之后然后再合并到master分支。

特别说明：在合并到master主分支的同事，还要合并一份到develop分支，否则之后将develop合并到master时候，可能会导致修复的问题复现。

**4.release分支：**

当develop分支开发到自认为足够稳定的状态，将此分支合并到release分支（在此分支进行上线前的最后测试）。

最后测试完成后，再合并到master分支和develop分支。

合并到master分支是非常好理解的，因为要上线运行。合并到develop是因为release分支后续可能还会发现问题，所以要将与develop分支同步，以防止以后develop再合并到release分支出现问题。

**5.feature分支：**

此分支作用其在介绍develop分支的时候已经涉及，在feature进行新功能的开发，开发完成后再合并到develop。

---

#### fast-forward

#### git rebase

#### git merge --no-ff

master分支下的修改
我在这里bugfix下也修改了文件
master里只在工具区改了
my-server端修改内容

---

- [x] 本地任务1
- [ ] 本地任务2
- [ ] 本地任务3



