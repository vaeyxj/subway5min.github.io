# Hugo

## 目录

- [1 初始化操作](#1-初始化操作)
- [2 发布文章](#2-发布文章)
- [3 自动化脚本发布](#3-自动化脚本发布)

> Hugo 是一个用 [Go](https://go.dev/ "Go") 编写的[静态站点生成器](https://en.wikipedia.org/wiki/Static_site_generator "静态站点生成器")，针对速度进行了优化，并专为灵活性而设计。凭借其先进的模板系统和快速的资源管道，Hugo 可以在几秒钟内渲染一个完整的站点，通常更短。

访问入口： [https://vaeyxj.github.io/subway5min.github.io/](https://vaeyxj.github.io/subway5min.github.io/ "https://vaeyxj.github.io/subway5min.github.io/") &#x20;

注意：上面地址在hugo.toml可配置：(baseURL = '[https://vaeyxj.github.io/subway5min.github.io/](https://vaeyxj.github.io/subway5min.github.io/ "https://vaeyxj.github.io/subway5min.github.io/")')

# 1 初始化操作

hugo逻辑是通过hugo脚本直接生成静态html资源，项目本身是一个生成服务，发布文章后，通过`hugo server -D`, 在public目录生成网站静态资源，只需要把public下面git init，来提交到github，然后通过github到pages配置github.io，来访问网站！

个人hugo生成服务仓库：[https://github.com/vaeyxj/subway5min/tree/master](https://github.com/vaeyxj/subway5min/tree/master "https://github.com/vaeyxj/subway5min/tree/master")
个人blog站点仓库：[https://github.com/vaeyxj/subway5min.github.io/tree/master](https://github.com/vaeyxj/subway5min.github.io/tree/master "https://github.com/vaeyxj/subway5min.github.io/tree/master")

mac安装：

> brew install hugo

创建新站点：

> hugo new site my-blog
> cd my-blog

添加主题：

主题统一放在themes目录下，配置主题生效，在`hugo.toml`配置文件更新`theme = "ananke"`

> git init
> git submodule add [https://github.com/theNewDynamic/gohugo-theme-ananke.git](https://github.com/theNewDynamic/gohugo-theme-ananke.git "https://github.com/theNewDynamic/gohugo-theme-ananke.git") themes/ananke

# 2 发布文章

1、新建一篇文章

> hugo new posts/my-first-post.md

2、本地调试&#x20;

地址：[http://localhost:1313/](http://localhost:1313/subway5min.github.io/ "http://localhost:1313/"){repo}

eg: [http://localhost:1313/subway5min.github.io/](http://localhost:1313/subway5min.github.io/ "http://localhost:1313/subway5min.github.io/")

> hugo server -D

草稿态文章也会被实时更新到public文件夹！

3、生成静态文件

注意草稿态文章不会发布，即draft=true会被忽略！

> hugo

4、部署

```java
cd public
git init
git add .
git commit -m "Initial commit"
git push 
```

# 3 自动化脚本发布

切到hugo生成服务目录下：

> `./zed_editor.sh 20250113`

```bash
#!/bin/bash

# 创建新文章
hugo new posts/$1.md

# 打开 Zed 编辑器编辑文件
zed content/posts/$1.md
```

> ./publish.sh 今日阳光明媚

```bash
#!/bin/bash

# 生成静态文件
hugo

# 发布到 GitHub Pages
cd public
git add .
git commit -m "Add new post: $1"
git push origin masterh
```
