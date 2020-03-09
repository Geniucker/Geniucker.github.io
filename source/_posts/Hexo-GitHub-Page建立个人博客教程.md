---
title: Hexo+GitHub Page建立个人博客教程
categories:
  - 教程
tags:
  - 建站
date: 2020-03-06 21:21:36
updated:
---



# 安装 Git
Git是目前世界上最先进的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。也就是用来管理你的hexo博客文章，上传到GitHub的工具。  
+ Windows：下载并安装[Git](https://git-scm.com/download/win)
+ Linux (Ubuntu, Debian)：执行 `sudo apt-get install git-core`
+ Linux (Fedora, Red Hat, CentOS)：执行 `sudo yum install git-core`

<!---more--->{%note success%} <font size=5>**Windows 用户**</font>
对于中国大陆地区用户，可以前往 [淘宝 Git for Windows 镜像](https://npm.taobao.org/mirrors/git-for-windows/) 下载Git安装包{%endnote%}




# 安装 Node.js
Node.js 为大多数平台提供了官方的 [安装程序](https://nodejs.org/en/download/)。对于中国大陆地区用户，可以前往 [淘宝 Node.js 镜像](https://npm.taobao.org/mirrors/node) 下载。
{%note primary%} <font size=5>**Windows 用户**</font>
使用 Node.js 官方安装程序时，请确保勾选 **Add to PATH** 选项（默认已勾选）{%endnote%}
{%note danger%} <font size=5>**For Mac / Linux 用户**</font>
如果在尝试安装 Hexo 的过程中出现 `EACCES` 权限错误，请遵循 [由 npmjs 发布的指导](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) 修复该问题。强烈建议 **不要** 使用 root、sudo 等方法覆盖权限{%endnote%}


# 安装 Hexo
所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。
在控制台内执行`npm install -g hexo-cli`
安装以后，可以使用以下两种方式执行 Hexo：
1.`npx hexo <command>`
2.将 Hexo 所在的目录下的 `node_modules` 添加到环境变量之中即可直接使用 `hexo <command>`：

	echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
<br>

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件（\<folder>为你要放博客的详细路径）

	hexo init <folder>
	cd /d <folder>
	npm install
新建完成后，指定文件夹下有：
+ `node_modules`：依赖文件夹
+ `public`：存放生成的静态文件
+ `scaffolds`：模板
+ `source`：存放文章、草稿及手动创建的页面
+ `themes`：存放主题
+ `_config.yml`：Hexo配置文件



# GitHub 创建个人仓库
登录到GitHub,如果没有GitHub帐号，使用你的邮箱注册GitHub帐号 [点击注册](https://github.com/join)，点击GitHub中的New repository创建新仓库，仓库名应该为：`用户名`.github.io 这个`用户名`使用你的GitHub帐号名称代替，这是固定写法，比如我的仓库名称为 geniucker.github.io


# 配置 Git
## 设置user.name和user.email配置信息
在任意目录右键打开 Git Bash ，设置user.name和user.email配置信息：

    git config --global user.name <user_name>
    git config --global user.email <user_email>
`<user_name>`和`<user_email>`分别为你的GitHub注册名和注册邮箱  
## 生成 SSH Key 并完成连接
首先检查本地是否有ssh key 

    ls -al ~/.ssh
如果终端输出的是：

    No such file or directory
说明没有创建过SSH Key，创建SSH Key：

    ssh-keygen -t rsa -C <你的邮箱>
替换上自己的邮箱，接着都按<kbd>Enter</kbd>确认即可
接着打开用户名目录下的.ssh文件夹（若是不清楚什么事用户目录可以把 `%USERPROFILE%\.ssh` 复制到计算机的地址栏里）中的id_rsa.pub中的内容全部复制（可用记事本等打开）  
  
打开并登录GitHub，进入设置（点击角的头像，进入Settings），点击 `SSH and GPG keys` ，点击 `New SSH key` ，把刚才复制的内容粘贴到 Key 的文本框内，Title 随便填，点击 `Add SSH key` 完成添加。  
会到 Git Bash，输入 `ssh git@github.com` <kbd>Enter</kbd>，若得到

    The authenticity of host 'github.com (13.250.177.223)' can't be established.
    RSA key fingerprint is   SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.
    Are you sure you want to continue connecting (yes/no)? 
输入yes，<kbd>Enter</kbd>

    Warning: Permanently added 'github.com,13.250.177.223' (RSA) to the list of known hosts.
    Hi <user_name>! You've successfully authenticated, but GitHub does not provide shell access.
连接成功




# 配置
可以在 `_config.yml` 中修改大部分的配置，这里只列举常用的
## 网站
| 参数 | 描述 |
| --- | --- |
| `title` | 网站标题 |
| `subtitle` | 网站副标题 |
| `description` | 网站描述（主要用于SEO，告诉搜索引擎一个关于您站点的简单描述，通常建议在其中包含您网站的关键词） |
| `keywords` | 网站的关键词。使用半角逗号 `,` 分隔多个关键词。 |
| `author` | 您的名字（用于主题显示文章的作者） |
| `language` | 网站使用的语言 |
| `timezone` | 网站时区。Hexo 默认使用您电脑的时区。请参考 [时区列表](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) 进行设置，如 `America/New_York`, `Japan`, 和 `UTC` 。一般的，对于中国大陆地区可以使用 `Asia/Shanghai`。 |

## 网址
| 参数 | 描述 |默认值|
| --- | --- |---|
| `url` | 网址 |  |
| `root` | 网站根目录 |  |
| `permalink` | 文章的 [永久链接](https://hexo.io/zh-cn/docs/permalinks) 格式 | `:year/:month/:day/:title/` |
| `pretty_urls.trailing_index` | 是否在永久链接中保留尾部的 `index.html`，设置为 `false` 时去除 | `true` |
| `pretty_urls.trailing_html` | 是否在永久链接中保留尾部的 `.html`, 设置为 `false` 时去除 (*对尾部的 `index.html`无效*) | `true` |

{%note info%} <font size=5>**网站存放在子目录**</font>
如果您的网站存放在子目录中，例如 `http://yoursite.com/blog`，则请将您的 `url` 设为 `http://yoursite.com/blog` 并把 `root` 设为 `/blog/`{%endnote%}

    # 比如，一个页面的永久链接是 http://example.com/foo/bar/index.html
    pretty_urls:
      trailing_index: false
    # 此时页面的永久链接会变为 http://example.com/foo/bar/
## 分页
| 参数 | 描述 | 默认值 |
| --- | --- | --- |
| `per_page` | 每页显示的文章量 (0 = 关闭分页功能) | `10` |


## 扩展
| 参数 | 描述 |
| --- | --- |
| `theme` | 当前主题名称。值为`false`时禁用主题 |
| `deploy` | 部署部分的设置 |
>由于使用 GitHub Page，`deploy`部分改为
>```
deploy:
  type: git
  repository: git@github.com:<username>/<username>.github.io.git
  branch: master
>```
><username>替换为GitHub用户名

# 安装 git-deploy 插件
因为要通过 Git 将Hexo部署到GitHub，所以要用到 git-deploy

    cd <folder>
    npm install hexo-deployer-git --save
\<folder>为Hexo所在文件夹的详细目录


# 调试 Hexo
{%note danger%}执行任何 Hexo 的命令都要cd到博客所在文件夹，为了避免麻烦，我的做法是在博客根目录下建立一个bat文件，内容改为cmd，要执行命令只要打开它而不用cd <folder>{%endnote%}
`hexo server` 或 `hexo s`  在本地运行网站，当得到

    INFO  Start processing
    INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
可在浏览器打开localhost:4000访问你的博客，用完只要按<kbd>Ctrl</kbd>+<kbd>C</kbd>或直接关闭控制台窗口
<br>

`hexo clean` 清除缓存文件 (db.json) 和已生成的静态文件 (public)。在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。
<br>

`hexo generate` 或 `hexo g` 生成静态文件，后面可跟` -d`、` -f` 等参数
如： 
>`hexo g -f`强制重新生成静态文件，效果相当于`hexo clean` && `hexo g`
>`hexo g -d`生成静态文件后立即部署网站，效果相当于`hexo clean` && `hexo g`

<br>

`hexo deploy` 或 `hexo d` 部署网站，可跟参数 ` -g`部署之前先生成静态文件



# 绑定个人域名
1.为域名设置指向 \<yourname>.github.io 的记录
![picture](https://i.loli.net/2020/03/06/PN6DxtE5elfSkBy.jpg) ![picture](https://i.loli.net/2020/03/06/iUAz62XV4SBrKmI.jpg)
2.在网站根目录的source文件夹中建立文件`CNAME`（全大写，无拓展名），文件的内容为你要绑定域名（不是\<yourname>.github.io）
3.打开项目的设置页 github.com/\<yourname>/<\yourname>.github.io/settings（\<yourname>换乘GitHub用户名）定位到下图所示处： ![picture](https://i.loli.net/2020/03/06/WSEFZowDx182Itr.jpg)在Custom domain的编辑框内填上要绑定的域名
建议在 "Enforce HTTPS" 前的复选框上打勾，若无法打勾可能正在申请证书，过一段时间再试
4.正常部署网站，即可通过自己域名访问博客
**P.S.域名解析生效可能需要一定时间，不一定马上就能通过自己的域名访问**


# 其它
其它详细信息详见 [官方文档](https://hexo.io/zh-cn/docs/index.html)