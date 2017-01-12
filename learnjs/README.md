# Seven important tips for git users
> [实验楼](https://www.shiyanlou.com/question/2577)  
It's necessary for programmers to use a version control system during development.

由于大部分时间都只会用到` add, commit, branch, push/pull `等，如果是提交错误的文件或者信息呢？
这就需要我们来用下面的特殊技巧了。

1. 修改错误的提交信息(`commit message`) 
下面的命令可以让你编辑保留在代码库（code base）中最近一次的提交信息，但要确保没有对当前的代码库（working copy）做修改，
否则修改内容会随之一起提交。 
```shell
$ git commit --amend -m "YOUR-New-Commit-Message"
``` 
假如你已经提交（`git commit`）推送（`git push`）到远程分支，下面的命令将强制推送本次提交：
```shell
$ git push <remote> <branch> --force
``` 
建议关注下[Stack Overflow](http://stackoverflow.com/questions/179123/edit-an-incorrect-commit-message-in-git/179147#179147)
2. 提交之前撤销`git add`
若你向暂存区（staging area）加入了一些错误的文件，但是还没有提交，一条命令搞定：
```shell
$ git reset
```
当然你可以指定文件名来移除指定文件。 
可以关注[Stack Overflow](http://stackoverflow.com/questions/348170/undo-git-add-before-commit/348234#348234)
3. 撤销最近一次代码提交
直接贴上：
```shell
$ git reset --soft HEAD~1 #工作文件更改
$ git add -A .
$ git commit -c ORIG_HEAD
```
** 说明 **
执行第一条命令，HEAD指针（pointer）移向此前的一次提交，之后才能移动文件或者修改。 
最后命令，git会打开你的默认文本编辑器，其中会包含上一次提交时的信息。
当然，你可以修改提交信息，或者使用参数`-C`而不是`-c`，来路过这一步。
4. Git仓库撤销至前一次提交时的状态
撤销（revert）非常有必要的--尤其在你把代码搞的一团糟的情况下，常见的情况是，你想回到之前代码版本，检查下
那个时候的代码库，然后再回到现在状态。
```shell
$ git checkout <SHA>
```
""中填入的是你想查看的提交拥有哈希值（Hash Code）中前8-10个字符，这个命令使<HEAD>指针脱离（detach）,
可以让你在不检出（）任何分支的情况下查看代码--脱离HEAD并不像听上去那么可怕。 
```
$git checkout -b <SHA>
```
回到当前工作进度，只需检出（check out）所在分支即可。  
可以关注[Stack Overflow](http://stackoverflow.com/questions/4114095/revert-git-repo-to-a-previous-commit/4114122#4114122)
5. 撤销合并（Merge）
要想撤销合并， 你可能必须使用恢复命令（HARD RESET）回到上一次提交的状态。  
“合并”所做的工作基本上就是重置索引，更新working tree（工作树）中的不同文件，
即当前提交（`git commit`）代码中与HEAD 游标所指向代码之间的不同文件；但是合并会保留索引与working tree之间的差异部分（例如那些没有被追踪的修改）。
```shell
$ git checkout -b <SHA>
```
其它办法，可以查看[这篇文章](http://stackoverflow.com/questions/2389361/undo-a-git-merge?rq=1)
6. 从当前分支移除未追踪的本地文件
假设你凑巧有一些未被追踪的文件（因为不再需要它们），不想每次使用`git status`命令时让它们显示出来。下面是解决这个问题的一些方法： 
```shell
$ git clean -f -n # 1
$ git clean -f # 2
$ git clean -fd # 3
$ git clean -fX # 4
$ git clean -fx # 5
```
(1): 选项-n将显示执行（2）时将会移除哪些文件。  
(2): 该命令会移除所有命令（1）中显示的文件。  
(3): 如果你还想移除文件件，请使用选项-d。  
(4): 如果你只想移除已被忽略的文件，请使用选项-X。  
(5): 如果你想移除已被忽略和未被忽略的文件，请使用选项-x。  
** 请注意最后两个命令中X的区别。 **  
更多详情，查看官方文档[git-clean](http://git-scm.com/docs/git-clean)
7. 删除本地和远程Git分支
删除本地分支：
```shell
$ git branch --delete --force <BranchName>
```
或者使用简写参数选项：
```shell
$ git branch -D
```
删除远程分支：
```shell
$ git push origin --delete <BranchName>
```
详情请参考 [Git官方文档][0]。
---
文章来源： * 编程派 *  
链接地址：[编程派](http://www.codingpy.com/article/seven-git-hacks-you-just-cannot-ignore/)  
2015-12-04 14:07  
![addr-map](http://www.hfsyrj.com/uploadfile/2015/1106/20151106102710306.gif)

[0]: http://git-scm.com/doc