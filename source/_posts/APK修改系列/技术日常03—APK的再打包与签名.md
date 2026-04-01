---
title: APK技术日常03—APK的再打包与签名
categories:
  - APK修改系列
abbrlink: 15022
tags:
  - APK
  - 技术日常
date: 2024-01-11 00:57:59
---
# 前言
***&emsp;&emsp;此处的apk的再打包是指之前教程中所拆解出来的apk文件的打包，如果是自己做的文件，不确定是否适用。而签名则是相当于对apk文件的认证，不签名则无法安装。***
<!--more-->

---

# 打包步骤
&emsp;&emsp;首先在你需要打包的文件的上一级目录下，打开CMD，运行以下命令

    apktool b <folderPath> -o folder's name.apk
&emsp;&emsp;这个命令的意义在于将 ***< floderpath >*** 这个文件夹打包为以这个文件夹名为文件名的apk文件。<br>&emsp;&emsp;比如此时我的文件结构为：<br>&emsp;&emsp;&emsp;&emsp;&emsp;E:<br>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;└─ apktool（需要打包的文件夹的上一级目录）<br>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;└─pose-monitor-release（需要打包的文件夹）<br>&emsp;&emsp;所以此时我就需要在apktool文件夹下运行cmd，运行命令：

    apktool b pose-monitor-release -o pose-monitor-release.apk
&emsp;&emsp;这样就会把pose-monitor-release这个文件夹打包成一个名为pose-monitor-release的apk文件，当出现如下图所示的信息时即为打包成功。
![image.png](https://s2.loli.net/2024/01/11/WMcSA1CfyBxoQPl.png)
&emsp;&emsp;之后你就可以看到你打包好的apk文件了（如果在需要打包的目录的同一级目录下没有找到，那就到需要打包的文件夹下的 ***build*** 文件夹下查看。

---

# 签名APK

## 工具准备
&emsp;&emsp;[MT管理器](https://mt2.cn/)

## 步骤
&emsp;&emsp;首先，在MT管理器中找到要处理的文件（可以用右上角三个点搜索）
![目录.jpg](https://s2.loli.net/2024/01/11/2IMwYcCarh6A35z.jpg)
&emsp;&emsp;为了确认，我点了一下，看了下详细信息
![详细信息.jpg](https://s2.loli.net/2024/01/11/cwsQYWACzPfxHpm.jpg)
&emsp;&emsp;然后长按，选择签名
![菜单.jpg](https://s2.loli.net/2024/01/11/SjQrmH6Nylqsoue.jpg)
&emsp;&emsp;签名秘钥可以选默认，也可以选自定义（如果你会的话），方案选择V1+V2（如果有报错，试试其他的方案）
![签名选择.jpg](https://s2.loli.net/2024/01/11/xtmzhCZG1BaVRd4.jpg)
&emsp;&emsp;此时大概率会有以下两种提示
![报错（权限）.jpg](https://s2.loli.net/2024/01/11/hXrMAptilO5vInG.jpg)
![报错（权限2）.jpg](https://s2.loli.net/2024/01/11/x4AQF5uOVvaw9Cz.jpg)
第一个发送通知点允许就好，这个是为了出现第二个提示。第二个提示随便点就好，没什么影响。
&emsp;&emsp;等到进度条走完
![进度条.jpg](https://s2.loli.net/2024/01/11/iMkVmHRYeN2uFbr.jpg)
&emsp;&emsp;会出现一个新的文件
![生成文件.jpg](https://s2.loli.net/2024/01/11/2QGXdAOqCFN5tkv.jpg)
&emsp;&emsp;第一个那个不是绿色的文件就是。至此，签名完成，可以自己试着安装。

---

# 后记
&emsp;&emsp;签名后如果产生报错，可以换个签名方式。V1，V2，V3其实对应着不同的安卓版本，自己看就好，还有一种签名方式就是使用JAVA的keytool，但是我忘了我的秘钥，具体可以自行百度。我觉得用MT最简单~~~