---
title: Hexo建设日志03-对于Error Spawn failed报错的修复（歪门邪道）
date: 2024-01-21 11:38:55
tags:
  - Hexo建设日志
categories:
  - Hexo建设日志
abbrlink: 39589
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
excerpt: "这是文章摘要 This is the excerpt of the post"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2026-01-21 11:38:55
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---
# 前言：
&emsp;&emsp;最近被Error:Spawn failed这个报错，折磨得一塌糊涂。试了试网上的，什么删除.deploy_git文件夹，什么改_config.yml里面的deploy:repo的git@github.com:，还有本地推送啥的，对我都没作用。试了试一个偏方。在这把方法分享一下。

<!--more-->

---

# 步骤：
&emsp;&emsp;首先，我们直接打开Git Bash，不要在任何一个文件夹下运行。打开应该是下图这个样子（ ***~*** 后面没有任何东西，或者是一个 ***/*** 但是后面也没有东西）（我是在win菜单下运行的，没有添加到win菜单的话，你可以在你安装Git的文件夹下找到这个Git Bash）
![image.png](https://s2.loli.net/2024/01/21/2MpTKdWPS1zC8lR.png)
![image.png](https://s2.loli.net/2024/01/21/wWRtYIMnuXsoejy.png)
&emsp;&emsp;输入以下内容

    cd ~/.ssh
    # 进入以下文件夹：C:\Users\user\.ssh

&emsp;&emsp;现在上面的info信息就是这样
![image.png](https://s2.loli.net/2024/01/21/2jKHUNEpcTFQy9I.png)
&emsp;&emsp;然后呢，，接下来我们要通过常用的来创建一个控制.ssh的config，然后我习惯就是用，[VSCode](https://code.visualstudio.com/Download)，但是呢，我习惯用的vscode的zip版本。直接使用Git启动的话我倒是不会。所以我是下图这样的创建config的。视频看上去有点卡的话，这边有百度网盘的链，可以通过百度网盘看看，或者挂梯子。[HexoMader05-01 百度网盘在线版](https://pan.baidu.com/s/184laBs0d5H2yMEK8xfl_GQ?pwd=48wq)）

<iframe id="spkj" src="https://www.acfun.cn/player/ac43642408" width="100%" frameborder="no" scrolling="no" allowfullscreen="allowfullscreen"><span data-mce-type="bookmark" style="display: inline-block; width: 0px; overflow: hidden; line-height: 0;" class="mce_SELRES_start"></span> <span data-mce-type="bookmark" style="display: inline-block; width: 0px; overflow: hidden; line-height: 0;" class="mce_SELRES_start"></span> </iframe> <script type="text/javascript"> document.getElementById("spkj").style.height=document.getElementById("spkj").scrollWidth*0.76+"px"; </script>

&emsp;&emsp;然后呢就会唤起我的vscode，打开这样的界面
![image.png](https://s2.loli.net/2024/01/21/FZjyOwUbfQKc4vo.png)
&emsp;&emsp;在里面输入

    Host github.com
    User git
    Hostname ssh.github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa
    Port 443
    
    Host gitlab.com
    Hostname altssh.gitlab.com
    User git
    Port 443
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa

&emsp;&emsp;保存，在GIT输入以下内容
    
    ssh -T git@github.com

&emsp;&emsp;如果出现以下内容，说明修改成功了，但是GitHub不提供服务。
    
    Hi 你的名字! You've successfully authenticated, but GitHub does not provide shell access.

&emsp;&emsp;如果出现有个需要填yes还是弄的地方，填yes。我填完忘记截图了，然后来解决GitHub does not provide shell access.这个问题。解决办法就是重新生成SSH秘钥。<br>&emsp;&emsp;首先在Git输入以下信息：
    
    ssh-keygen -t rsa -C “your_email.com”

&emsp;&emsp;然后，第一个按一下回车；第二个，输入y；第三个，回车；第四个，回车。
![image.png](https://s2.loli.net/2024/01/21/ZHyMiU1r4dueEGb.png)
&emsp;&emsp;然后在 ***.ssh*** 文件夹下的找到 ***id_rsa.pub*** 打开，把里面的文本全部复制到GitHub的SSH秘钥里面，步骤就是：
    
    登录github
    点击 setting
    点击SSH and GPG keys
    选择 new ssh key
    添加公钥
    完成

&emsp;&emsp;这样就可以正常推送了
