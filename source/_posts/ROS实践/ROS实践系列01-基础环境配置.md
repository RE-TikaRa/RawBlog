---
title: ROS实践系列01-基础环境配置
thumbnail: 'https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png'
excerpt: 安装并配置虚拟机以及Ubuntu
banner: 'https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png'
password: ''
abstract: '有东西被加密了, 请输入密码查看.'
message: '您好, 这里需要密码.'
wrong_pass_message: '抱歉, 这个密码看着不太对, 请再试试.'
wrong_hash_message: '抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.'
expires: '10000-01-01 07:59:59'
categories:
  - ROS实践
abbrlink: aee7723c
date: 2026-03-15 18:21:30
tags:
sticky:
---

# 安装VMware Workstation

VMware Workstation 是由 VMware 公司开发的一款桌面虚拟化软件（也称为托管型 Hypervisor），允许用户在单一物理计算机上同时运行多个操作系统，例如 Windows、Linux 和 BSD 等，作为虚拟机（VM）运行在宿主操作系统之上。截至 2025 年，**VMware Workstation** 所属的公司是 **Broadcom Inc.**（博通公司）。Broadcom 于 **2023 年 11 月**正式完成对 VMware 的收购 。自此，VMware 成为其旗下虚拟化业务的一部分。

值得注意的是，在 Broadcom 收购 VMware 之后，**VMware Workstation Pro 自 2024 年 5 月起已转为免费提供**，不再收取许可费用，适用于个人和商业用途 。

但是基于国内网络的特殊性，以及博通网站的复杂性，我已做了新版的备份。

## 安装过程

双击打开`VMware-workstation-full-17.6.4-24832109.exe`安装包

