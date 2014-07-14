<link href="/Users/wanghu/phenomenon/personlig/markdown/kevinburke.css" rel="stylesheet"></link>

# LOCAL GIT REPOSITORY

***

***
***

建立git仓库：

    git init

添加项目初始文件、跟踪及提交到仓库：

    git add .    # 将添加该路径下的所有文件
    git commit -m “注释”

在本地的git仓库"添加一个远程仓库",当然这个远程仓库还是你自己的这个目录：

    git remote add origin ssh://192.168.1.115/~/testgit/.git

将本地的 master分支 ，跟踪到远程的分支

    git push origin master

显示远程信息

    git remote show origin

利用其他局域网的电脑测试你的仓库

    git clone ssh://192.168.1.115/home/～/testgit/.git

就是这样简单。
