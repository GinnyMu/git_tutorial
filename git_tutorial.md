#Git Tutorial
##git 常用命令

![](http://upload-images.jianshu.io/upload_images/1736058-dda5369b0f7ebf93.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###设置

| 命令 | 说明 |
|--------|--------|
|   git config --global user.name     |   配置全局用户名     |
|    git config --global user.email    |     配置全局电子邮箱   |
|      git config --list  |   显示所有配置信息     |
###创建
| 命令 | 说明 |
|--------|--------|
| git init| 在本地初始化一个git仓库|
| git clone | 从远程服务器克隆一个仓库到本地|



###基础

| 命令 | 说明 |
|--------|--------|
|git add |添加|
|git add -A 　 |添加从status处可观察到的所有改变的文件 |
| git add README.md |只添加README.md |
| git rm 　| remove|
|git status  | 显示工作树的状态|
| git commit -m| 提交暂存区的文件，带有提交消息 m 代表message|
| touch | 创建|

NOTE:

1. git status 一般有三种状态:
 - Untracked files：未被跟踪的文件，表示是工作目录新增加的文件
 - Changes not staged for commit：工作目录中修改了文件，但是没有被添加到暂存区
 - Changes to be committed:添加到暂存区的文件，等待提交
 
2. git commit -m "docs(login model): update api document" 是git commit基本格式, 其中docs包含7中类别:
 - feat (新功能)
 - fix (bug修复)
 - docs (文档)
 - style (格式)
 - refactor(重构)
 - test 
 - chore (构建过程或辅助工具的变动)


###分支与合并
####git pull

git pull 分为两步

| column | column |
|--------|--------|
|    git fetch    |    从远端库下载最新的数据, 但是并不同步你本地库    |
|    git merge    |   从git fetch下载的数据同步到本地库     |

所以git pull 可理解为 git fetch+ git merge

####branch

| 命令 | 说明 |
|--------|--------|
|    git branch    |    可看见所有的branch    |
|git branch new_feature| 创建new_feature branch|
|   git checkout -   | 切换到最后使用的branch     |
| git checkout -b  new_feature_2  |  直接创建新的branch new_feature_2  并且保存到new_feature_2      |
Example:
-git checkout-: 
例如你从master切换到new_feature_2 可通过git checkout - 直接切换回master branch上 再次输入git checkout - 再次切换到new_feature_2

#### merge

| 命令 | 说明 |
|--------|--------|
|    git merge branchname    |  将指定分支合并到当前分支上    |
|     git merge oldbranchname newbranchname   |     将oldbranchname分支合并到newbranchname分支上   |

####get tag---reference to a commit can not be changed

| 命令 | 说明 |
|--------|--------|
|    git tag v1.0.0     |   create a tag v1.0.0(major/minor/patch)     |
|      git tag   |     show all tages   |
|    git tag -d v0.9   |   delete tag  v0.9    |
NOTE: 一般来说v1.0.0 第一个数字代表大型修改, 第二个数字小修改, 第三个数字修复bug之类的小操作


####git stash

| 命令 | 说明 |
|--------|--------|
|     git stash   |  save uncommited  changes  and dont show it in list      |
|git stash apply |bring back uncommitd file|

NOTE:
-当你在使用git stash apply的时候, 会出现错误提示, 可通过解决merge confilct的方法来解决

###push confilct
一般会出现在两个人修改了同一个file, 并且都push到了远端库上的时候. 当出现时:
git stauts   --查看是哪个file 在merge的时候出现了conflict
使用编辑器查看出错的file
![](http://ww3.sinaimg.cn/mw690/bf9ab080gw1f98l2x47v8j20q40bqmzd.jpg)

图中三个标记 `<<< HEAD `
`=====`
`>>>STRING`
区分了你做的更改和其他人做的更改. 此时可以选择

1. 保留自己的更改

2. 保留其他人的更改

3. 合并更改

做出更改以后重新commit push



###考察与比较

####log

| 命令 | 说明 |
|--------|--------|
|    git log    |     list all the commit(latest at top)   |
|    git log --oneline    |     show log history in single line|
|    git log --decorate     |     show all references    |
|    git log --graph    |     show merge path   |
|    git log --p   |    show changes made in each commit    |
|     git log --stat   |    show insertion and deletions    |
|   git log {argument}     |   filter git log for specific argument from log history     |
|     git log -3   |     show 3 most recent commit   |
|    git log --after= "yesterday"    |    show commit after yesterday    |
|     git log --before= "yesterday"   |   show commit before yesterday      |
|     git log --since xxx --until xxx   |     commit between   |
|   git log --author="XXX\xxxx"     |     作者是XXXX或者是xxxx   |
|   git log --grep ="copyright"     |   specific filter     |
|     git log -S"math"   |    find string math    |
|     git log -p -GMATH\RANDOM   |    show all changes that contain the word MATH OR RANDOM    |
|   git log -i -S"random"     |   i = ignore  显示所有random字符 不区分大小写     |
|    git log master .. new_feature    |   show log history between master and new_feature     |
|    git log README.md    |    show commit about README.md    |

NOTE:

1. when u enter log history:
press q to quit
f b  navigate by screen
j k  navigate by line
/    search for specific
n N  go forward and backward for search result

2. 都可以合并使用
example:  git log --oneline --graph


###git diff
修改文件以后 可以通过git diff 来查看对文件的修改

| 命令 | 说明 |
|--------|--------|
|     git diff -cached   |   show differece between stage area and last commit     |
| git diff HEAD  | show  differece between stage and unstage|
| git diff origin/master| show  differece between  origin/master   |

###修补与调试

####git blame
git blame getRandomElement.js   show commit history about getRandomElement.js


####git rebase

| 命令 | 说明 |
|--------|--------|
|     git rebase branchname   |     将指定分支上所有修改应用到当前分支上   |
|     git rebase branchname branchname   |   将第一个指定分支上所有修改应用到第二个分支上     |


####git bisect

| 命令 | 说明 |
|--------|--------|
|   git bisect start     |    start bisect    |
|     git bisect bad [<commit>]    |     设置指定提交（默认是当前分支）为bad |
|       git bisect good [<commit>] |     设置指定提交（默认是当前分支）为good   |
|git bisect reset|  quit bisect|
