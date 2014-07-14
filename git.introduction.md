<link href="/Users/wanghu/phenomenon/personlig/markdown/kevinburke.css" rel="stylesheet"></link>

# GIT

***
_我用git來進行文件版本管理。_

***
***

## Tutorial

設置是按照[github-simple-tutorial](http://wuyuans.com/2012/05/github-simple-tutorial/)和[git-github-usage](http://artori.us/git-github-usage/)來進行的。
主要有以下幾步：

### 註冊賬戶以及創建倉庫
### 在本地創建ssh key

    ssh-keygen -t rsa -C "huwung@gmail.com"
    
首次設置會提示是否continue，輸入yes，如果成功連上github會返回：

    You've successfully authenticated, but GitHub does not provide shell access

回到github的頁面上，進入Account Settings。
在該頁面的 **SSH Public Keys** 標籤中選擇 **Add another public key**。
**Title** 隨意，在 **Key** 中複製粘貼 **id_rsa.pub** 中的內容。
文本編輯器我用的是 **vim**。

使用以下命令測試連接

    ssh -v git@github.com

    
### 設置username和email
    
    git config --global user.name “huWANG”
    git config --global user.email "huwung@gmail.com"

### gitignore
.gitignore顧名思義就是告訴git需要忽略的文件。
一般我們寫完代碼後會執行編譯、調試等操作，這期間會產生很多中間文件和可執行文件，這些都不是代碼文件，是不需要git來管理的。

### tag


### 上传至Github

    git remote add origin git@github.com:huwung/something.git
    git push origin master
    
    