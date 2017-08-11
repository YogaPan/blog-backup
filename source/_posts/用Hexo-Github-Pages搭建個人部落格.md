---
title: 用Hexo + Github Pages搭建個人部落格
date: 2017-08-11 20:27:17
tags:
  - hexo
  - blog
---

## 什麼是Hexo？
[Hexo](https://hexo.io/zh-tw/index.html)官方簡介：
> A fast, simple & powerful blog framework, powered by Node.js  
{% asset_img 01.png %}

Hexo的特色:
* 用Markdown語法寫blog
* 用Command Line來進行操作
* 140幾種網站主題可供選擇
* 多種插件，可以加入[disqus](https://disqus.com/)討論功能和瀏覽人數計數等功能
* 輕易部署到[Github Pages](https://pages.github.com)和[Heroku](https://www.heroku.com/)

<!--more-->

- - - -
## 安裝Hexo
Hexo是由[Node.js](https://nodejs.org/en/)寫成的，所以可以透過Node.js的套件管理工具[npm](https://www.npmjs.com/)或者[yarn](https://yarnpkg.com/en/)來安裝。我個人是使用Yarn來作為我的Node套件管理工具。如果電腦裡面還沒有安裝yarn可以過以下指令安裝：

Mac使用者透過[Homebrew](https://brew.sh)安裝
```sh
$ brew install yarn
```

Windows使用者透過[Chocolatey](https://chocolatey.org)安裝
```sh
$ choco install yarn
```

接著安裝Hexo:
```sh
$ yarn global add hexo
```

創建我的部落格
```sh
$ hexo init blog
```

啟動local端server
```sh
$ cd blog
$ hexo server
```

接著在你的瀏覽器裡輸入localhost:4000，就可以看到你的部落格啦！
{% asset_img 02.png %}



- - - -
## 目錄結構
再繼續往下看以前，我們先來暸解整個目錄結構:
```sh
blog/
  _config.yml.           -> 最主要的設定檔
  package.json.          -> 相依套件列表
  node_modules/          -> 相依套件
  public/                -> 生成的靜態網站資源
  source/
    _posts               -> 你寫的文章都放在這裡面
      hello-world.md     -> 文章
  themes/                -> 網站主題都放裡面
    landscape/
      _config.yml        -> 主題設定檔
  scaffolds/
    draft.md
    page.md
    post.md
```

### 設定檔
網站設定`_config.yml`，可設定：
* 作者名字、標題、描述
* 語系設定
* 是否產生assets資料夾
* 套用主題

主題設定`themes/<theme-name>/_config.yml`，可設定：
* 頭像
* 社群網路連結
* 新增頁面
* 其他客製化選項(scheme、高亮、動畫等等)

### 主題資料夾
`themes/`這個資料夾用來放置主題，目前裡面只有預設的landscape而已。

### 發文資料夾
`source/_posts`這個資料夾是真正會存放你文章的地方。裡面有一篇預設的Hello World。

- - - -
## 更換主題
### NexT
Hexo預設的主題是[landscape](https://github.com/hexojs/hexo-theme-landscape)，但是似乎有點....不夠帥氣，所以我們可以到這裡來挑選我們想要的主題： https://hexo.io/themes/

在精挑細選後，我決定使用[NexT](http://theme-next.iissnan.com)這個主題，因為：
* 介面美觀
* 官方文件詳細
* 可自定性高(多種scheme和code highlight)
* 支援多種語言
* Github上星星數多達9000顆，跟風一起用準沒錯
{% asset_img 03.png %}

用Git安裝NexT
```sh
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```

接著修改網站設定`_config.yml`
```yml
theme: next
```

重新啟動server
```sh
$ hexo server
```

{% asset_img 04.png %}
{% asset_img 05.png %}
哇！！整個高端大氣上檔次！

### 語言設定
在`_config.yml`中找到language欄位，設定為zh-tw
```yml
language: zh-tw
```
這樣就支援繁體中文了！

### Scheme設定
NexT提供多種Scheme選擇，其中Muse是預設的主題。而我個人是選擇使用Pisces當做我的主題。

在主題設定`theme/next/_config.yml`裡找到schema設定，把注釋去掉即可開啟。
```yml
#scheme: Muse
#scheme: Mist
scheme: Pisces
#scheme: Gemini
```

Muse:
{% asset_img 06.png %}

Mist:
{% asset_img 07.png %}


Pisces:
{% asset_img 08.png %}

Gemini:
{% asset_img 09.png %}

### 代碼高亮
官方說明
> NexT 使用 Tomorrow Theme 作为代码高亮，共有5款主题供你选择。 NexT 默认使用的是 白色的 normal 主题，可选的值有 normal，night， night blue， night bright， night eighties  
```yml
highlight_theme: normal
```

{% asset_img 10.png %}


### 動畫效果
在主題設定`themes/next/_config.yml`裡選擇要開啟的動畫效果，要打開就把值設定成true
```yml
# Canvas-nest
canvas_nest: true

# three_waves
three_waves: false

# canvas_lines
canvas_lines: false

# canvas_sphere
canvas_sphere: false

# Only fit scheme Pisces
# Canvas-ribbon
canvas_ribbon: false
```

我通常會開啟canvas_nest這個背景動畫效果，帶有微微的科技中二感，很對我的口味。
{% asset_img 11.png %}

- - - -
## 關於作者
主題都換好了，那我們的頭像和作者介紹呢？

### 頭像
先新增一個資料夾，用來存放大頭照
```sh
$ mkdir source/uploads
```

然後把你的大頭照丟進`source/uploads/`這個資料夾裡，然後在**主題設定**`themes/next/_config.yml`中設定大頭照路徑:
```yml
avatar: /uploads/avatar.jpg
```

### 作者
在**網站設定**`_config.yml`中設定名字、標題和副標題
```yml
title: <標題>
subtitle: <副標題>
description: <描述>
author: <你的名字>
```

### 開啟社群帳號連結
在**主題設定**`themes/next/_config.yml`中新增社群網路連結。
```yml
# Social links
social:
  GitHub: https://github.com/your-user-name
  Twitter: https://twitter.com/your-user-name
```

### About Me Page
新建一個about頁面
```sh
$ hexo new page "about"
```

在`themes/next/_config.yml`將about前面的註解去掉
```yml
menu:
  home: /
  archives: /archives
  tags: /tags
  about: /about
```

編輯`source/about/index.md`
```md
---
title: 關於我
date: 2017-08-10 13:23:37
---

# 哈囉
我是小蛇蛇我好可愛 >///<
```

成果:
{% asset_img 12.png %}
{% asset_img 13.png %}

Ok，到這裡關於自己的一切都設定好了，接下來要發表第一篇文章囉！

- - - -
## 我的第一篇文章
### 設定
所有的文章都會在`source/_posts`裡面。其實一開始裡面就已經有一篇範例文章`hello-world.md`了。

在發表文章以前，先進行一個簡單的設定，在網站設定`_config.yml`中:
```yml
post_asset_folder: true
```
這樣每當新增一篇文章時，會自動在`source/_posts/`裡新增一個跟文章同名的資料夾用來放置圖片資源。

### 新增文章
創造一篇名叫”測試”的文章
```sh
$ hexo new post 測試
```

編輯`source/_posts/test.md`
```md
---
title: 測試
date: 2017-08-11 19:46:32
tags:
---

測試發文～～～
```

### 嵌入圖片
圖片遷入的格式
```md
{% asset_img [image-name] %}
{% asset_img [image-name] [title] %}
```

例如說有一個圖片`snake.jpg`

要引用在文章裡只要先把`snake.jpg`丟到`source/_posts/測試/` 裡，然後在`source/_posts/測試.md` 裡
```md
---
title: 測試
date: 2017-08-10 13:23:37
tags:
---

測試發文～～～
{% asset_img snake.jpg %}
```

就可以看到圖片了
{% asset_img 14.png %}

- - - -
## Tags分類
文章可以透過標籤來進行分類

新建一個頁面，叫做`tags`
```sh
$ hexo new page "tags"
```

編輯剛新建的頁面`source/_posts/tags/index.md`，將頁面的type設為”tags”。
```md
---
title: All tags
date: 2017-08-10 13:23:37
type: "tags"
---
```

為剛剛那篇文章加入標籤
```md
---
title: 測試
date: 2017-08-10 13:23:37
tags: test
---
```

當一篇文章有多個Tags時
```md
tags:
  - Tag1
  - Tag2
  - Tag3
```

登登！文章現在可以透過標籤分類了
{% asset_img 15.png %}
{% asset_img 16.png %}

- - - -
## 文章搜索
很酷的是，Hexo還支援文章搜索的功能喔！

安裝套件
```sh
$ yarn add hexo-generator-search
```

在主題設置`theme/next/_config.yml`中找到local_search，並把enable設為true
```yml
# Local search
search
  local_search:
    enable: true
```

可以支援搜尋功能了！
{% asset_img 17.png %}

- - - -
## 部署到Github Pages
到這裡，只剩下最後一步，就是讓大家都能看到你的部落格！
有很多種部署的方式，在這裡我們選擇使用最簡單的[Github Page](https://pages.github.com/)。

Github Page的官方介紹
> Websites for you and your projects.  
> Hosted directly from your GitHub repository. Just edit, push, and your changes are live.  

先創建一個Github專案，名稱為`<username>.github.io`。例如說我的名字叫做yogapan，那我就創建一個`yogapan.github.io`的專案。
{% asset_img 18.png %}

安裝套件
```sh
$ yarn add hexo-deployer-git
```

修改**網站設定**`_config.yml`，找到deploy之後進行以下修改
```yml
deploy:
  type: git
  repo: https://github.com/<yourAccount>/<repo>
  branch: <your-branch>
```

Repo是你剛新建專案的網址
Branch則是指定分枝，通常是master

接著部署到Github Pages
```sh
$ hexo deploy
```

接下來就可以到你的網站`<username>.github.io`來看看囉！


關於部署更詳細的資料可以看這裡:
https://hexo.io/docs/deployment.html

- - - -
## 加入Disqus留言功能
https://github.com/iissnan/hexo-theme-next/wiki/%E8%AE%BE%E7%BD%AE%E5%A4%9A%E8%AF%B4-DISQUS

- - - -
## RSS訂閱
TODO

- - - -
## Hexo指令備忘錄
```sh
$ hexo init
$ hexo clean
$ hexo generate
$ hexo new post <title>
$ hexo new page tags
$ hexo server
$ hexo server -p 8000 --debug
$ hexo deploy
```

- - - -
## FAQ
Q: 為什麼我修改了設定之後，沒有反應出來呢？
A: 可以重啟server試試看，通常都可以解決問題。

Q: 為什麼部署到Github Page之後網站沒有更新呢
A: 部署到Github Pages上後可能會有延遲，有時要等個30秒左右才會更新。

- - - -
## 參考資料
### 連結:
Hexo
https://github.com/hexojs/hexo
https://hexo.io/zh-tw/index.html

Hexo Theme:
https://hexo.io/themes/

NexT:
http://theme-next.iissnan.com
https://github.com/iissnan/hexo-theme-next

Github Pages:
https://pages.github.com

Node.js
https://nodejs.org/en/

Npm and Yarn
https://www.npmjs.com/
https://yarnpkg.com/en/

Brew and Chocolatey
https://brew.sh
https://chocolatey.org

Disqus:
https://disqus.com/

### 其他不錯的主題
* [hexo-theme-icalm](https://github.com/nameoverflow/hexo-theme-icalm)
* [hexo-theme-one](https://github.com/EYHN/hexo-theme-one)
* [hexo-theme-huxblog](https://github.com/Kaijun/hexo-theme-huxblog)
* [hexo-theme-beantech](https://github.com/YenYuHsuan/hexo-theme-beantech)

### 同性質應用：
* [Hugo](http://gohugo.io/)
* [jekyll](https://jekyllrb.com/)
