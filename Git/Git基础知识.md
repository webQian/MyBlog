# 一、Git配置基本命令
Git可以设置全局用户信息也可以对单个仓库进行设置，由参数config
决定设置的全局的还是单个仓库的，获取、修改用户信息同理  

设置全局用户名:
```
git config --global user.name "YourName"
```
设置全局邮箱:
```
git config --global user.email "YourEmail"
```
# 二、创建一个本地库
1.  在git bash中进入到要创建的本地库的磁盘

进入当前目录下的文件夹
```
cd 文件夹名
```
转到另一此磁盘
```
cd /盘名
```
2.  创建本地库的文件夹并进入该文件夹

创建Blog文件夹
```
mkdir Blog
```
进入该文件夹
```
cd Blog
```
3.  使用git init将该文件夹初始化为本地仓库

```
git init
```
4.  在该目录下创建一个文件
5.  使用git add "文件名" 将该文件添加到git的暂存区中

```
git add README.txt
```
6.  使用git commit -m "本次提交信息" 将暂存区中的文件提交到版本库中
```
git commit -m "提交了新创建的README.TXT文件"
```
# 三、将本地git与github连接
1.  通过git命令获得SSH key
 
通过 cd ~ 回到git的主目录
```
cd ~
```
如果之前使用过git，需要在主目录下查看是否有.ssh文件夹，以及该文件夹中是否有id_rsa和id_rsa.pub，如果有，则跳过此步骤2
2.  使用ssh-keygen -t rsa -C "YourEmail"
```
ssh-keygen -t rsa -C "YourEmail"
```
如果不需要设置密码，一路回车就好
3.  登录Github，在settings中选择SSH and GPG keys，然后新建一个SSH key，输入key的名字，然后打开主目录，在.ssh文件夹下找到id_rsa.pub文件，复制其中的内容到Key文本域中，添加

4.  如果是初次创建，使用
```
ssh -T git@github.com
```
然后输入yes即可

5.  创建仓库，在github中创建一个远程repository，创建成功后，在本地仓库中运行
```
git remote add origin git@github.com:YourGithubUsername/YourGithubRepository
```
6.  接下来就可以将你本地仓库中的文件提交到github上了
```
git push -u orgin master
```
由于仓库开始是空的，所以加上-u参数，加上-u后，git会把本地的分支和远程仓库的分支关联起来，之后提交时就不用添加参数-u，-u
# 四、查看仓库状态和提交日志
查看仓库状态
```
git status
```
查看提交日志
```
git log
```
查看工作区和暂存区的文件区别
```
git diff
```
通过git log可以得到你的每次提交到版本库的记录，每条记录中包括提交操作的id、提交人、提交时间和提交时的说明
# 五、进行版本回退
1.  先对本地库中的一个文件进行修改和提交
```
git add 
git commit -m
```
2.  通过git log查看提交日志
3.  得到id号进行版本回退
```
git reset --hard HEAD~回退几个版本
```
也可以在后面加id号来决定跳转到哪个版本，id号不用输全，可分辨即可
```
git reset --hard 版本号
```
如果忘记了版本号，可以使用
```
git reflog
```
里面记录着你每次操作的Id号，这样就能实现版本的操作了
# 六、git的暂存区和工作区
git add命令会把工作区的文件修改添加到暂存区中，而git commit会将暂存区中的所有文件修改全部进行提交
# 七、撤销修改
1. 第一种情况:只是在工作区进行了修改，但是还没有被放到暂存区中，这时候撤销修改就会让版本回到与暂存区中版本一致，其实就是撤销了在文件中的修改
```
git checkout -- 文件名
```
这时候你打开该文件，就会发现文件中你刚才进行的修改已经被撤销了
2. 进行了修改并且将其加入到了暂存区中，但是还没有提交，你可以使用git reset HEAD test.txt把暂存区的修改撤销掉，重新放到工作区
```
git reset HEAD
```
这时候可以使用git status命令看到文件被修改了但是还没有提交，然后你可以利用第一步来撤销修改，最后查看仓库状态，工作区也干净了
3. 如果你不但将文件加入到了暂存区，还将其提交到了版本库，可以使用
```
git checkout --hard HEAD
```
进行版本的回退，回退到你提交之前的版本
# 八、删除文件
一般来说，你删除文件都是在文件管理器中进行的，但是当你删除了文件时，git会告诉你删除了文件，这个时候你可以使用
```
git rm
git commit -m
```
从版本库中也删除该文件
如果你是删错了，那么可以使用
```
git checkout -- 文件名
```
git checkout其实是用版本库中的版本替换工作区的版本，无论是工作区还是版本库中的文件都可以进行还原，但是如果你直接删除了在工作区但是还没有提交到版本库的文件，那么你就需要到回收站还原了
