### git常用命令

```shell
$ git
```

linux系统：

`sudo apt-get install git`

`./config`,`make`,`sudo make install`

设置`$ git config --global user.name "guohao"`,`$ git config --global user.email "guohao0817@gmail.com"`

创建SSH Key `$ ssh-keygen -t rsa -C "guohao0817@gmail.com"`
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥

要关联一个远程库，使用命令`git remote add origin git@github:guohaoxu/guohaoxu.git`

使用命令`git push -u origin master`第一次推送master分支的所有内容

每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改

用命令`$ git clone git@github.com:guohaoxu/guohao-blog.git`克隆一个远程库

创建版本库`$ mkdir firstgit`, `$ cd firstgit`, `$ git init`

把文件添加到仓库`$ git add readme.txt`, `$ git add file1.txt, file2.txt`, `$ git add . #添加所有文件`

把文件提交到仓库`$ git commit -m "add a new file "`

查看git状态`$ git status`

对比本地仓库文件的修改`$ git diff a.txt`

查看历史记录`$ git log`

版本回退 `$ git reset --hard HEAD^`, `$ git reset --hard HEAD^^`, `$ git reset --hard HEAD~100`, `$ git reset --hard 3628164`

让这个文件回到最近一次`git commit`或`git add`时的状态 `$ git checkout -- readme.md`

从版本库中删除该文件,用命令`$ git rm test.txt`, `$ git commit -m "remove test.txt"`

创建dev分支，然后切换到dev分支：`$ git checkout -b dev`

`git checkout`命令加上-b参数表示创建并切换，相当于以下两条命令：`$ git branch dev`, `$ git checkout dev`

查看当前分支 `$ git branch`

把dev分支的工作成果合并到master分支上：`$ git merge dev`

删除dev分支 `$ git branch -d dev`

多人协作的工作模式通常是这样：

首先，可以试图用`git push origin branch-name`推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream branch-name origin/branch-name`

命令`git tag <name>`用于新建一个标签，默认为HEAD，也可以指定一个commit id；

`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；

命令`git tag`可以查看所有标签。

命令`git push origin <tagname>`可以推送一个本地标签

命令`git push origin --tags`可以推送全部未推送过的本地标签

命令`git tag -d <tagname>`可以删除一个本地标签

命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签
