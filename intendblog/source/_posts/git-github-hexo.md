---
title: git+github+hexo学习
date: 2020-06-21 16:33:25
comments: false
auto_excerpt: true
toc: true
tags: hexo
categories: 
description:
---
此文仅是本人学习笔记。

## 1、什么是版本控制

版本控制（Revision control）是一种在开发的过程中用于管理我们对文件、目录或工程等内容的修改历史，方便查看更改历史记录，备份以便恢复以前的版本的软件工程技术。
•	实现跨区域多人协同开发
•	追踪和记载一个或者多个文件的历史记录
•	组织和保护你的源代码和文档
•	统计工作量
•	并行开发、提高开发效率
•	跟踪记录整个软件的开发过程
•	减轻开发人员的负担，节省时间，同时降低人为错误
简单说就是用于管理多人协同开发项目的技术。

## 2、SVN与Git优缺点比较

### （1）SVN优缺点
优点： 
1、	管理方便，逻辑明确，符合一般人思维习惯。 
2、 易于管理，集中式服务器更能保证安全性。 
3、 代码一致性非常高。 
4、 适合开发人数不多的项目开发。
缺点： 
1、 服务器压力太大，数据库容量暴增。
2、 如果不能连接到服务器上，基本上不可以工作，看上面第二步，如果服务器不能连接上，就不能提交，还原，对比等等。 
3、 不适合开源开发（开发人数非常非常多，但是Google app engine就是用svn的）。但是一般集中式管理的有非常明确的权限管理机制（例如分支访问限制），可以实现分层管理，从而很好的解决开发人数众多的问题。

### （2）Git优缺点
优点： 
1、适合分布式开发，强调个体。 
2、公共服务器压力和数据量都不会太大。 
3、速度快、灵活。 
4、任意两个开发者之间可以很容易的解决冲突。 
5、离线工作。 
缺点： 
1、学习周期相对而言比较长。
2、不符合常规思维。 
3、代码保密性差，一旦开发者把整个库克隆下来就可以完全公开所有代码和版本信息。

## 3、设置用户名与邮箱（用户标识，必要）

当你安装Git后首先要做的事情是设置你的用户名称和e-mail地址。这是非常重要的，因为每次Git提交都会使用该信息。它被永远的嵌入到了你的提交中：
git config --global user.name "mingcheng"  #名称
git config --global user.email youxiang   #邮箱
只需要做一次这个设置，如果你传递了--global 选项，因为Git将总是会使用该信息来处理你在系统中所做的一切操作。如果你希望在一个特定的项目中使用不同的名称或e-mail地址，你可以在该项目中运行该命令而不要--global选项。总之--global为全局配置，不加为某个项目的特定配置。

## 4、创建SSH Key

第一步：在用户主目录（C:\Users\Administrator）下，看看有没有.ssh文件，如果有，再看文件下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接到下一步。如果没有，打开Git Bash，输入命令，创建SSH Key
ssh-keygen -t rsa -C "邮箱" //注册GitHub的邮箱
第二步：创建成功，再去用户主目录里找到.ssh文件夹，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露，id_rsa.pub是公钥，可以公开。
第三步：到GitHub上，打开“Account settings”--“SSH Keys”页面，然后点击“Add SSH Key”，填上Title，在Key文本框里粘贴 id_rsa.pub文件里的全部内容。点“Add Key”，你就应该看到已经添加的Key，可以添加多个Key
第四步：验证是否成功，在git bash里输入下面的命令ssh -T git@github.com，如果初次设置的话，会出现如下界面，输入yes 同意即可。

## 5、上传自己的文件到GitHub远程仓库上

第一步：cd进入你放项目文件的地址，我的地址在D:\MYFILE\graduation\study\项目程序
第二步：输入git init，当前项目的目录中生成本地的git管理（会发现在当前目录下多了一个.git文件夹）
第三步：输入git add . ，将项目上所有的文件添加到仓库中的意思
第四步：输入git commit -m "first commit"，表示你对这次提交的注释 
第五步输入git remote add origin https://自己的仓库url地址（上面有说到） 将本地的仓库关联到github上，
如果想要修改先使用git remote rm origin 删除关联
最后一步，输入git push -u origin master，这是把代码上传到github仓库的意思。
Or git push origin master推送最新修改
执行完后，如果没有异常，会等待几秒，然后跳出一个让你输入Username和Password 的窗口，你只要输人github的登录账号和密码就行了。

