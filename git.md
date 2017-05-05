Git跟踪并管理的是修改，而非文件

$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

    注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

$ mkdir learngit
	新建文件夹learngit,windows系统下最好各级目录不含中文
$ cd learngit
	进入learngit文件夹
$ cd E:\othertime
$ pwd
	显示当前目录

$git init
    当前目录变成Git可以管理的仓库。如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls-ah命令就可以看见。
    所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。
    不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的，如果要真正使用版本控制系统，就要以纯文本方式编写文件。

	因为文本是有编码的，比如中文有常用的GBK编码，日文有Shift_JIS编码，如果没有历史遗留问题，强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。

    使用Windows要特别注意：
    千万不要使用Windows自带的记事本编辑任何文本文件。原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。建议你下载Notepad++代替记事本，不但功能强大，而且免费！记得把Notepad++的默认编码设置为UTF-8 without BOM即可.
    
--git add and commit
$ git add readme.txt
    用命令git add告诉Git，把文件添加到暂存区stage。没有消息就是好消息。
$ git commit
    告诉Git，把文件提交到仓库Repository
$ git commit -m "wrote a readme file"
    -m 本次提交的说明
    
$ git add file1.txt
$ git add file2.txt file3.txt
    $ add 可以多次使用
$ git commit -m "add 3 files."

$ git status
    查看仓库当前的状态
    q退出显示的当前状态
$ git diff
    查看修改的前后对比
    
$ git log
    查看最近到最远的提交日志
$ git log --pretty=oneline
    一行显示每次提交的日志
退出用q

$ git reset --hard commit_id
$ git reset --hard HEAD^
    HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令。用git log可以查看提交历史，以便确定要回退到哪个版本。
$ git reflog
    要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
    
$ git checkout -- readme.txt
    把readme.txt文件在工作区的修改全部撤销，
$ git reset HEAD readme.txt
    若已经采用git add 加入到暂存区，则要使用git reset HEAD   file， 将文件从暂存区中撤回，然后使用git checkout -- file 来删除工作区的修改。
    
$ rm test.txt
    删除文件，使得版本库和工作区不一样。
$ git checkout -- test.txt
    如果删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版
$ rm -rf dir
    删除dir文件夹

$ git rm test.txt     
$ git commit -m "remove test.txt"
    确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit

--远程
$ ssh-keygen -t rsa -C "youremail@example.com"
    在用户主目录（C:\Users\Administrator）里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。在github网站输入id_rsa.pub中的内容，即可确认你的身份
    
--github 现在github上创建新的repository
$ git remote add origin git@github.com:michaelliao/learngit.git
    远程库的名字就是origin，这是Git默认的叫法。michaelliao/learngit.git你自己的git账号下的repository
$ git push -u origin master
    当前分支master推送到远程。由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
$ git push origin master

--git clone
$ git clone git@github.com:michaelliao/gitskills.git
    git clone克隆一个本地库。GitHub给出的地址不止一个，还可以用https://github.com/michaelliao/gitskills.git这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议

--分支
