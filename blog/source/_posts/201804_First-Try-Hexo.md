---
title: 使用Hexo框架及佈署到Github
date: 2018-04-24 20:59:36
updated: 
tags: Hexo
categories: [框架, Hexo]

---

## 準備環境
- 順手的編譯工具 (如: Visual Studio Code)
- Node.js (https://nodejs.org/en/)
- git 
我幾乎都是用VS在編寫程式碼，指是前端寫起來比較輕鬆，我會改用比較輕量的Code
至於Node.js, 主要是使用npm比較方便，指示我對他還很不熟，就不多說了 "XD
git則可有可無，如果沒裝，稍後取得檔案的部分，就要從網站上下載，無法享受git的方便之處

## 安裝Hexo框架
1. VS Code中「新增資料夾至工作區」
2. 以Ctrl+`打開終端機，然後照著Hexo官方網站(https://hexo.io/zh-tw/) 的說明，分別輸入指令
    {% blockquote  %}
    npm install hexo-cli -g
    hexo init blog
    cd blog
    npm install
    hexo server
    {% endblockquote %}
3. 看到 "Hexo is running at http://localhost:4000/. Press Ctrl+C to stop" 這段時，就能壓著Ctrl點網址看看 "Hello World!"

到這邊應該不會遇到什麼大問題，不排除Hexo的建置有改指令，最好第一次建構時要去官網確認。
Hexo預設的測試路徑為 http://localhost:4000/ ，如有改過Hexo的設置，網址可能會不同。
要特別注意的是，接下來的操作，都是在blog這資料夾中執行，如關掉編譯器再開啟時發現指令無法生效，記得檢查有沒有cd到正確路徑

## 套用主題(theme)
除了自己切版外，Hexo有許多他人提供的theme (https://hexo.io/themes/index.html)
我最後是選擇 indigo(https://github.com/yscoder/hexo-theme-indigo), 主因是它有RWD, 而且側邊欄能隨意收合
如果已裝了兩種(不含預設)以上的theme，以下操作請自行酌減。

參考theme的文件 https://github.com/yscoder/hexo-theme-indigo/wiki/%E5%AE%89%E8%A3%85
1. 下載主題包。在terminal執行
    {% blockquote  %}
    git clone https://github.com/yscoder/hexo-theme-indigo.git themes/indigo
    npm install hexo-renderer-less --save
    npm install hexo-generator-feed --save
    npm install hexo-generator-json-content --save
    npm install hexo-helper-qrcode --save
    {% endblockquote %}
2. 開啟標籤(tags)。在terminal執行
    {% blockquote  %}
    hexo new page tags
    {% endblockquote %}
3. 將上個指令所產生的檔案(/source/tags/index.md)加上
    {% blockquote %}
    layout: tags
    comments: false
    {% endblockquote %}
4. 分類(categories)功能。在terminal執行
    {% blockquote  %}
    hexo new page categories
    {% endblockquote %}
5. 將上個指令所產生的檔案(/source/categories/index.md)加上
    {% blockquote %}
    layout: categories
    comments: false
    {% endblockquote %}
6. 開啟_config.yml, 將 "theme: landscape" 改為 "theme: indigo" 
7. 在termial中輸入 "hexo server" 來啟動網頁

到這裡，就會看到網站文章雖然沒變，風格卻已經大改了。只是這版面仍有很多是原作者的設定，可參考原作提供的文件調整(https://github.com/yscoder/hexo-theme-indigo/wiki/%E9%85%8D%E7%BD%AE) ，接下來我只說明比較特別的部分

8. 停用「賞」。(類似+1或讚)
將 /blog/themes/indigo/_config.yml 中
    {% blockquote %}
    title: 谢谢大爷~
    wechat: /img/wechat.jpg     #微信，关闭设为 false
    alipay: /img/alipay.jpg     #支付宝，关闭设为 false
    {% endblockquote %}
改為
    {% blockquote %}
    reward: false
    {% endblockquote %}

## 佈署到Github
路徑的部分，就看情況代換了。以我來說，是把git設定在某個Projects下的StartHexo
最外層的結構長這樣
    {% blockquote %}
    StartHexo/.git/
    StartHexo/blog/
    StartHexo/docs/
    {% endblockquote %}
而我在Github上有一個對應的Repo也叫做StartHexo，以下範例是在這前提下演示的
如果要改成別的，就記得取代 StartHexo 這字眼

1. 到 /blog/_config.yml 檔案中，設定URL和匯出資料夾(改下面三個屬性，我預計用 /docs 這subfolder)
    {% blockquote %}
    url: https://laroyeh.github.io/StartHexo
    root: /StartHexo/
    public_dir: ../docs
    {% endblockquote %}
2. 上傳到Github上 (這個應該不用說了? 我比較懶, 是用 Github Desktop操作) 
3. 到Github中的該Repo的設定(Setting)中，找到"GitHub Pages"，然後將 Source 選擇成有 "/docs folder" 這字眼的，然後Save(儲存)
4. 應該會看到一個網址，點下去檢查有沒有問題吧！ (正在看的Blog，就是這樣生出來的)

---
### 版本參考
- Visual Studio Code v1.19.3
- Node.js v8.9.4
- hexo: 3.7.1
- hexo-cli: 1.1.0
- git version 2.16.1.windows.1

### 參考資料: 
https://hexo.io/zh-tw/
https://hexo.io/zh-tw/docs/configuration.html
https://github.com/yscoder/hexo-theme-indigo
https://github.com/yscoder/hexo-theme-indigo/wiki