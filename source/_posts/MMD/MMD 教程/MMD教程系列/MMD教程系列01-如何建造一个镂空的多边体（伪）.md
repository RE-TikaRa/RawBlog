---
title: MMD教程系列01-如何建造一个镂空的多边体
date: 2024-01-25 01:25:34
tags:
  - MMD
categories:
  - MMD
  - MMD 教程
  - MMD教程系列
abbrlink: 14648
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
sticky:
excerpt: "这是文章摘要 This is the excerpt of the post"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2026-01-25 01:25:34
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---
# 前言：
&emsp;&emsp;最近在到处水群的时候，看到了一位热衷于复刻PJSK的MV的群友[诺耶耶](https://space.bilibili.com/104696950)。在做MMD的时候遇到了一些小问题，所以我去试了试，然后感觉还不错，然后写了这个做镂空多边体的教程。请注意，此处并不是真正意义上的镂空，而是伪造的，所以当你使用某些会把透明通道关闭的渲染时，会穿帮。
<!--more-->

---

# STUFF：
## TOOL：
&emsp;&emsp;1、Metasequoia4_Ver.4.8.3b<br>&emsp;&emsp;2、GIMP_Ver_2.10.34<br>&emsp;&emsp;3、MikuMikuDance_Ver_926<br>&emsp;&emsp;4、PmxEditor_0273
## MODEL:
&emsp;&emsp;ぴるら式星界&emsp;&emsp;modeler: PilouLaBaka

---

# 如何建造一个镂空的多边体
## 模型建造篇
&emsp;&emsp;首先我在Metasequoia4里面建造了一个块块，然后选择一侧顶点放在一起，为什么没有合并呢，因为这样建造完他的UV还是一个方块，不是三角形，这样我画贴图就会很方便。至于为什么是Metasequoia4呢，是因为我用习惯了，包括导出UV贴图等，可以根据自己情况选择，比如PE的创建简易物体，然后用UV导出插件导出一张UV，此处记着UV图必须是带透明通道的格式。具体步骤见下：
### 视频版

<iframe src="https://www.acfun.cn/player/ac43645857" width="768" height="432" frameborder="0" allowfullscreen></iframe>

### 图文版
&emsp;&emsp;第一步：打开Metasequoia4。
![1.jpg](https://s2.loli.net/2024/01/26/PfRNyJgxOUB6971.jpg)
&emsp;&emsp;第二步：选择 ***“基本图形”*** ，在新打开的窗口中选择 ***“立方体”*** ，点击 ***生成***。
![2.jpg](https://s2.loli.net/2024/01/26/P6D7oYLsu4gGcQX.jpg)
&emsp;&emsp;第三步：选择一侧顶点（图中绿色的顶点），选择缩放，在新打开的窗口中输入 ***0*** ，点击 ***OK***。
![3.jpg](https://s2.loli.net/2024/01/26/xZFLY7eE91DRpCn.jpg)
&emsp;&emsp;然后就可以得到一个四棱锥。
![4.jpg](https://s2.loli.net/2024/01/26/LgrykZiVSXFDzhJ.jpg)
&emsp;&emsp;第四步：点击 ***左上角*** 那个 ***模型（字符）*** 大框框，在下拉选框中选择 ***导出UV贴图*** ，然后点击 ***展开*** ，之后大概率能够得到一个绿色的四边形和你的四棱锥，如果没有，在 ***视图窗的左上角选中展开图和物体*** ，如图中 ***第一步的文字提示下面的那个彩色框***中所示。
![5.jpg](https://s2.loli.net/2024/01/26/a5PSrjHRbTg76lF.jpg)
&emsp;&emsp;第五步：点击 ***UV操作*** ，选择 ***输出UV线图***。
![6.jpg](https://s2.loli.net/2024/01/26/3oNX9TRSdnr7tQh.jpg)
&emsp;&emsp;第六步：在新打开的窗口中输入UV图的长和宽，建议与贴图一致，不然之后很麻烦，然后选中文件，指定路径保存即可。
![7.jpg](https://s2.loli.net/2024/01/26/gMHahxfku9tSPvm.jpg)
&emsp;&emsp;第七步，点击 ***文件***，选择 ***另存为***，保存类型选择 ***.pmd***，此时要注意你的pmd文件必须 ***与刚才导出的UV图处于同一文件夹下***。
![8.jpg](https://s2.loli.net/2024/01/26/yVYMTgGuiceAxEb.jpg)
![9.jpg](https://s2.loli.net/2024/01/26/dLc2fRKBDOCrikx.jpg)
&emsp;&emsp;然后你就可以得到以下文件。
![10.jpg](https://s2.loli.net/2024/01/26/FZDElRVxfGN6KBW.jpg)

## 贴图处理篇
&emsp;&emsp;此处重点是将导出的UV贴图处理成一个框框，建议看视频版教程，图片版我不写了，用UV贴图作为基础修改是因为这样后期只需要重新指定一下材质的贴图路径就好，不需要做UV上的修改。中间记着得是透明的，所以处理后保存时文件类型必须是带透明通道的，如bmp，png等，所以这一步你用美图秀秀做出来一个框也是一样的效果。
### 视频版

<iframe src="https://www.acfun.cn/player/ac43645838" width="768" height="432" frameborder="0" allowfullscreen></iframe>

## 模型处理篇
&emsp;&emsp;此处是将我们的模型变成镂空的。
### 视频版

<iframe src="https://www.acfun.cn/player/ac43645829" width="768" height="432" frameborder="0" allowfullscreen></iframe>

### 图文版
&emsp;&emsp;第一步：用PE打开刚才导出的PMD，会发现一片白，连坐标轴都看不见。没关系，不要介意。首先我们在PmxView窗口中选择 ***显***，然后点击 ***背景色旁边的白色的框***，然后在新打开的窗口选择一个自己喜欢的颜色（此处建议对比度高一点，比如深色系），点击 ***确定***。
![1.jpg](https://s2.loli.net/2024/01/26/HmIqOwR7DcYFMyL.jpg)
&emsp;&emsp;第二步：把整个模型缩小，用插件也行，直接顶点缩放也行，反正没刚体没J点，你想怎么缩放怎么缩放，但是此时模型应该是比较大的，缩放应该在0.1倍左右才算正常，具体大小你自己看看吧，按照自己所需要的缩放就成。
![2.jpg](https://s2.loli.net/2024/01/26/ueqhCSLBHnMroY9.jpg)
&emsp;&emsp;第三步：在 ***Pmx编集*** 窗口下 ***材质***一栏中，将我们刚从处理好的贴图赋予材质（在tex那里输入我们刚处理好的贴图的文件名即可，如下图）
&emsp;&emsp;此时，我们的模型就变成透明的了。但是有一个问题，只能透过一边，看不见对面的，怎么办呢，此时在描绘那里打开 ***双面描绘*** 就解决了！然后保存为pmx即可
![3.jpg](https://s2.loli.net/2024/01/26/aAsMIjkoDbpXdcq.jpg)
![4.jpg](https://s2.loli.net/2024/01/26/tFDMydbiju4AqeS.jpg)
&emsp;&emsp;这样，我们就做好了一个（伪）镂空的四棱锥，其余的也是同理，只不过在处理UV那里就不太一样了，下面的视频是对复杂模型镂空化的处理。但是，注意到其实他这个透明处理的不太行，这边其实更建议用SAI2做这个透明通道，SAI2中可以直接选择明度转换到透明度，就很方便。最后如果有不正常透过关系，记着调材质顺序。

<iframe src="https://www.acfun.cn/player/ac43642417" width="768" height="432" frameborder="0" allowfullscreen></iframe>
