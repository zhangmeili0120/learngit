1.git安装
2.git创建版本库
	git bash here打开命令窗口进行操作。
	
	mkdir learngit//当前目录下创建一个learngit文件夹
	cd learngit//从目前的目录切换到learngit目录下
	pwd是可以查看当前在哪个目录
	git init//创建一个空的仓库，会自动生成一个.git文件夹
3.历史穿梭
	git log//查看日志
	git log// --pretty=oneline//一行简洁日志
	git reflog//查看所有的日志，含有版本号信息
	git add readme.txt
	git commit readme.txt -m "there is zhushicontent"
	git status//查看状态
	git diff//查看修改的内容

	git reset --hard HEAD^//回退到上一个版本
	git reset --hard HEAD^^//回退到上两个版本
	git reset --hard HEAD~100//回退100个版本
	git reset --hard 6位版本号
	
4.工作库和暂存区
	工作库是我们写的项目，暂存区是git add之后放在.git 里边暂存。需要commit之后才算放入了版本库。
5.管理修改
	提交后，用git diff HEAD -- readme.txt命令可以查看工作区和版本库里面最新版本的区别：
6.撤销修改
	1）git checkout -- readme.txt//丢弃工作区的修改
	2) git reset HEAD readme.txt//丢弃暂存区的修改（unstage),重新放回工作区，然后git checkout -- readme.txt丢弃工作区的修改
7.删除文件
	rm test.txt 删除test.txt文件
	1）确定删除
	git rm test.txt
	git commit -m "remove test.txt"
	2)删错了，因为版本库还有，可以一键还原
	git checkout --test.txt
	
****************************************************

*****************************************************
一，远程仓库的使用
1.注册github账号，要使用自己可以用的，能收到邮件验证的邮箱。

2.
	第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，
如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
$ ssh-keygen -t rsa -C "youremail@example.com"
这样你的本地就有了这个目录和这两个文件。如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，
这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
	
	第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

二，添加远程库
现在的情景是，你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，
又可以让其他人通过该仓库来协作，真是一举多得。

首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：
在Repository name填入learngit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：
目前，在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令：

$ git remote add origin git@github.com:xxxxxx/learngit.git
---其中xxxxxx改成你的github账户名。
添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

下一步，就可以把本地库的所有内容推送到远程库上：

$ git push -u origin master
把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。

由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，
还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

现在起，只要本地作了提交，就可以通过命令：

$ git push origin master
把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！




