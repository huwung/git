<link href="/Users/wanghu/phenomenon/personlig/markdown/kevinburke.css" rel="stylesheet"></link>

# Git
_版本控制是一種記錄若干文件內容變化，以便將來查閱特定版本修訂情況的系統。_
_實際上，你可以對任何類型的文件進行版本控制。_

- source: [git-scm](http://www.git-scm.com/blog)
- source: [think like a git](http://think-like-a-git.net)

***
***

## 為甚麼我要折騰這玩意兒
source: [git起步](http://blog.jobbole.com/25775/)

***

- 將某個文件回溯到之前的狀態，甚至將整個項目都回退到過去某個時間點的狀態。
- 比較文件的變化細節，查出最後是誰修改了哪個地方，從而導致出現怪異問題，又是誰在何時報告了某個功能缺陷等等。
_(想都不用想，一般都是我親自幹的)_
- 使用版本控制系統通常還意味著，就算你亂來一氣把整個項目中的文件改 的改刪的刪，你也照樣可以輕鬆恢復到原先的樣子。
- 完成以上的動作，額外增加的工作量卻微乎其微。

### 分布式版本控制系統(Distributed Version Control System, DVCS)
在這類系統中，像 Git，Mercurial，Bazaar 以及 Darcs 等，客戶端並不只提取最新版本的文件快照，而是把原始的代碼倉庫完整地鏡像下來。
這麼一來，任何一處協同工作用的服務器發生故障，事後都可以用任何一個鏡 像出來的本地倉庫恢復。
因為每一次的提取操作，實際上都是一次對代碼倉庫的完整備份

![figure](http://jbcdn2.b0.upaiyun.com/2012/08/Git-start3.png)

許多這類系統都可以指定和若干不同的遠端代碼倉庫進行交互。
籍此，你就可以在同一個項目中，分別和不同工作小組的人相互協作。
你可以根據需要設定不同的協作流程，比如層次模型式的工作流，而這在以前的集中式系統中是無法實現的。

## 基本操作

***

## 創建新倉庫

創建新文件夾，打開，然後執行 

    git init

就能創建一個新的 git 倉庫。

## 檢出倉庫

執行如下命令以創建一個本地倉庫的克隆版本：

    git clone /path/to/repository 

如果是遠端服務器上的倉庫，你的命令會是這個樣子：

    git clone username@host:/path/to/repository

## 添加和提交

你可以提出更改（把它們添加到暫存區），使用如下命令：

    git add <filename>
    git add *

這是 git 基本工作流程的第一步；使用如下命令以實際提交改動：

    git commit -m "代碼提交信息"

現在，你的改動已經提交到了 HEAD，但是還沒到你的遠端倉庫。

## 推送改動
你的改動現在已經在本地倉庫的 HEAD 中了。執行如下命令以將這些改動提交到遠端倉庫：

    git push origin master

可以把 master 換成你想要推送的任何分支。 
如果你還沒有克隆現有倉庫，並欲將你的倉庫連接到某個遠程服務器，你可以使用如下命令添加：

    git remote add origin <server>

如此你就能夠將你的改動推送到所添加的服務器上去了。

## 工作流
你的本地倉庫由 git 維護的三棵“樹”組成。
第一個是你的 _**工作目錄**_，它持有實際文件；
第二個是 **暫存區(Index)**，它像個緩存區域，臨時保存你的改動；
最後是 **HEAD**，它指向你最後一次提交的結果。

## 分支
分支是用來將特性開發絕緣開來的。
在你創建倉庫的時候，master 是“默認的”分支。
在其他分支上進行開發，完成後再將它們合併到主分支上。

創建一個叫做“feature_x”的分支，並切換過去：

    git checkout -b feature_x;

切換回主分支：

    git checkout master;

再把新建的分支刪掉：

    git branch -d feature_x;
    
除非你將分支推送到遠端倉庫，不然該分支就是不為他人所見的:

    git push origin <branch>;
    
## 更新與合併
要更新你的本地倉庫至最新改動，執行：

    git pull

以在你的工作目錄中 獲取（fetch） 並 合併（merge） 遠端的改動。
要合併其他分支到你的當前分支（例如 master），執行：

    git merge <branch>

在這兩種情況下，git 都會嘗試去自動合併改動。遺憾的是，這可能並非每次都成功，並可能出現衝突（conflicts）。
這時候就需要你修改這些文件來手動合併這些衝突（conflicts）。
改完之後，你需要執行如下命令以將它們標記為合併成功：

    git add <filename>

在合併改動之前，你可以使用如下命令預覽差異：

    git diff <source_branch> <target_branch>
    
## 標籤
為軟件發佈創建標籤是推薦的。這個概念早已存在，在 SVN 中也有。你可以執行如下命令創建一個叫做 1.0.0 的標籤：

    git tag 1.0.0 1b2e1d63ff

1b2e1d63ff 是你想要標記的提交 ID 的前 10 位字符。
可以使用下列命令獲取提交 ID：

    git log

你也可以使用少一點的提交 ID 前幾位，只要它的指向具有唯一性。

## 替換本地改動
假如你操作失誤（當然，這最好永遠不要發生），你可以使用如下命令替換掉本地改動：

    git checkout -- <filename>

此命令會使用 HEAD 中的最新內容替換掉你的工作目錄中的文件。
已添加到暫存區的改動以及新文件都不會受到影響。

假如你想丟棄你在本地的所有改動與提交，可以到服務器上獲取最新的版本歷史，並將你本地主分支指向它：

    git fetch origin
    git reset --hard origin/master

## 實用小貼士
內建的圖形化 git：

    gitk

彩色的 git 輸出：

    git config color.ui true

顯示歷史記錄時，每個提交的信息只顯示一行：

    git config format.pretty oneline

交互式添加文件到暫存區：

    git add -i
    