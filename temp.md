本地git仓库的相关操作

想要进行git的相关操作，首先要建立一个git仓库，有两种方式可以建立git仓库，一个是新建，一个是克隆现有的git仓库：
    新建一个git仓库：  git init
    克隆现有的git仓库：  git clone [url] [目录名（如果木有，则建立一个和原仓库同名的目录）]
建立起来的git仓库都是在目录下多了一个.git目录，不同点是init的里边啥也木有，clone的是把目标git仓库复制过来了。

以下就开始git的相关操作了：
git status            查看文件的状态，是否暂存；
git add <file name>        将未暂存文件暂存；
git rm <file name>        删除文件；
git rm --cache <file name>    在git仓库中删除此文件的跟踪，但是不删除文件；
git reset HEAD <file name>    将暂存的文件拉回未暂存状态；
git checkout <file name>    取消未暂存状态的文件的修改，返回到暂存或者已经提交的状态；
git diff [<filename>]         查看未暂存文件的修改；
git diff --cache        查看已暂存状态的文件的修改；
git diff --staged        效果同上，在git1.6.1以上版本可用。

忽略某些文件
    我们总会有些文件不需要跟踪，比如使用eclipce开发android的时候的bin/，这些就需要我们忽略掉，方法如下：
        1.在./.git/info/exclude文件中添加需要忽略的名字；
        2.在.下新建一个名字为.gitignore的文件，把需要忽略的名字添加进去。

提交更新
    提交更新的命令是 git commit ，后边有些选项可以选择来节省某些步骤：
        -a             可以省略add 步骤；
        -m "commit message"     是添加提交的内容概述，可以省略直接使用git commit后打开文本编辑器来输入内容概述。

移动文件 
    移动文件的命令是 git mv file_from file_to,该命令相当于 mv fill_from fill_to    git rm file_from   git add file_to

撤销操作
    修改最后一次的提交，可以覆盖最后一次commit的内容，用于补充忘记提交的内容或者改动提交内容的概述，命令为 git commit --amend
    取消已经暂存的文件，将状态从已暂存拉回未暂存，git reset HEAD <file name>
    取消对文件的修改，只有未暂存状态才可以使用，git checkout <file name>
    
查看提交历史
    一个是用图形工具来查看:gitk ;另外就是代码查看:git log  ，会按照时间顺序列出所有的提交，有很多选项可以选择：
    -p        显示出所有的具体改动
    -n        显示最近的n条数据
    --stat        显示每次更新的增删改的具体数据
    等等，很多很多，不过感觉没啥用，就不一一写了，从来没用过，gitk用的最多，而且看起来清楚

远程仓库的相关使用
    查看远程仓库：git remote   ,另外，添加-v选项（verbose），可以显示对应的克隆地址；
    查看某个远程仓库的详细信息：git remote show [remote-name]
    添加远程仓库：git remote add [remote-name] [url]
    远程仓库的改名：git remote rename [old-name] [new-name]
    远程仓库的删除：git remote rm [remote-name]
    从远程仓库抓取数据：git fetch [remote-name]
    推送数据到远程仓库：git push [remote-name] [branch-name] 这里需要注意的是，如果只写了本地branch的名字，他会将本地的branch推送上去，如果remote上木有该branch，将会新建一个，如果想推送的remote的某个branch里边，需要写成 git push [remote-name] [local-branch-name]:[remote-branch-name]  这样就可以了，之前没理解清楚的时候没写远程仓库的branch名字，费了好多时间才弄明白，血的教训阿
    
标签
    查看现有的标签：git tag，按照字母顺序排列
    查看某些特定的标签：git tag -l '搜索条件'
    新建标签：git tag -a [tag-name]   ,可以添加-m选项来添加标签的附注，省略打开文本编辑器来写的步骤了；
    补充添加标签；有时忘记在每次commit后建立标签，只需要在新建标签中添加对应的commit的ssh-1码的前几位就可以了 git tag -a [tag-name] [ssh-1] 
    新建轻量级标签： git tag [tag-name] 
    查看标签对应的内容：git show [tag-name]
    分享标签：git push [remote-name] [tag-name]
    推送所有的标签：git push [remote-name] --tags
    


# 建立git遠程倉庫，利用git clone进行共享

- 建立该项目的 git 目錄。
例如，molnplus的其中一個項目是DR70，其路徑是：

    ~/phenomenon/

    mkdir repositoryname

    cd repositoryname

- 建立git倉庫

    git init

系统将會反饋：

    Initialized empty Git repository in /a certain path/"repositoryname"/.git/

- 添加項目初始文件， 一般是从其他路径拷贝过来，如果要新建的话：

    vim "filename".md

1. 跟蹤及提交到倉庫
    git add .
    git commit -m "a comment"

1. 在本地的git倉庫"添加一個遠程倉庫",當然這個遠程倉庫還是你自己的這個目錄。

    git remote add origin ssh://你的IP/~/testgit/.git

這時候,本地的 .git/config 應該會改變

1. 將本地的 master分支 ，跟蹤到遠程的分支

    git push origin master

1. 顯示遠程信息

    git remote show origin

1. 利用其他局域網的電腦測試你的倉庫

    git clone ssh://你的IP/home/～/testgit/.git

1. 大功告成，開始動手建立你的倉庫吧。

Ubuntu下測試ssh時使用ssh localhost 命令，出現錯誤提示connect to host localhost port 22:Connection refused

造成這個錯誤的原因可能是ssh-server未安裝或者未啓動。ubuntu 11.10 默認安裝openssh-client，但是木有安裝server

運行 ps -e | grep ssh，查看是否有sshd進程

如果沒有，說明server沒啓動，通過 /etc/init.d/ssh -start 啓動server進程，如果提示ssh不存在 那麼就是沒安裝server

通過 sudo apt-get install openssh-server命令安裝即可