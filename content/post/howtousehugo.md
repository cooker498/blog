---
title: "Hugo從安裝到部署"
date: 2018-04-10T22:09:49+08:00
draft: true
---

windows平臺安裝Hugo （翻譯自Hugo官方文檔）
-

1. 前往[hugo發行版](https://github.com/gohugoio/hugo/releases/ "Title")主頁。

2. ​最新的發行版公佈在頁面頂部，下拉到頁面底部查看下載列表，這些都是zip文件。

3. 在每一個版本的末尾找到windows文件，（因爲是更具字母表排序），根據你32位或64位的windows系統下載32位或64位的文件。

4. 將下載好的zip文件移動到你創建的任一盤符:Hugo\bin 文件下(如 `C:\Hugo\bin`)。

5. 雙擊zip文件將它解壓到前面創建的`Hugo\bin`目錄下，windows默認會解壓到當前目錄，除非你指定了其他的解壓目錄

6. 你現在應該有三個文件:hugo 的可執行文件（例如 `hugo_0.18_windows_amd64.exe`), `license.md`, 和 `readme.md`。（你現在可以刪除zip文件了。） 將hugo可執行文件(`hugo_0.18_windows_amd64.exe`)重命名為`hugo.exe`更易於使用。


   現在你需要將hugo加入你的windows PATH 設置中

使用Hugo創建站點（翻譯自Hugo官網）
-
* 在`c:\hugo\` 下新建sites文件夾
* 創建一個新站點

```bash
cd sites
hugo new site demo
```
* 配置主题

```bash
cd themes
git clone https://github.com/spf13/hyde.git
```

* 運行Hugo

```bash
cd ..
hugo server --theme=tyde --buildDrafts --watch
```
瀏覽器打開http://localhost:1313

部署Hugo到GitHub page
-
* 在你的GitHub創建一個倉庫，命名為`<你的github用戶名>.github.io`(如 `sss.github.io`)
* 在站點根目錄執行Hugo命令

```bash
cd c:\Hugo\site\demo
hugo -D --theme=hyde --baseUrl="http://sss.github.io/"
```
* 如果一切順利，在demo文件夾下會生成public目錄，將public目錄下的所有文件推送到剛創建的倉庫的master分支

```bash
cd public
git init
git remote add origin https://github.com/sss/sss.github.io.git
git add -A
git commit -m "first commit"
git push -u origin master
```
* 瀏覽器訪問http://sss.github.io/