![image.png](https://s2.loli.net/2025/10/02/1bLeR8Qj49dtJPr.png)

点击下一步

![image.png](https://s2.loli.net/2025/10/02/eBAupjPGL2IOrKq.png)

勾选后选择下一步

![image.png](https://s2.loli.net/2025/10/02/CgrLqZNFA9fzvJY.png)

保持默认，下一步

![image.png](https://s2.loli.net/2025/10/02/omXYj9g2Ur5OCuE.png)

取消勾选，下一步

![image.png](https://s2.loli.net/2025/10/02/ByYHNmqIWrM4L2l.png)

保持默认，下一步

![image.png](https://s2.loli.net/2025/10/02/JwvQqpxIPOzGa5y.png)

开始安装

![image.png](https://s2.loli.net/2025/10/02/hiXNryUvHZdbo9A.png)

![image.png](https://s2.loli.net/2025/10/02/Bpklj6etUnu8GvD.png)

安装完成



<div style="
  height: 1px;
  background: linear-gradient(to right, transparent, #B0A8B9, transparent);
  margin: 24px 0;
  opacity: 0.7;
"></div>

# 创建虚拟机-Ubuntu

打开VMware Workstation

![image.png](https://s2.loli.net/2025/10/02/YbTiN45XvqfwRdF.png)

点击`创建新的虚拟机`，在打开的新窗口中按照如下配置

![image-20251002020151721](https://s2.loli.net/2025/10/02/2wl1mKN9MfecWTP.png)

![image-20251002020309661](https://s2.loli.net/2025/10/02/VAumvznqb3QhIa7.png)

![image-20251002020404921](https://s2.loli.net/2025/10/02/yOJk9SsF2f3drou.png)

![image-20251002020452001](https://s2.loli.net/2025/10/02/3OymLZgwTGcRDAu.png)

![image-20251002020526721](https://s2.loli.net/2025/10/02/qoA26mfwkTJILFQ.png)

![image-20251002021205838](https://s2.loli.net/2025/10/02/fKeErd2H1OuYxqV.png)

![image-20251002021256677](https://s2.loli.net/2025/10/02/cTpgJtMAdjz9QKX.png)

![image-20251002021347484](https://s2.loli.net/2025/10/02/QXKMhJsUZ8fg9av.png)

![image-20251002021412471](https://s2.loli.net/2025/10/02/Gi5eZ6UrlKkcxg1.png)

![image-20251002021431496](https://s2.loli.net/2025/10/02/Z7uTngzySLm84ox.png)

![image-20251002021515051](https://s2.loli.net/2025/10/02/62qS3ouOxFnW8rP.png)

![image-20251002022914546](https://s2.loli.net/2025/10/02/mQocq45FtreSkbg.png)

![image-20251002023033509](https://s2.loli.net/2025/10/02/r2Gnq3WikTEyFMp.png)

![image-20251002023148533](https://s2.loli.net/2025/10/02/GJDluktHnXUgMfw.png)

![image-20251002023221645](https://s2.loli.net/2025/10/02/IYUPQX2l9kCyfzh.png)

此时虚拟机部分创建完毕
<div style="
  height: 1px;
  background: linear-gradient(to right, transparent, #B0A8B9, transparent);
  margin: 24px 0;
  opacity: 0.7;
"></div>
# 配置虚拟机系统

![image-20251002023915515](https://s2.loli.net/2025/10/02/yuDKlRrPMqXHn3J.png)

<div style="
  height: 1px;
  background: linear-gradient(to right, transparent, #B0A8B9, transparent);
  margin: 24px 0;
  opacity: 0.7;
"></div>
# 虚拟机系统设置

## 基本设置

启动虚拟机

![image-20251002024224715](https://s2.loli.net/2025/10/02/ICKMb4cgwzRHU2Y.png)

等待加载至如下界面，下翻找到`简体中文`，点击后选择`试用`

![image-20251002024403918](https://s2.loli.net/2025/10/02/ARu2pUWNOBthZSK.png)

打开设置

![image-20251002024614732](https://s2.loli.net/2025/10/02/E5kFMWvsbPYBeZ6.png)

下翻找到设备，调整设备分辨率以适合窗口

![image-20251002024850619](https://s2.loli.net/2025/10/02/erYu5mpM9XVf6DZ.png)

双击桌面上的安装Ubuntu

![image-20251002025231984](https://s2.loli.net/2025/10/02/ReWMXE8DT5mlbhG.png)

![image-20251002025347956](https://s2.loli.net/2025/10/02/Q86YjvMly35bq2a.png)

![image-20251002025411190](https://s2.loli.net/2025/10/02/8sD1LwCUeYHtkfy.png)

![image-20251002025451570](https://s2.loli.net/2025/10/02/lyRAbhWw9XCK8G2.png)

![image-20251002025559235](https://s2.loli.net/2025/10/02/1GrSauzlyxkYDHP.png)

![image-20251002025637091](https://s2.loli.net/2025/10/02/f9oSHY8nD6OXaT5.png)

![image-20251002025715469](https://s2.loli.net/2025/10/02/FDazoh9wBeVSCxs.png)

![image-20251002025810540](https://s2.loli.net/2025/10/02/Vl6hTswdoLMuSrB.png)

![image-20251002030103891](C:\Users\Tika\AppData\Roaming\Typora\typora-user-images\image-20251002030103891.png)

![image-20251002030303689](https://s2.loli.net/2025/10/02/i1mw79VjcK8PbuF.png)

重启后重新修改一遍分辨率，步骤同上

## 创建模板

![image-20251002031647027](https://s2.loli.net/2025/10/02/7VmCrOKi8gwz5xS.png)

然后随便复制一个文本文件到模板文件夹下，改一下你熟悉的名字

![image-20251002031724534](https://s2.loli.net/2025/10/02/8qFaZmMzlhiYGPj.png)

## 安装VM-TOOLS

打开终端，使用如下命令

```commands
sudo apt install open-vm-tools-desktop -y
```

得到如下即可

![image-20251002032024117](https://s2.loli.net/2025/10/02/nTtGvyQFWrPZuOU.png)

输入密码时，需要注意的是，此时终端并不会显示你的密码，所以，你直接输入后回车即可，安装完成之后重启虚拟机

## 安装ROS

终端中使用如下命令以一键安装（使用鱼香ROS）

```commands
wget http://fishros.com/install -O fishros && . fishros
```

![image-20251002033002992](https://s2.loli.net/2025/10/02/W167qjPYrsuUInB.png)

如上便是安装完成

然后选择`一键安装(推荐):ROS(支持ROS/ROS2,树莓派Jetson)`

 1sudo ln -s /usr/bin/python3 /usr/bin/pythonbash

接下来出现如下内容，按照我的选择即可（即安装melodic(ROS1)和melodic(ROS1)桌面版）

```commands

RUN Choose Task:[请输入括号内的数字]
请选择你要安装的ROS版本名称(请注意ROS1和ROS2区别):
[1]:bouncy(ROS2)
[2]:crystal(ROS2)
[3]:dashing(ROS2)
[4]:eloquent(ROS2)
[5]:melodic(ROS1)
[0]:quit
请输入[]内的数字以选择:5

RUN Choose Task:[请输入括号内的数字]
请选择安装的具体版本(如果不知道怎么选,请选1桌面版):
[1]:melodic(ROS1)桌面版
[2]:melodic(ROS1)基础版(小)
[0]:quit
请输入[]内的数字以选择:1
```





### 报错

在此安装鱼香ROS时下可能会有报错，即无法连接到网络，如果无法连接到网络，这边建议更换网络模式，如下

![image-20251002033325042](https://s2.loli.net/2025/10/02/W167qjPYrsuUInB.png)

![image-20251002033328172](https://s2.loli.net/2025/10/02/audMcAFp8xXoPUV.png)

如果更换后问题依旧，这边建议Bing或者找我