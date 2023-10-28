+++
title = 'Github Pages With Hugo'
date = 2023-10-28T14:36:53+08:00
description = "本文记录了hugo + github pages搭建静态博客的步骤。"
+++

# 搭建个人静态博客网站

## Hugo + GITHUB PAGES

Hugo: Hugo是一个用 Go 语言编写的静态网站生成器。它将MARKDOWN文件渲染成网页。

GITHUB PAGES: github 提供的静态网站托管服务。

使用这两个工具，我们只需要这几点即可将博客对外托管。

1. 熟悉markdown
2. 学习hugo的使用
3. 熟悉git和github

同时，下面两个工具可以让个人编写博客的效率变高很多。

1. vscode: 用于编辑博客并对markdown进行实时渲染
2. chatgpt: 用于生成文案样板

当然，对于写博客来说，最重要的写，也就是我们写的markdown文档。

其他种种工具，只是为了让世界看见而已。

本文只会阐述怎么搭建静态博客，工具的使用不会提及太多。

## 搭建静态博客

`步骤一`：安装Hugo

参考 [hugo安装-中文](https://www.gohugo.org/) 安装hugo


`步骤二`：创建github仓库

正如 [关于github-pages](https://docs.github.com/zh/pages/getting-started-with-github-pages/about-github-pages) 中提到，用户站点必须以 `<username>.github.io` 为仓库名。

从浏览器的url上可以看到自己的用户名。

比如这个链接 `https://github.com/arc1024` 的用户名则是 `arc1024`，创建的仓库名应该是 `arc1024.github.io`。

`步骤三`：初始化网站

```shell
# 创建网站的目录
hugo new site arc1024.github.io
cd arc1024.github.io

# 跟踪远端仓库
git init
git remote add origin git@github.com:arc1024/arc1024.github.io.git
git branch -M main

# 随便添加一个主题
mkdir -p themes 
git submodule add git@github.com:zhaohuabing/hugo-theme-cleanwhite.git themes/hugo-theme-cleanwhite

# 推送代码到远端
git add .
git commit -am "add hugo-theme-cleanwhite"
git push -u origin main

# 添加 .gitignore
echo 'public' >> ./.gitignore
echo '.hugo_build.lock' >> ./.gitignore

# 推送代码到远端
git add .gitignore
git commit -m "add gitignore"
git push -u origin main

# 配置网站，修改hugo.toml
baseURL = 'https://arc1024.github.io/'
languageCode = 'en-us'
title = 'Arc1024'
theme = 'hugo-theme-cleanwhite'
[params]
  SEOTitle = "郑元湖的博客 | Zhengyuanhu Blog"
  description = "郑元湖, 后端程序员 | 这里是 郑元湖 的博客。"
  keyword = "郑元湖, Zhengyuanhu , 郑元湖的博客, Zhengyuanhu Blog, 博客, 个人网站, 互联网, Web, 云原生, IaaS, Kubernetes, 微服务, Microservice"
  slogan = "既来之，则安之。"

  [params.social]
  github = "https://github.com/arc1024"

  [[params.addtional_menus]]
  title =  "ABOUT"
  href =  "/about/"

# 写一篇博客
# 我们的markdown文件会生成在content目录下。
# 同时，我们需要注意post目录是cleanwhite主题渲染的主目录
hugo new /post/blob/github-pages-with-hugo.md

# 本地运行看下效果
hugo serve -D

# 去掉博客中的 draft = true 后编译，输出会在public目录下
hugo

# 初始化public
cd public
git init
git remote add origin git@github.com:arc1024/arc1024.github.io.git
git branch -M public
cd ..

# 推送public
hugo
cd public
git add .
git commit -am "publish post"
cd ..
```

`步骤四`：配置github page

打开下面连接`https://github.com/arc1024/arc1024.github.io/settings/pages`，选择public分支建立github pages，注意链接上的用户名和仓库需要改一下。

## 参考链接

1. [hugo quick-start](https://gohugo.io/getting-started/quick-start/)
2. [关于github-pages](https://docs.github.com/zh/pages/getting-started-with-github-pages/about-github-pages)
3. [cleanwhite主题](https://themes.gohugo.io/themes/hugo-theme-cleanwhite/)