# 初识GitHub
尝试使用GitHub
今天主要是尝试GitHub的一些常用命令，熟悉GitHub的功能
#### Git的常用命令行

---
Git安装包下载完成之后，在桌面会生成两个图标。其中客户端是直接通过各种按钮在本地仓库操作，最后同步到远程仓库。另一种方法就是通过命令来实现操作。今天学习的主要就是这个方法。
1. ##### 创建仓库


创建本地仓库，首先先选择文件夹 
```
cd e                //在E盘下寻找文件
cd testGit          //打开本地目录,testGit为自建的文件夹名称

```
##### 2.将远程仓库（在GitHub上建立的仓库）的文件下载到本地

```
git clone url  //这里的克隆地址在如下图的“Clone or download”里


```
![image](http://note.youdao.com/yws/public/resource/976ef2669aa8d0034c2a9b4243626af8/xmlnote/E069FF73F30A4A749DE268763A213EC4/1022)

这些命令完成之后，本地仓库就建立在了testGit文件夹下。
##### 3.设置贡献者

```
git config --global user.name                   //设置贡献者名
git config --global user.email "123456@qq.com"  //设置贡献者邮箱
```

##### 4.master就是主干，branch可以理解为master生成的副本，便于修改。
##### 5.Git的三个区
- 工作区  
- 暂存区
- 版本库

> 工作区可以理解为本地文件夹，将修改好的文件要先提交到暂存区，再提交到版本库

以下是用到的Git命令：

```
//添加到缓存区
git add filename     
git add .                                   //将更新过的文件全部提交
//添加到版本库
git commit filename                         
git commit filename -m "description"        //上面的方法在添加之后，会弹出一个文本，让书写描述内容，这个命令方法，直接一步达成
//可以将两步合成一步，一键将需要更新的文件提交到版本库
git commit filename -a -m "description"    

git log                                     //查看提交的历史版本
```

在提交的过程中，三部分的内容并不是完全一致的，该如何查看他们的不同呢？

```
git diff                    //工作区与暂存区之间的差别
git diff --cached           //暂存区与版本库
git diff --staged           //暂存区与版本库
git diff master             //工作区与版本库

```
文件已经上传到下一部分，该如何撤回呢？

```
git reset HEAD filename     //将暂存区文件撤回到工作区
git checkout --filename     //将工作区还原为版本库里的状态
//注意：如果缓存区有文件，先还原暂存区，再还原版本库
git commit -m "" --amend
```
删除操作

``` 
//首先，直接在工作区把文件删除，如果文件已经上传至暂存区，在暂存区的文件不会受到影响。

git rm filename             //删除暂存区的文件

//第二种情况，当工作区与暂存区都有文件时，用
git rm -f filename 
//删除两者，注意在这种情况下，只使用下面代码，这个时候是不会删除暂存区文件 
git rm

//第三种情况，如果只删除暂存区文档，但是不想删除工作区文档的时候
git rm --cache
```
恢复操作


```
//版本库中有我们上传的版本，当我们想获取已经上传到版本库中的文件时
git log                         //打印出所有修改的历史版本，版本信息中心含有版本id
git checkout id filename        //恢复到最新版本到工作区
git reset --hard id             //恢复版本
git reset --hard HEAD^          //还原上一版
git reset --hard HEAD~num       //num代表还原的版本数，如果是2，就是还原2个版本以前的版本，以此类推

```
##### 6.上传到远程仓库
做完上面这些，我们刷新网站，网站却没有什么变化，这是为什么呢？

其实以上我们已经介绍了GitHub在管理代码的三个工作区和常用到的代码，但是我们刚刚只是将我们的代码传到版本库，但是却没有上传到远程端上，同步到远程端上。这也是为什么刷新网站却没有变化的原因。

###### 准备工作

```
git remote                  //获取远程名字
git remote -v               //远程端地址
```
###### 开始上传

```
git push name master        //name是指上一步获取的远程名字，master这个位置可以填写“master”，或者其他分支的名字，这样就可以把我们的代码上传到GitHub的存储器上啦

```
###### 如何恢复到工作状态？
有时候我们会不小心把命令框输入工具给不小心关闭掉了，重新打开的时候，要恢复到工作状态，这个时候，就要用到以下命令了

```
git config --global user.name
git config --global user.email "email name"
//完成登录
cd..
cd..
cd testGit/test         //testGit是本地存储目录的名字，test是项目名称
```
###### 如何多人协作？
网站上setting里有add collborator里添加协作人
###### 当协作上传文档，发生冲突时，如何解决冲突？
这个时候，建议先下载源文件，查看区别再上传

```
git fetch                               //将文件下载到本地
git diff master origin/master           //查看区别，origin是远程端名字，master是主分支的名字
git merge origin/master                 //这个方法也可以查看区别
git commit -a -m                        //在本地修改好代码后，提交
git push                                //上传
```
##### 7.分支

```
git branch                              //获取当前分支
git branch new                          //创建以“new”为名的分支
git checkout new                        //切换到“new"分支
git branch -b new1                       //创建并切换到分支new1
git merge new1                          //将分支new1的改动内容合并到master上
git branch --merged                      //当前master上与哪些分支合并了
git branch --no --merged                 //当前master 没有合并哪些分支
git branch -d new1                      //删除new1分支
git branch --D new1                     //强制删除

```
修改分支上的内容并上传到服务器
```
git merge new           //先试试合并，如果有错误时
git status              //查冲突
git add.                //提交全部
git commit -m"test"     //提交到test项目中
git push origin new1    //上传到名为origin的远程上，new1的分支上

```
