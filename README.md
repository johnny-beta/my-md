## cvs dvs

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

    ---

    git 暂存区设计你本地改到一半，同事跟你说有个紧急的 bug 需要修复。你不想将改到一半的东西 commit 进去。所以先 stash 一下，改掉 bug 并 commit，然后 `stash pop` 出来继续没完成的工作。

    # Stage 赋予 Git 更多灵活性

    不知道时，你对它可能毫无所感。知道后，你一定会感动地想哭，并十分之膜拜 Git 的开发者- Linus Torvalds ，stage 就是这么精彩的玩意。以下看起来比较束手无策的场景，只要理解 stage,用好相应命令，都能轻易解决：

    - 修改了4个文件，在不放弃任何修改的情况下，其中一个文件不想提交，如何操作？（没add : git add  已经add: git reset --soft ）
    - 修改到一半的文件，突然间不需要或者放弃修改了，怎么恢复未修改前文件？ (git checkout)
    - 代码写一半，被打断去做其他功能开发，未完成代码保存？(git stash)
    - 代码写一半，发现忘记切换分支了？(git stash & git checkout)
    - 代码需要回滚了？（git reset）
    - 









------

![](https://raw.githubusercontent.com/DRPrincess/BlogImages/master/qiniu/2429e4d2661e60027537aea0077f6e40.png)



```flow
st=>start: 开始
op=>operation: 我的条件
cond=>condition: 判断是否通过
op1=>operation: 测试条件
e=>end: 结束
st->op->op1->cond
cond(yes)->e
cond(no)->op
```



bug fix

![Git flow](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015122302.png)



> git diff工作区 vs 暂存区
>
> git diff head工作区 vs 版本库
>
> git diff --cached暂存区 vs 版本库


master分支下的修改
我在这里bugfix下也修改了文件

