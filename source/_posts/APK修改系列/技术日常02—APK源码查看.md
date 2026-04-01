---
title: APK技术日常02-APK源码的查看
tags:
  - APK
  - 技术日常
categories:
  - APK修改系列
abbrlink: 64111
date: 2024-01-08 15:04:26
---
# 前言
***&emsp;&emsp;代码设计是每位工程师心血的结晶，源代码的查看仅能作为学习使用，不可以不劳而获。***
<!--more-->

---

# 准备阶段
&emsp;&emsp;1、[dex2jar](https://sourceforge.net/projects/dex2jar/files/latest/download)&emsp;用于可运行文件classes.dex反编译为jar文件；<br>&emsp;&emsp;2、[JD-GUI](http://java-decompiler.github.io/)&emsp;用于查看jar文件源码

---

# 使用方法
&emsp;&emsp;1、将自己所要提取的apk文件后缀名改为zip（或者其他可以解压的后缀，如rar），并且解压（注：此过程不可逆，解压缩之后再压缩，会导致apk损坏，建议先备份一份，然后用副本做修改工作）
![image.png](https://s2.loli.net/2024/01/09/GpUrjXvH8EBdMnJ.png)
&emsp;&emsp;2、将&ensp;***classes.des***&ensp;文件复制到dex2jar的目录之下
![image.png](https://s2.loli.net/2024/01/09/g7ewyZ4hQDvdGVS.png)
&emsp;&emsp;3、在此目录下运行cmd（运行办法见[APK技术日常01](https://re-tikara.github.io/2024/01/07/mou-xie-ji-zhu-ri-chang/apk-xiu-gai-xi-lie/ji-zhu-ri-chang-01-apk-fan-bian-yi/)），在CMD中运行以下命令

    d2j-dex2jar.bat classes.dex

&emsp;&emsp;会生成由 ***classes.dex*** 反编译得到的jar文件 ***classes-dex2jar.jar*** 。
![image.png](https://s2.loli.net/2024/01/09/8VIBrYyfChSlNpw.png)
4、用JD-GUI打开 ***classes-dex2jar.jar***即可查看源码（注：源码若经过混淆，此处能查看的也是经过混淆的版本）
![image.png](https://s2.loli.net/2024/01/09/wHEtAbVxR2OYCsP.png)

---

# STAFF
&emsp;&emsp;1、dex2jar：https://sourceforge.net/projects/dex2jar/files/latest/download<br>&emsp;&emsp;2、JD-GUI：http://java-decompiler.github.io/


---

# 后记
&emsp;&emsp;如果只是想更换图片等资源，在[APK技术日常01](https://re-tikara.github.io/2024/01/07/mou-xie-ji-zhu-ri-chang/apk-xiu-gai-xi-lie/ji-zhu-ri-chang-01-apk-fan-bian-yi/)那里处理完apk进入对应文件夹修改即可。修改代码比较麻烦，因为反编译出来的结果中只有smali文件，即Java虚拟机支持的汇编语言。如果确实需要修改代码，就得对照smali文件和从classes.dex反编译出来的源码了，按照smali的规范来改动即可。相当于写汇编，难度较大，感兴趣可以自己探索。