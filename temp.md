# 建立git遠程倉庫，利用git clone进行共享

- 建立该项目的 git 目錄

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