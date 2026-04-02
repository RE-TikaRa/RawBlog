---
title: APK技术日常01—APK解包
date: 2024-01-07 22:43:22
tags:
  - APK
  - 技术日常
categories:
  - APK修改系列
abbrlink: 55002
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
sticky:
excerpt: "这是文章摘要 This is the excerpt of the post"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2026-01-07 22:43:22
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---

# 前言
***&emsp;&emsp;本教程全部基于 ***Windows10*** 系统下，不同系统下可能略有差异。教程中的文件都源自于网络开源，其STAFF列表会在文章末尾标注。本教程 ***不适用于游戏提取等用途*** ，教程中教学的是处理并修改APK文件以及查看相关文件等，如有侵权，请联系我删除。***
<!--more-->

---

# 所需工具
&emsp;&emsp;[APKTool](https://apktool.org/docs/install/)：编译和反编译apk，可以从APK中获得基础性资源（如图片等）<br>

---

# 准备阶段
&emsp;&emsp;一、安装[Java](https://www.java.com/zh-CN/)，具体步骤请详见Java官网，此处不再赘述；<br>&emsp;&emsp;二、下载[ApkTool脚本文件](https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/windows/apktool.bat)；<br>&emsp;&emsp;&emsp;&emsp;（如果不会下载，可以复制网页中的文本，新建一个名为&ensp; ***apktool*** &ensp;的&ensp; ***txt*** &ensp;文件，将网页文本内容复制下来，保存在&ensp; ***apktool.txt*** &ensp;中，之后将后缀&ensp; ***.txt***&ensp; 修改为&ensp; ***.bat*** &ensp;即可）<br>&emsp;&emsp;三、下载最新版本的[apktool.jar](https://bitbucket.org/iBotPeaches/apktool/downloads/)，并且重命名为 ***apktool.jar*** <br>&emsp;&emsp;&emsp;&emsp;（例如，我下载的文件为apktool_2.9.2.jar，只需要删除_2.9.2，使文件名为apktool.jar即可）<br>&emsp;&emsp;四、将 ***apktool.bat*** 和 ***apktool.jar*** 放在 ***同一目录（文件夹）*** 下。

---

# 基本用法（为了方便展示，我把所有文件放在了一个目录下）
&emsp;&emsp;一、APK文件的提取<br>&emsp;&emsp;1、在APK文件目录下运行CMD（在路径那里输入cmd，敲回车即可）
![image.png](https://s2.loli.net/2024/01/08/7AmXYRbDNIrUGS4.png)
![image.png](https://s2.loli.net/2024/01/08/BGtFrgCwSPbXmQD.png)
&emsp;&emsp;2、输入命令

    apktool.bat d [-s] -f <apkPath> -o <folderPath>

&emsp;&emsp;此处的 ***< apkPath >*** 是你的apk路径，比如我的为 ***"E:\apktool\pose-monitor-release.apk"*** （注意此处的引号为 ***英文*** ） ***< folderPath >*** 是你的导出目录， ***不填写*** 则会自动以 ***安装包名***在 ***apk的相同目录*** 下新建文件夹并且导出， ***若不填写，请一并删去&ensp;-o&ensp;这一命令*** 。
![image.png](https://s2.loli.net/2024/01/08/QeOiJfTmVbN8oYz.png)
&emsp;&emsp;显示这样的信息且在导出文件夹下存在 ***apktool.yml*** 文件代表导出成功，接下来就在文件夹中修改你的基础资源（如图片等）吧。
![image.png](https://s2.loli.net/2024/01/08/SAeLnvGIRZ1FUrE.png)

---

# STAFF
&emsp;&emsp;APKTool：https://apktool.org/docs/install/<br>&emsp;&emsp;pose-monitor-release:https://github.com/linyiLYi/pose-monitor
<div style="position:relative; width:100%; height:0; padding-bottom:75%;">
<iframe src="//player.bilibili.com/player.html?aid=732141008&bvid=BV1uD4y187zX&cid=879804782&p=1" 
scrolling="no" border="0" frameborder="no"  framespacing="0"  
style="position:absolute; width:100%; height:100%;  left:0; top:0"  > </iframe>
</div>
