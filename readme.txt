*********************************************************
git基本常用命令和安装
1.git安装
	下载一路安装。没啥问题。
	需要配置用户名和邮箱。
	
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
	3)最麻烦的了，
		如果确认删除本地文件，想要远程github同步。按照1的方法执行，然后再添加一个命令 git push -u origin master或者git push(命令窗口会警告,看不懂）
		如果不知道出了什么问题就是同步不了。也别着急，先git pull下来，然后执行3的操作就ok啦。
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

现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令,添加远程仓库：

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


三.从远程仓库克隆至本地
1.登录github,建一个新的仓库，这次名叫做gitskills,勾选initialize this reposity with a README
2.要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
本地命令git clone克隆一个本地库：

$ git clone git@github.com:xxxxxx/gitskills.git

cd gitskills
ls
就可以查看到本地的README.md

你也许还注意到，GitHub给出的地址不止一个，还可以用https://github.com/michaelliao/gitskills.git这样的地址。
实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。

使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。



四.分支的创建合并和删除
Git鼓励大量使用分支：

查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>

案例中给的<name>都用的dev


五.解决冲突
比如：
我们创建新的分支feature1(git checkout -b feature1)，并在新的分支提交。
然后切换回到主分支（git checkout master）,写一句很相似的话，就一两个字不同。提交。

合并这个新的分支：git merge feature1
会提示冲突了，
我们直接查看readme.txt内容，显示了这两个不同分支上做出的修改。需要我们手动修改成最终想要的样子。。。保存。提交。
用带参数的log可以看到修改后分支的情况。
git log --graph --pretty=oneline --abrev-commit
最后，删除feature1分支，工作完成。
小结：
当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

用git log --graph命令可以看到分支合并图。


六.分支管理策略。
方法：
1.创建分支(git checkout -b dev)，添加内容，提交(add+commit -m "")，切换回到主分支(git checkout master)，
合并新的分支（git merge --no-ff -m "merge with no-ff" dev）,带参数的log查看（git log --graph --pretty=oneline --abbrev-commit）

合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

this is branch1.

-----------------------------------
七.bug分支
比如要紧急处理一个bug，但是在dev分支上的还不能提交，因为还没完成。
Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：
git stash
首先，在哪个分支修复bug，先切换到那个分支，然后再那个分支上再创建临时分支

git checkout master
git checkout -b issue-101

进行bug修复工作,修改完成后

git add readme.txt
git commit -m "fix bug 101"
git checkout master
git merge --no-ff -m "merged bug fix 101" issue-101
git branch -d issue-101

完成了bug修复和提交合并
可以继续完成分支dev上的工作
git checkout dev
git status
//此时工作区是干净的。没有东西
git stash list//查看刚才的工作现场

工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：

一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

另一种方式是用git stash pop，恢复的同时把stash内容也删了：

再用git stash list查看，就看不到任何stash内容了：

你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令：

$ git stash apply stash@{0}

----------------------------------
八.Feature分支
新功能，实验性的代码，在分支上操做
git checkout -b "feature-valcan"
git add valcan.txt
git commit -m "add valcan.txt"
git checkout dev
所以，feature分支和bug分支是类似的
然后合并，删除
git merge feature-valcan
git branch -d feature-valcan

如果，此时。我们需要强行删除这个分支，这个功能不需要了。
git branch -D feature-valcan
就可以强制删除，我们做的修改将不会保存。
总结：
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

----------------------------------
九.多人协作
$ git push origin master
如果要推送其他分支，比如dev，就改成：

$ git push origin dev
但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

master分支是主分支，因此要时刻与远程同步；

dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。


多人协作的工作模式通常是这样：

首先，可以试图用git push origin branch-name推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，
用命令git branch --set-upstream branch-name origin/branch-name。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。



***********************************************************
一。标签管理

发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。
将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。
Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。

------创建标签
1.切换到分支上，git checkout master
2.打新标签 git tag v1.0
3.查看所有标签git tag
默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？

方法是找到历史提交的commit id，然后打上就可以了：
比方说要对add merge这次提交打标签，它对应的commit id是6224937，敲入命令：
$ git tag v0.9 6224937

注意，标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息：

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：
$ git tag -a v0.1 -m "version 0.1 released" 3628164

--------------------------------------------------------------------------------------
用PGP签名的标签是不可伪造的，因为可以验证PGP签名。验证签名的方法比较复杂，这里就不介绍了。
还可以通过-s用私钥签名一个标签：
$ git tag -s v0.2 -m "signed version 0.2 released" fec145a

签名采用PGP签名，因此，必须首先安装gpg（GnuPG），如果没有找到gpg，或者没有gpg密钥对，就会报错：
gpg: signing failed: secret key not available
error: gpg failed to sign the data
error: unable to sign the tag
如果报错，请参考GnuPG帮助文档配置Key。

用命令git show <tagname>可以看到PGP签名信息：
--------------------------------------------------------------------------------------
小结

命令git tag <name>用于新建一个标签，默认为HEAD，也可以指定一个commit id；

git tag -a <tagname> -m "blablabla..."可以指定标签信息；

git tag -s <tagname> -m "blablabla..."可以用PGP签名标签；

命令git tag可以查看所有标签。

------操作标签

如果标签打错了，也可以删除：
$ git tag -d v0.1
因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令git push origin <tagname>：
$ git push origin v1.0

者，一次性推送全部尚未推送到远程的本地标签：
$ git push origin --tags

如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
$ git tag -d v0.9
然后，从远程删除。删除命令也是push，但是格式如下：
$ git push origin :refs/tags/v0.9

---------
小结

命令git push origin <tagname>可以推送一个本地标签；

命令git push origin --tags可以推送全部未推送过的本地标签；

命令git tag -d <tagname>可以删除一个本地标签；

命令git push origin :refs/tags/<tagname>可以删除一个远程标签。

*************************************************************

使用github
在GitHub上，可以任意Fork开源仓库；

自己拥有Fork后的仓库的读写权限；

可以推送pull request给官方仓库来贡献代码。
**************************************************************
自定义git
配置颜色：(全局)
git config --global color.ui true

忽略特殊文件：
.gitignore
在线忽略文件地址https://github.com/github/gitignore
最后一步就是把.gitignore也提交到Git，就完成了！当然检验.gitignore的标准是git status命令
是不是说working directory clean。

如果你确实想添加该文件，可以用-f强制添加到Git：

$ git add -f App.class
或者你发现，可能是.gitignore写得有问题，需要找出来到底哪个规则写错了，可以用git check-ignore命令检查：

$ git check-ignore -v App.class

------
配置别名
git config --global alias.st status

git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch

ustage操作
git reset HEAD file 可以把暂存区的修改撤销掉（unstage），重新放回工作区，可以配置一个unstage别名
git config --global alias.unstage 'reset HEAD'
那么输入git unstage test.txt === git reset HEAD test.txt
git config --global alias.last 'log-l'可以用git last查看最后一次的信息提交。
配置log
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"


配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

配置文件放哪了？每个仓库的Git配置文件都放在.git/config文件中：

别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。

当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中：
配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。

******************************************************
******************************************************
期末总结：

安装软件--初始化仓库（git init）--配置用户名和邮箱--放到暂存区--提交到版本库--查看日志（一行日志，全部日志）
--查看状态--版本回退（当前版本，上一个，上n个版本，指定版本）--修改（查看）--撤销修改（checkout unstage）--删除（确定删除和误删）

添加远程仓库--推送到远程----克隆远程仓库到本地

分支(创建，切换，合并，删除）
--bug分支--feature分支----多人协作
--
标签管理--创建普通标签，带a，m参数标签，s,m参数标签--查看标签--删除标签----推送标签（单个和全部）---远程删除标签

配置颜色--忽略特殊文件--配置别名---配置文件存放位置

*********************************************************
*********************************************************