注意：遇到git remote地址不对时，进行以下操作。
```javascript
//1、查看当前配置有哪些远程仓库
$ git remote 
origin
//2、执行时加上 -v 参数，你还可以看到每个别名的实际链接地址。
$ git remote -v
origin  ps://github.com/Intend-xie/Intend-xieblog (fetch)
origin  ps://github.com/Intend-xie/Intend-xieblog (push)
//3、修改地址
$ git remote set-url origin https://github.com/Intend-xie/Intend-xieblog.git
//4、再次查看
$ git remote -v
origin  https://github.com/Intend-xie/Intend-xieblog.git (fetch)
origin  https://github.com/Intend-xie/Intend-xieblog.git (push)
```

## 6、Git和hexo的连接

第一步：每个git账号都可以有一个用于展示个人博客的静态网站，且仓库名固定，如s <git_username>.github.io，创建一个远程仓库
第二步：仓库创建完成后，得到仓库地址URL，修改配置文件 /_config.yml 相关的配置。
```javascript
deploy:
type: git
    repo: <repository_url>  # git远程仓库地址
    branch: <branch_name>  # 分支名，一般是master
```
第三步：将工程推到git上，输入命令hexo clean清除缓存，hexo deploy进行部署，执行hexo的deploy部署命令推到git上时，目录结构跟本地工程的不同，也就是编译过。，
第四步：为了便于维护，可以再建一个git远程仓库，执行git命令把工程推上去，用来管理工程源代码。

## 7、运维必须要会用的 10 个 Git 命令

检查：
先了解一下如何检查改动痕迹。
git diff——查看所有本地文件的改动。只改动一个文件的话可以在命令后添加文件名。
git log——查看所有提交历史。还可用于带有 git log –p my_file 的文件，输入 q 退出。
git blame my file——了解谁在什么时候对 my_file 做了什么样的改动。
git reflog——显示本地代码库 HEAD 的更改日志。这个命令很适合查找丢失的工作。
用 Git 进行检查并不麻烦。相比之下，Git 中有不少删除和撤销提交以及文件改动的操作。

撤销：
可以用 git reset、git checkout 和 git revert 撤销在代码库中所做的改动，这些命令可能有点难理解。
git reset 和 git checkout 既可用于提交也可用于单个文件的修改，而 git revert 只能用在提交层面。如果你只需要处理尚未合并到协作远程工作的本地提交，你可以使用这三者中任何一条命令。如果是协同工作且需要撤销远程分支中的提交，那么就用 git revert。
这些命令中的每一条都有多个参数。以下是常见的用法：
git reset –-hard HEAD——撤销最近提交以来暂存区和非暂存区的改动。
指定不同的提交而不是 HEAD，以撤销自这条提交以来的更改。--hard 指的是撤销暂存区和非暂存区的更改。
要确保你撤销的不是协作伙伴所依赖的远程分支的提交。
git checkout my commit——从 my_commit 中撤销非暂存区的改动。
HEAD 常用在 my_commit，用来撤销最近一次提交以来在本地工作目录的改动。
checkout 最适合用于仅限于本地的撤销。它不会破坏你的协作伙伴所依赖的远程分支的提交历史。
如果你将 checkout 用在分支而不是提交上，HEAD 将会切换到指定分支，并更新成匹配的工作目录。这是 checkout 命令更常见的用法。
Git revert my commit——撤销 my_commit 中的更改。当用 revert 撤销改动时，它会产生新的提交。
对协作项目而言，revert 是很安全的，因为它不会覆盖其他用户分支可能依赖的历史记录。
有时候你只想删除本地目录中的未追踪文件。例如，也许你运行的代码在版本库中创建了许多你不需要的不同类型的文件。你可以一键清除它们！
Git clean –n——删除本地工作目录中的未追踪文件。
–n 表示试运行，在试运行中什么都不会删除。
-f 表示实际删除文件。
-d 表示删除未追踪的目录。
默认情况下不会删除 .gitignore 中的未追踪文件，但这种行为是可以更改的。
现在你已经知道了 Git 中用于撤销操作的命令，接下来我们再看两条可以有序排列文件的命令。

整理：
Git commit –amend——将暂存区的更改添加到最近一次提交中。
如果暂存区中什么都没有，你可以用该命令编辑最新的提交信息。只有在提交尚未整合到远程主分支中时才使用该命令！
Git push my remote –tags——将所有本地标记发送到远程版本库中。适用于版本变更。