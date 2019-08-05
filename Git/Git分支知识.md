# 一、Git的分支
在Git中，会把每次提交串成一条时间线，这条时间线就是一个分支。在Git里，这个分支叫做主分支，也就是master,HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以HEAD指向的就是当前分支
![image](CF9D8D73FC7D420BAC6A12179D4E48DA)

每次提交时，master分支都会向前进一步，随着不断提交，master分支的线就会越来越长。
# 二、新的分支
当新创建一个new分支时，git新创建了一个new指针，指向master相同的提交，再把HEAD指向新的分支，就表示当前分支在new上

![image](0727AFF6B04445C7B4FBEAC87F108548)

但是当当前分支改变时，这时候的每一次提交就会在该分支上进行提交，此时new指针就会向前移动，而master指针不变

![image](CB81945CA9B14810A24890CE5A2F5CFF)

当我们在new分支上完成工作后，就可以将new分支和master分支进行合并，Git分支合并时:将master指向New分支当前的提交，就完成了合并，移动master指针到新分支上。

![image](53B2766654794F22A890B17738D897B9)

当你合并分支后就可以将创建的分支删除了。

# 三、实践一下
1. 创建新分支，并转到新分支上
```
git branch 分支名
git checkout 分支名
```
上面的两条语句也可以合并为一条
```
git checkout -b 分支名
```
代表创建一个新分支并且移动到该分支上
2. 在该分支上创建一个文件，然后提交
3. 在newBranch分支上工作完成，将master指针指向newBranch分支
先将分支切换到master分支上，再进行合并
```
git merge newBranch
```
4. 合并分支后删除该分支

# 四、分支冲突的产生原因
在两个已经提交的分支的相同文件的相同位置进行了不同的操作，git不知道需要提交到远程仓库哪一个，产生了分支冲突。
在修改之前，先合并别的分支。
先pull更新项目，在Push上传项目
# 五、分支管理策略
在合并分支时，默认采用的是Fast forward模式，在这种模式下，删除分支后，会丢掉分支信息，如果强制禁用了该模式，**git在合并时会生成一个新的commit**。
```
git merge --no-ff -m "会生成新的commit" 分支名
```
在进行开发时，master分支是不能动的，都在一个新的分支(dev)上进行工作，等到要发布新版本1.0时，把dev合并到master分支上，
而每个人都有自己的分支，时不时的向dev分支上合并就好了。
# 六、bug分支
当在一个分支上进行开发时，需要去解决一个Bug，首先需要将你在该分支上的工作隐藏，然后创建一个新的分支去解决Bug，在Bug解决完毕后，将该分支进行合并，然后取出被隐藏的分支，继续工作
使用git stash隐藏当前分支上的工作
```
git stash
```
恢复被隐藏的工作
```
git stash apply
```
使用git stash apply，stash上的内容并不会删除，你需要手动的进行删除
```
git stash drop
```
或者使用合并语句，取出内容并删除
```
git stash pop
```
还可以隐藏多个任务，在恢复时，利用git stash list查看列表，然后使用git stash apply进行恢复
```
git stash list
git stash apply stash@{o}
```
# 七、Feature分支
当有一些实验性工作时，应该创建一个feature分支。
在你还没有合并时当功能取消时，使用
```
git branch -D Feature分支
```
应该使用大写的参数D来强制删除分支，因为该分支上的提交还没有合并
# 八、标签
为了替代不好辨识的Id，可以给一个分支添加一个id来进行标识
```
git tag <name> 可选的commit id
```
带说明的标签
```
git tag -a 标签名 -m "说明" commit id
```
获得说明
```
git show 标签名
```
删除标签
```
git tag -d 标签名
```
推送标签到远程
```
git push origin 标签名
```
给一个分支添加了标签后

