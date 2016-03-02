# git入门笔记

```sh
$ git
```
---
linux系统：
`sudo apt-get install git`
可以通过源码安装,下载源码，解压，输入：
`./config`,`make`,`sudo make install`
---
### 设置
```sh
$ git config --global user.name "guohao"
$ git config --global user.email "guohao0817@gmail.com"
```
---
### 创建版本库
```sh
$ mkdir firstgit
$ cd firstgit
$ git init
```
---
把文件添加到仓库
```sh
$ git add readme.txt
$ git add file1.txt, file2.txt
$ git add . #添加所有文件
```
---
把文件提交到仓库
```sh
$ git commit -m "add a new file "
```
---
查看git状态
```sh
$ git status
```
---
对比本地仓库文件的修改
```sh
$ git diff a.txt
```
---
查看历史记录
```sh
$ git log
```
---
版本回退
```sh
$ git reset --hard HEAD^
$ git reset --hard HEAD^^
$ git reset --hard HEAD~100
$ git reset --hard 3628164
```
---
让这个文件回到最近一次`git commit`或`git add`时的状态
```sh
$ git checkout -- readme.md
```

nishi sb!!
hehe..you too
