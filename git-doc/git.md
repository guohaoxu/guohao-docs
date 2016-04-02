### git常用命令
---
**linux系统**

`sudo apt-get install git-core` ubuntu

`sudo yum install git-core` centos

**设置**

`$ git config --global user.name "username"`

`$ git config --global user.email "username@qq.com"`

`$ git config --list"` 查看设置信息

**创建SSH Key**

`$ ssh-keygen -t rsa -C "youremail@qq.com"`

在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥

**关联一个远程库**

`$ git remote add origin git@github.com:guohaoxu/guohao-docs.git`

`$ git remote rm origin` 删除关联远程库

`$ git remote -v` 查看远程库

`$ git push -u origin master` 第一次推送master分支

**克隆一个远程库**

`$ git clone git@github.com:guohaoxu/guohao-blog.git`

**创建版本库**

`$ mkdir firstgit`

`$ cd firstgit`

`$ git init`

**查看git状态**

`$ git status`

**查看git日志**

`$ git log`

**添加文件到仓库暂存区**

`$ git add readme.txt`

`$ git add file1.txt, file2.txt`

`$ git add .` 添加所有文件

**提交文件到仓库**

`$ git commit -m "add a new file "`

**对比工作区文件与仓库文件**

`$ git diff a.txt`

**查看历史记录**

`$ git log`

**版本回退**

`$ git reset --hard HEAD^`

`$ git reset --hard HEAD^^`

`$ git reset --hard HEAD~100`

`$ git reset --hard 3628164`

**文件回到最近一次仓库或暂存区**

`$ git checkout -- readme.md`

**从版本库中删除该文件**

`$ git rm test.txt`

`$ git commit -m "remove test.txt"`

---

**创建并切换dev分支**

`$ git checkout -b dev` 相当于以下两条命令

`$ git branch dev`

`$ git checkout dev`

**查看当前分支**

`$ git branch`

**把dev分支合并到master分支上**

`$ git merge dev`

`$ git merge origin/dev` 在本地分支上合并远程分支先fetch

**删除dev分支**

`$ git branch -d dev`

**取回远程仓库分支 自动与本地分支合并**

`$ git pull origin master:master`

`$ git pull origin master` 与本地的当前分支合并

**取回远程库所有分支更新**

`git fetch origin`

`git fetch origin master` 取回特定分支

`git branch -r` 查看远程分支

`git branch -a` 查看所有分支

`git push origin :test` 删除远程分支

`git push origin --delete test` 删除远程分支

没有冲突或者解决掉冲突后

`$ git push origin branch-name` 推送成功

---

**新建一个标签**

`$ git tag <name>`

`$ git tag -a <tagname> -m "blablabla..."` 指定标签信息

**查看所有标签**

`$ git tag`

**推送本地标签到远程仓库**

`$ git push origin <tagname>`

**推送全部本地标签**

`$ git push origin --tags`

**删除本地标签**

`$ git tag -d <tagname>`

**删除远程标签**

`$ git push origin :refs/tags/<tagname>`