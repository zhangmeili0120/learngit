git is a distributed version controll software.
git is free software distributed under the GPL..
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
	