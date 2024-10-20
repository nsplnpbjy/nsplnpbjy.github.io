# 静态网站部署



以往我们在部署自己的网站，例如博客一类网站的时候，通常还需要部署一个服务器，用来运行后端服务和数据库，如果我们仅仅是需要做一个博客这种与后端交互比较少的网站，这会非常浪费钱。
于是，我们使用 [hugo](https://gohugo.io/ "hugo官方网站")这种工具以及 [Github Pages](https://github.com "github") 来进行一个免费的站点制作。

![配图](../philly-magic-garden.9c0b4415.jpg "配图")


**什么是hugo？**
hugo是一个使用go语言环境的网页生成器，简而言之，你的博客每更新一次文章，就用hugo来重新生成整个网站，再把它推送到服务器上就可以运行。
这样做的好处是，不用后端的一系列服务和数据库，省去了买服务器的钱，再加上github本身又让你免费host一个静态网站，那么你用hugo生成出来的网站也可以直接放上去不要钱，**赢麻了**这波属于是。

**怎么安装hugo？**
首先你要有go的环境，这一步无非就是去[golang](https://go.dev/ "golang")下载一下go，然后配置一下环境变量，这里就不细说了。

其次你要安装一个hugo，[点击这里](https://github.com/gohugoio/hugo/releases "hugo下载")下载hugo，hugo是一个单独的文件，比如在Windows下是**hugo.exe**，这里建议下载**extended**版本的，可以避免一些后续问题。

现在要设置环境变量，比如我的hugo.exe在D:\hugo_extended_0.136.2_windows-amd64里，那么我就去编辑系统变量的Path，把这个D:\hugo_extended_0.136.2_windows-amd64地址加入进去，然后你使用powershell就可以运行hugo命令了。

尝试运行`hugo version`，如果跳出版本号，就说明hugo安装成功。

**创建一个网站**

这里我们用powershell进入一个文件夹，然后运行`hugo new site quickstart`，你就能得到一个名为quickstart的网站的框架结构。
自动创建的文件里，**hugo.toml**是非常重要的配置文件，它的配置通常取决于你的**主题**选择。
自动创建的**content**文件夹就是你以后发布文章的地方
别忘了在你的网站目录下运行`git init`来初始化git

**下载一个主题**

我们去github搜索一个主题，你可以搜索关键字类似于**hugo theme**，来寻找主题，这里我们使用[hugo-coder](https://github.com/luizdepra/hugo-coder "coder")这个主题。
使用
`git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder`
来下载这个主题，这个命令会把主题下载到**themes/hugo-coder**里面。
现在我们要修改**hugo.toml**文件来把这个主题使用起来。
我们有[主题作者给的示例](https://github.com/luizdepra/hugo-coder/blob/main/exampleSite/hugo.toml "示例")

**根据主题作者给的指示来修改hugo.toml文件是一个难点，非常重要**

这里，你可以根据自己的需求来更改配置，比如我们修改
~~~toml
//修改前
[[params.social]]
name = "Medium"
icon = "fa-brands fa-medium fa-2x"
weight = 5
url = "https://medium.com/@johndoe"

//修改后
[[params.social]]
name = "微博"
icon = "fa-brands fa-weibo fa-2x"
weight = 5 //序号
url = "你的微博链接"
~~~
就加上了你的社交媒体
接下来我们关注
~~~toml
[[languages.pt-br.menu.main]]
name = "Projetos"  //菜单名
weight = 3  //序号
url = "projects/" //content文件夹下装文章的文件夹
~~~

**创建文章**
我们使用`hugo new content content/posts/my-first-post.md`来创建一个新文章，这篇文章在posts下面，所以会被
~~~toml
[[languages.pt-br.menu.main]]
name = "Blog"
weight = 2
url = "posts/"
~~~
的菜单来使用到，文章会自动生成一些参数，比如：
~~~md
+++
date = '2024-10-19T13:37:19+08:00'
draft = false
title = '联系方式'
+++
~~~
这里面的draft是草稿的意思，如果true，那么在后续的一些命令中这篇文章不会被使用到。

**生成网站**
我们写好文章之后，使用`hugo build`来把网站生成出来。
我们会得到一个**public**文件夹
这个文件夹就是传统的Web 应用服务器类似于tomcat引擎用到的部署文件。

**部署网站**
首先去github创建一个仓库，这个仓库必须被命名为**你的ID.github.io**，否则我的评价是不行。
比如我的叫做**nsplnpbjy.github.io**
进入刚刚生成的**public**文件夹，初始化一下**git**，然后push到**你的ID.github.io**仓库。
**然后等一下**
**要等两分钟左右**
打开**https://你的ID.github.io/**，比如我的**https://nsplnpbjy.github.io/**，就是你的网站了。

**难点：找到合适的主题，并按照主题作者的指引文件配置好hugo.toml**

