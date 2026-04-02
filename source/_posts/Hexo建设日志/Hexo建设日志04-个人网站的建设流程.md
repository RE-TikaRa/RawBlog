---
title: Hexo建设日志04-个人网站的建设流程
date: 2024-06-15 00:06:00
tags:
  - Hexo建设日志
categories:
  - Hexo建设日志
abbrlink: e5e9716c
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
excerpt: "这是文章摘要 This is the excerpt of the post"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2026-06-15 00:06:00
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---

## 前言
&emsp;&emsp;做了这么几次个人网站，总结一下基本流程，把踩到的坑也写一下，以后自己迁移网站应该会方便很多。据说可以配置到cloudfare，但是目前没有试过。用我的这个流程，除了时间成本和人力成本，不需要其他的，并且不需要备案，但是网站是在GitHub上，所以加载速度真就是随缘。<br>&emsp;&emsp; ***注：本教程全部基于windows10系统，若有差异，自行搜索解决！！！*** ~~小声：我亲友的话倒是可以QQ滴滴我~~

<!--more-->

---

## 准备
&emsp;&emsp;这里是把所有的用到的网站都列了一遍，都是基本需求，但是不一定要下载，比如Hexo走的是命令，就不用下载，所以下文如果需要某个官网，点这里就能打开。要下载的我会在后面标注。<br>&emsp;&emsp;1、[GitHub](https://github.com/)账户：需要自己创建。<br>&emsp;&emsp;2、[Hexo](https://hexo.io/zh-cn/index.html): Hexo是一个快速、简洁且高效的博客框架。可以避免自己写框架时的麻烦事<br>&emsp;&emsp;3、[Gitee](https://gitee.com/)：GitHub的国内镜像，但是吧，，如果说做个人网站，这个要上传身份证什么的，还有审核期，不推荐<br>&emsp;&emsp;4、[Git](https://git-scm.com/)：最重要的东西！我们之后所有的命令都要在这个上运行！要下载！类比的话，，CMD！我们之后所有的命令都要在Git上运行！注意的一点就是，这个上面不能用ctrl+C或者+V来复制粘贴，所以右键复制粘贴是明智的选择<br>&emsp;&emsp;5、[Node.js](https://nodejs.org/zh-cn/)：Hexo的运行环境，要下载！<br>&emsp;&emsp;6、[VScode](https://code.visualstudio.com/)：是一个文本编辑器，超级好用，有很多很多的插件，包括写文章时候的可以实时预览之类的，当然如果你用的管别的文本编辑器，像是exeryeditor，那么就用你喜欢的就好。<br>&emsp;&emsp;7、[SM图床](https://sm.ms/)：用来上传你的图片并且生成Markdown格式的链接，这样就不会在插入图片的时候占用本地或者Github的存储空间。并且这个东西没有审核，想上传啥就上传啥（意味深长），但是需要注册<br>&emsp;&emsp;8、[MarkDown语法教程](https://markdown.com.cn/)：MarkDown的中文网，里面提到了MarkDown语法要咋写，这个十分简单，常用的也就那几个<br><br>&emsp;&emsp;下载不方便的话，我将提供截止到写稿为止的最新版本的百度网盘下载方式。

---

## 基础本地博客构造
&emsp;&emsp;1、安装Git和Node.js<br>&emsp;&emsp;&ensp;&emsp;首先打开git官网，点击右边的 ***Download for Windows*** 
![image.png](https://s2.loli.net/2024/06/15/bF146zjmfpgAOkX.png)
&emsp;&emsp;打开如下界面后在 ***Standalone Installer*** 范围内选择自己的系统版本，比如我的是X64，就下载64位，如果不会，百度
![Clip_2024-06-15_00-55-07.png](https://s2.loli.net/2024/06/15/VewItCL42Xg9rKF.png)
&emsp;&emsp;下载完成后，双击安装，无脑下一步即可（如果自己会，并且有特殊需求，按自己情况来定）安装完成后，鼠标右键空白处出现下图两个选项，若出现图示选项，则证明安装成功
![Clip_2024-06-15_01-06-41.png](https://s2.loli.net/2024/06/15/kVnIUNhlYCS2Q8r.png)
&emsp;&emsp;打开Node.js官网，点击 ***Download Node.js (LTS)*** 
![Clip_2024-06-15_01-07-58.png](https://s2.loli.net/2024/06/15/WYERh4OqKifZ3nB.png)
&emsp;&emsp;依旧是无脑下一步即可（如果自己会，并且有特殊需求，按自己情况来定），期间这个建议选一下，但是如果自己知道这是在干什么，不选也可以
![image.png](https://s2.loli.net/2024/06/15/uXbcSFnkyGwtAVT.png)
&emsp;&emsp;然后cmd输入 ***node -v*** 查看是否安装成功，若出现版本号，则证明安装成功
![Clip_2024-06-15_01-17-20.png](https://s2.loli.net/2024/06/15/8dRFDBASiysZt3O.png)
&emsp;&emsp;2、安装Hexo：Hexo是一个快速、简洁且高效的博客框架。对中文支持比较友好<br>&emsp;&emsp;&ensp;&emsp;首先我们找到自己要新建一个网站的存放文件夹，然后在这个文件夹右键，选择 ***Git Bash Here*** 
![Clip_2024-06-15_01-20-37.png](https://s2.loli.net/2024/06/15/nH6EMa82kvQdFTG.png)
&emsp;&emsp;然后复制Hexo官网的第一行命令，输入到Git

    npm install hexo-cli -g

出现下一或者下二的代码都是成功，下一是提示你npm版本有点旧，要升级而已，图二是绝对正常

    removed 1 package,and changed 53 packages in 46s
    14 packages are looking for funding
    run"npm fund`for detai1s
    npm notice
    npm notice New minor version of npm available! 10.7.0 -> 10.8.1
    npm notice Changelog: https://github.com/npm/cli/releases/tag/v10.8.1npm notice To update run: npm insta11 -g npm@1o.8.1
    npm notice

![Clip_2024-06-15_01-28-57.png](https://s2.loli.net/2024/06/15/NjenXori7KPtlFp.png)
&emsp;&emsp;然后复制第二行命令输入Git

    hexo init blog
&emsp;&emsp;出现如下内容则表明成功（这个过程可能极其漫长，视电脑配置和网络情况而定，尤其是连接GitHub的网速）
![Clip_2024-06-15_01-38-10.png](https://s2.loli.net/2024/06/15/7WdQ9fopL8aF4GD.png)
&emsp;&emsp;然后你会发现你的文件夹下多了个blog文件夹
![Clip_2024-06-15_01-41-25.png](https://s2.loli.net/2024/06/15/rvUkPVNEZofBmDw.png)
&emsp;&emsp;复制第三行命令到git，其实也可以直接打开这个文件夹，再打开一遍 ***Git Bash Here*** ，效果一样，因为下面这个代码作用就是，进入blog这个文件夹

    cd blog

![Clip_2024-06-15_01-45-12.png](https://s2.loli.net/2024/06/15/RXtsWbz7AQum1dB.png)
&emsp;&emsp;然后运行第四行命令

    npm install

![Clip_2024-06-15_01-46-50.png](https://s2.loli.net/2024/06/15/C5fujMZwqzLTXm2.png)
&emsp;&emsp;这样博客的基本框架就构造完毕了，可以运行第五行命令来检验是否创建成功

    hexo s
    是hexo server的缩写，两个效果一样

![Clip_2024-06-15_01-50-02.png](https://s2.loli.net/2024/06/15/2YPL93vZTXauwke.png)
&emsp;&emsp;然后我们就可以将 http://localhost:4000/ 输入到浏览器，查看博客基本框架构造是否完成（切记不要用ctrl+c，当前场景中这个按键组合代表退出或者关闭当前服务），如下图
![Clip_2024-06-15_01-52-44.png](https://s2.loli.net/2024/06/15/WogblQ8KtUFdG5e.png)

---

## 博客美化
&emsp;&emsp;我们来让博客更好看一点，可以自己写css和json之类的美化，也可以下载现成的主题，这边我以下载主题这一方式来美化。<br>&emsp;&emsp;在Hexo主页面下有探索主题的按钮，或者打开网址：https://hexo.io/themes/ 。主题这边基本就是英文，并且切换简体中文没啥用，所以还是开个翻译器比较好，还有就是，这个页面加载异常缓慢，可以顺便开个加速器。<br>&emsp;&emsp;选一个自己合乎心意的的主题模板，我选择 ***[Fluid](https://github.com/fluid-dev/hexo-theme-fluid)*** 这一主题演示（因为我喜欢这种有大头图的）
![Clip_2024-06-15_02-03-24.png](https://s2.loli.net/2024/06/15/oEazbseqh2JdY6M.png)
&emsp;&emsp;首先打开他的GitHub项目页，往下翻翻，找到 ***快速开始*** 
![Clip_2024-06-15_02-05-13.png](https://s2.loli.net/2024/06/15/XH5ONnumvg9bsaJ.png)
&emsp;&emsp;接下来我以习惯性的方式进行演示（方式二，因为npm不咋会用的话容易出奇奇怪怪的BUG）<br>&emsp;&emsp;下载最新release版本，解压到 themes 目录，并将解压出的文件夹重命名为 fluid。这样你的blog文件夹下的theme文件夹下一个就会有一个fluid文件夹了，然后这个文件夹里面就是我们解压出来的各种文件，如下图
![Clip_2024-06-15_02-11-08.png](https://s2.loli.net/2024/06/15/9FegRvr4LqiCOnm.png)
&emsp;&emsp;然后我们回到blog文件夹下，找到 ***_config.yml*** 文件，打开它，找到 ***theme*** 这个字段，将值改为 fluid，如下图
![Clip_2024-06-15_02-13-27.png](https://s2.loli.net/2024/06/15/7dloTtwQEC5qHKf.png)
&emsp;&emsp;再找到 ***language*** ，将值定义为 ***zh-CN*** ，如下图
![Clip_2024-06-15_02-15-14.png](https://s2.loli.net/2024/06/15/2lLnfDOUpqYeoVz.png)
&emsp;&emsp;这样我们就完成了博客主题的更改，之后的博客名修改等等，参照下表即可（所有修改都是blog文件夹下的_config.yml文件，不要改主题下的_config.yml文件）
| 参数 | 描述 |
|---|---|
| title | 网站标题 |
| subtitle | 网站副标题 |
| description | 网站描述 |
| keywords | 网站的关键词。支持多个关键词。 |
| author | 您的名字 |
| language | 网站使用的语言。对于简体中文用户来说，使用不同的主题可能需要设置成不同的值，请参考你的主题的文档自行设置，常见的有 zh-Hans和 zh-CN。 |
| timezone | 网站时区。Hexo 默认使用您电脑的时区。请参考 时区列表 进行设置，如 America/New_York, Japan, 和 UTC 。一般的，对于中国大陆地区可以使用 Asia/Shanghai。 |

&emsp;&emsp;还有就是，如果用某个主题，那么建议多看看这个主题的配置文档，如我本次使用的[Fluid配置文档](https://hexo.fluid-dev.com/docs/guide/)，里面作者会要求你该咋用不该咋用。

---

## 编写文章和创建页面
&emsp;&emsp;在 ***blog文件夹*** 下运行 ***Git Bash Here*** ，输入下面的指令，你就可以在 ***source***文件夹下的 ***POST***文件夹里面看到你所创建的文章了。

    hexo new post "文章名"
&emsp;&emsp;此处举例

    hexo new post Hexo建设日志06-个人网站的建设流程
&emsp;&emsp;得到返回

    INFO  Validating config
    INFO  Created: H:\测试\blog\source\_posts\Hexo建设日志06-个人网站的建设流程.md

&emsp;&emsp;就表明创建成功，Hexo文章支持MarkDown语法，所以我们打开后要根据MarkDown语法来写文章，关于MarkDown语法的教程可以在上文准备处有提及。<br>&emsp;&emsp;在 ***blog文件夹*** 下运行 ***Git Bash Here*** ，输入下面的指令，你就可以在 ***source***文件夹下看到你所创建的页面的同名文件夹了。（如果是英文页面，建议全小写）

    hexo new page “页面名”
&emsp;&emsp;此处以创建一个about页面为例

    hexo new page about

创建成功后，编辑博客目录下 /source/about/index.md，添加 layout 属性。
修改后的文件示例如下：

    ---
    title: about
    layout: about
    ---

    随便写一点什么吧~
这样就成功创建了一个关于页，运行网站就能在最上面就能看到了。
![Clip_2024-06-15_02-49-02.png](https://s2.loli.net/2024/06/15/MVqfYQhAd4sokxD.png)
![Clip_2024-06-15_02-51-04.png](https://s2.loli.net/2024/06/15/ZpOAxcIM3fvz4rn.png)
&emsp;&emsp;创建页面时，Hexo 会自动创建一个文件夹，里面有一个 index.md 文件，这个文件就是页面的内容。<br>&emsp;&emsp;下面是一些Hexo在Git中的代码：

    基础：hexo 某一条命令

| 命令 | 作用 |
|---|---|
| clean | 删除生成的文件 |
| deploy | 部署网站 |
| generate | 生成静态网站 |
| help | 帮助 |
| new | +post+名称是生成文章<br>+page+名称是生成某个页面<br>+名称默认是生成文章 |
| server | 开始本地服务器 |
| version | 版本 |

---

## 将网站上传至GitHub并且创建GitHub Pages
&emsp;&emsp;首先，你需要注册一个GitHub账号，用户名慎重一点，因为这个会成为你的网址。在GitHub上创建一个仓库，名字叫 ***用户名.github.io*** ，比如我的就是 ***re-tikara.github.io*** 。~~（等我换个号来演示一下）~~
![Clip_2024-06-15_13-00-55.png](https://s2.loli.net/2024/06/15/2X5aHDJuOqpw1Zg.png)
&emsp;&emsp;然后在随便任何一个文件夹里面运行 ***Git Bush*** ，输入以下命令

    ssh-keygen -t rsa -C "你的github注册邮件地址"

&emsp;&emsp;然后点四下回车，出现类似如下则表示成功

    Generating public/private rsa key pair.
    Enter file in which to save the key (默认路径):
    Created directory '默认路径'.
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in 默认路径
    Your public key has been saved in 默认路径
    The key fingerprint is:
    SHA256: XXXXXX
    The key's randomart image is:
    +---[RSA 3072]----+
    |         . .   .+|
    |         .= o  oX|
    |         +=+.+.=X|
    |       .oo.=+.o=+|
    |        S o o+ oo|
    |         o .  oE+|
    |            . .B.|
    |           . .o+*|
    |            ..+o*|
    +----[SHA256]-----+

&emsp;&emsp;然后文本编辑器打开如下路径

    C:\Users\用户名\.ssh\id_rsa.pub

&emsp;&emsp;这个里面就是你的SSH密码，切记不要外露，全部复制之后，回到GitHub的设置界面
![20240706134521.png](https://s2.loli.net/2024/07/06/uVRzCkl5n2NFrjs.png)
&emsp;&emsp;点 ***NEW SSH Key***，打开如下界面，把该填的填进去
![20240706134950.png](https://s2.loli.net/2024/07/06/RSXmhyLwad2lo8z.png)
&emsp;&emsp;然后运行以下代码测试一下是否成功

    ssh -T git@github.com

&emsp;&emsp;回车，点“yes”，出现如下

    The authenticity of host 'github.com (20.205.243.166)' can't be established.
    XXXXX key fingerprint is SHA256:XXXXXXXXXXXXXXXXXXXXX
    This key is not known by any other names.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added 'github.com' (XXXXX) to the list of known hosts.
    Hi re-alpworld! You've successfully authenticated, but GitHub does not provide shell access.


&emsp;&emsp;这边基本的GitHub本地设置就好了，以后就可以本地直接推送到github，然后更改博客根目录下的 ***_config.yml***，把下面的项目按照类似的改一下

    # URL
    ## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
    url: http://re-alpworld.github.io（这一项要改）
    permalink: :year/:month/:day/:title/
    permalink_defaults:
    pretty_urls:
    trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
    trailing_html: true # Set to false to remove trailing '.html' from permalinks
    # Deployment
    ----------------------------------------------------------------------------------
    ## Docs: https://hexo.io/docs/one-command-deployment
    deploy:
    type: git
    repo: git@github.com:name/name.github.io
    branch: main
    message: blog file
    （这一块建议直接复制替换，然后把地址改一下）

&emsp;&emsp;接下来开启github的个人page
![image.png](https://s2.loli.net/2024/07/06/aA9pTrH46GqFRyY.png)
&emsp;&emsp;最后把本地文件推送上去即可，在根目录地下运行***Git Bush*** ，输入以下命令

    hexo d

&emsp;&emsp;这样就完成了在线推送，输入 ***用户名.github.io*** 就可以看到了
