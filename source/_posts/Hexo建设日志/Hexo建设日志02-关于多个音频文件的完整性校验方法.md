---
title: Hexo建设日志02-关于多个音频文件的完整性校验方法
date: 2023-12-21 00:24:54
tags:
  - Hexo建设日志
categories:
  - Hexo建设日志
abbrlink: 23140
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
excerpt: "这是文章摘要 This is the excerpt of the post"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2025-12-21 00:24:54
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---
# ***前言：***
***&emsp;&emsp;最近在大量校验歌曲完整性时遇到了一点点小困难，文件错误或者文件损坏不能比较简便的检查出来。多方查询之后发现了一个较为简单的方法。***

<!--more-->

---

# ***工具：***
&emsp;&emsp;***foobar2000***<br>&emsp;&emsp;***需要校验的文件***

---

# ***步骤：***
&emsp;&emsp;首先，在&ensp;[foobar2000](http://www.foobar2000.org)&ensp;官网下载原始英文版软件，或者在吾爱破解等网站下载汉化版。我使用的是这个<br>&emsp;&emsp;链接：https://pan.baidu.com/s/1dI4ZSIPnbLY7wLYiJzpLmg?pwd=r6er<br>&emsp;&emsp;提取码：r6er<br>
&emsp;&emsp;然后打开软件。
![image.png](https://s2.loli.net/2023/12/21/3DQ5Y7JEfBAU9ZR.png)
&emsp;&emsp;把我们要校验的文件拖进来，同时***Ctrl+A***一下（全选完成就是文件名字上面变成了蓝色的条条）
![image.png](https://s2.loli.net/2023/12/21/UVsD25Qf8i7wXYI.png)
&emsp;&emsp;然后右键，选择&ensp;***工具-检验完整性***
![image.png](https://s2.loli.net/2023/12/21/CpzSr1Nm7w3ibyq.png)
&emsp;&emsp;然后等他走完进度条
![image.png](https://s2.loli.net/2023/12/21/d3SaRNzmnhWvb9q.png)
&emsp;&emsp;查看结果即可，有需要的话也可以导出成txt文件看
![image.png](https://s2.loli.net/2023/12/21/Z7p2S8wqBJzAbxy.png)
