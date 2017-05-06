# Learn Git
Git跟踪并管理的是修改，而非文件

## local
$ git config --global user.name "Your Name"

$ git config --global user.email "email@example.com"

> 注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

$ mkdir learngit
> 新建文件夹learngit,windows系统下最好各级目录不含中文

$ cd learngit
> 进入learngit文件夹

$ cd E:\othertime

$ pwd
> 显示当前目录

$git init
> 当前目录变成Git可以管理的仓库。如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls-ah命令就可以看见。

> 所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

> 不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的，如果要真正使用版本控制系统，就要以纯文本方式编写文件。

> 因为文本是有编码的，比如中文有常用的GBK编码，日文有Shift_JIS编码，如果没有历史遗留问题，强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。

> 使用Windows要特别注意：  千万不要使用Windows自带的记事本编辑任何文本文件。原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。建议你下载Notepad++代替记事本，不但功能强大，而且免费！记得把Notepad++的默认编码设置为UTF-8 without BOM即可.
    
## git add and commit
$ git add readme.txt
> 用命令git add告诉Git，把文件添加到暂存区stage。没有消息就是好消息。

$ git commit
> 告诉Git，把文件提交到仓库Repository

$ git commit -m "wrote a readme file"
> -m 本次提交的说明
    
$ git add file1.txt

$ git add file2.txt file3.txt

> add 可以多次使用

$ git commit -m "add 3 files."

$ git status
> 查看仓库当前的状态。

$ git diff
> 查看修改的前后对比
    
$ git log
    查看最近到最远的提交日志
$ git log --pretty=oneline
> 一行显示每次提交的日志
---

退出用q

---

$ git reset --hard commit_id

$ git reset --hard HEAD^
>    HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令。用git log可以查看提交历史，以便确定要回退到哪个版本。

$ git reflog
> 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
    
$ git checkout -- readme.txt
> 把readme.txt文件在工作区的修改全部撤销，

$ git reset HEAD readme.txt
> 若已经采用git add 加入到暂存区，则要使用git reset HEAD   file， 将文件从暂存区中撤回，然后使用git checkout -- file 来删除工作区的修改。
    
$ rm test.txt
> 删除文件，使得版本库和工作区不一样。

$ git checkout -- test.txt
> 如果删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版

$ rm -rf dir
> 删除dir文件夹

$ git rm test.txt 
    
$ git commit -m "remove test.txt"
> 确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit

## remote 远程
$ ssh-keygen -t rsa -C "youremail@example.com"
> 在用户主目录（C:\Users\Administrator）里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。在github网站输入id_rsa.pub中的内容，即可确认你的身份
    
### github 现在github上创建新的repository

$ git remote add origin git@github.com:michaelliao/learngit.git

> 远程仓库的默认名称是origin。michaelliao/learngit.git你自己的git账号下的repository
    
$ git push -u origin master
> 当前分支master推送到远程。由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

$ git push origin master

$ git remote
> 查看远程库的信息

$ git remote -v

### git clone
$ git clone git@github.com:michaelliao/gitskills.git
> git clone克隆一个本地库。GitHub给出的地址不止一个，还可以用https://github.com/michaelliao/gitskills.git这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议

## 分支
$ git branch
> 查看所有分支，当前分支前加*，即为当前工作目录

$ git branch <name>
> 创建分支<name>

$ git checkout <name>
> 切换到分支<name>,该分支为当前工作目录。
> $ git checkout master,切换回master分支

$ git checkout -b <name>
> 等于以上两条命令, branch and checkout

$ git merge <name>
> 合并指定分支<name>到当前分支

$ git branch -d <name>
> 合并完成后可以删除被合并分支

## conflict 当前分支和要合并的分支同时做出了修改
$ git merge <branch name>
> 在同时被修改的文档中显示了相冲突的部分，需要手动选择一个合适的修改。然后在$ git add readme.txt $ git commit -m "conflict fixed"

$ git log --graph --pretty=oneline --abbrev-commit
> 图像显示合并冲突的过程

$ git log --graph

$ git merge --no-ff -m "merge with no-ff" dev
> --no-ff表示禁用Fast forward.

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

### bug分支
$ git stash
> 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场

$ git stash pop
> 恢复的同时将stash删除

$ git stash apply 
> 恢复，stash内容不删除

$ git stash drop
> 删除stash内容

$ git stash list

### feature 分支
开发一个新feature，最好新建一个分支；

$ git branch -D <name>
> 强行删除未合并的分支

### 协作
1. master分支是主分支，因此要时刻与远程同步；

2. dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

3. bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

4. feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

$ git push origin <branch-name>
> 推送分支到远程

当多人同时向远程提交时，产生冲突。解决办法：先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送。

$ git pull

$ git checkout -b branch-name origin/branch-name
> 在本地创建和远程分支对应的分支，使用本地和远程分支的名称最好一致；

$ git branch --set-upstream branch-name origin/branch-name
> 建立本地分支和远程分支的关联

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

## tag标签

$ git tag <tag：v1.0>
> 新建一个标签，默认为HEAD，也可以指定一个commit id；

$ git tag v0.9 6224937
> 对commit id为6224937的commit，打上标签v0.9

$ git tag -a v0.1 -m "version 0.1 released" 3628164
> 创建带说明的标签，-a指定标签名v0.1,-m指定说明文字

$ git tag -s <tagname> -m "blablabla..."
> -s用私钥签名一个标签,签名采用PGP签名，因此，必须首先安装gpg（GnuPG），如果没有找到gpg，或者没有gpg密钥对，就会报错

$ git show v0.1
> 查看tag为v0.1的PGP签名信息；

$ git tag
> 查看所有标签。

$ git tag -d v0.1
> 删除标签v0.1。因为标签只存储在本地，不会自动推送到远程，所以打错的标签可以在本地安全删除。

$ git push origin <tagname>
> 标签<tagname>推送到远程

$ git push origin --tags
> 推送所有尚未同步的本地标签到远程

$ git tag -d v0.1

$ git push origin :refs/tags/v0.1
> 如果v0.1标签已经推送到远程了，则先删除本地标签，然后删除一个远程标签。

## 忽略特殊的文件
在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore