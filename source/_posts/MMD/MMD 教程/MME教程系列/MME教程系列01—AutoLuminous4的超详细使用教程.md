---
title: MME教程系列01—AutoLuminous4的超详细使用教程
date: 2024-01-30 23:44:18
tags:
  - MME
categories:
  - MMD
  - MMD 教程
  - MME教程系列
abbrlink: 6e81bfe7
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
sticky:
excerpt: "这是文章摘要 This is the excerpt of the post"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2026-01-30 23:44:18
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---
# 前言
&emsp;&emsp;我又来了，这次是AutoLuminous4的超详细用法！比B站那个还详细（确信）在这里写写，然后我就不发到B站了，大致看看吧。然后就是，其实在这里写到的所有效果，在そぼろ的ReadMe文件中都有写到。
<!--more-->

---

# STUFF
## MODEL
&emsp;&emsp;◆Sour式初音ミクVer.1.02◆<br>&emsp;&emsp;製作者/Modeller：Sour暄
## POSE
&emsp;&emsp;Ponx-迫奈熏
## MME
### Main
&emsp;&emsp;&emsp;&emsp;発光エフェクト<br>&emsp;&emsp;&ensp;AutoLuminous Ver.4.2<br>&emsp;&emsp;&emsp;&emsp;&ensp;製作：そぼろ
### APPEND
&emsp;&emsp;splitview_v01<br>&emsp;&emsp;製作者：データP<br>&emsp;&emsp;Diffusion<br>&emsp;&emsp;製作者：そぼろ

## TOOL
&emsp;&emsp;1、VSCode<br>&emsp;&emsp;2、MikuMikuDance<br>&emsp;&emsp;3、PmxEditor

---

# 某些缩写：
    AutoLuminous4=AL、AL4（4为大版本，即Ver.4.x，本教程为Ver.4.2）
    ReadMe=RM
    MikuMikuDance=MMD
    PmxEditor=PE

---

# MME介绍
&emsp;&emsp;AL是由そぼろ为MMD所制作的一款基础性的插件，可以为符合AL标准要求的模型提供发光的效果。
![加入对比.png](https://s2.loli.net/2024/01/31/oeK6ntRiUdC9SrF.png)
&emsp;&emsp;AL目前已经更新到第四代，即AutoLuminous_ver4.2.本教程基于本AL版本下所编写，若有不同，请自行参照ReadMe文件或是下载最新版。
## 下载指路：
&emsp;&emsp;[そぼろ的配布站点](https://onedrive.live.com/?authkey=Arbitrary&id=EF581C37A4524EDA%21107&cid=EF581C37A4524EDA)

---

# 基础篇
&emsp;&emsp;AL的开放度极高，一般情况下都可以做到随载随用，所以本章节教程尽量不涉及模型的修改，代码层面的修改等，尽量在MMD主体以及MME插件下做简单讲解。
## 文件介绍
&emsp;&emsp;当我们下载好AL，并且全部解压之后，可以获得如下文件（如果是乱码建议换个可以改编码的压缩器）
    
    AutoLuminous4
    │  AL_Object.fxsub
    │  AutoLuminous.fx
    │  AutoLuminous.png
    │  AutoLuminous.x
    │  AutoLuminous.xml
    │  AutoLuminousBasic.fx
    │  AutoLuminousBasic.x
    │  Readme.txt
    │  Readme上級編.txt
    │  
    ├─Options
    │       AL_BlackMask.fxsub
    │       AL_Test.x
    │       AL_Texture.fxsub
    │       AutoLuminousSetter.zip
    │       full_saturate.fx
    │       LightSampling.fx
    │       LightSampling.x
    │       ToneCurve.x
    │       白背景.x
    │       追加UV一括設定スクリプト.cx
    │       黒背景.x
    │      
    └─Samples
            Sample1.x
            Sample2.pmd
            Sample3.pmx
            Sample4.pmx
            Sample5.pmx
            Sample6.pmx
            Sample6.png
&emsp;&emsp;其中AutoLuminous.x与AutoLuminousBasic.x是我们重点使用的文件，而AutoLuminousBasic.x是AutoLuminous.x的阉割版，前者没有后者那样的开放度，如：前者x，y，z参数等没有办法调整，发光只能发出白光等。故下文所有教程都是建立于AutoLuminous.x这一版本上。
## MMD内附件控制参数介绍
◆&ensp;Si参数讲解<br>&emsp;&emsp;Si是指发光强度，对比如下：
![SI对比.png](https://s2.loli.net/2024/01/31/sJm2BZ8cgwzVMAo.png)
◆&ensp;Tr参数讲解<br>&emsp;&emsp;此处借用原作者的话
    
    原文：
        ・Tr: ぼかし強度
    
        発光部分のぼかしの強さを指定します。
        大きくすることはできません。
        これは、もともとのぼかし強度がかなり大きく設定されているためです。
        それでも大きくしたい場合はエフェクトの直接編集が必要です
    译文：
        Tr：模糊强度。
        
        指定发光区域的模糊强度。
        不能增加。
        这是因为原始模糊强度设置得相当高。
        如果还想增加，则需要直接编辑效果。

&emsp;&emsp;对比如下：
![tr对比.jpg](https://s2.loli.net/2024/02/03/MxLSvQDW9pdCzKw.jpg)
◆&ensp;X参数讲解<br>&emsp;&emsp;X为炫光的光芒数，请注意，光芒数是以2倍关系存在的，比如你输入x=1，则会有2条光芒，以此类推，并且，当你光芒数增加时，亮度也会提升，同时对于电脑的渲染压力也会增大。对比如下：
![X对比.jpg](https://s2.loli.net/2024/02/03/dmqjgWPnCvNVUbY.jpg)
◆&ensp;Y参数讲解<br>&emsp;&emsp;Y参数掌控原始亮度，调节范围在-100到100之间。对比如下：
![Y对比.jpg](https://s2.loli.net/2024/02/03/gJcvdMmSoIpl16L.jpg)
◆&ensp;Z参数讲解<br>&emsp;&emsp;Z参数实际上就是更加精细的Si参数，此处借用作者的话：  

    原文：
        ・Z: 発光強度

        値の指定方法が違うだけで、効果はSiと同じです。
        適正範囲は -100～500 程度です。
        -100でSi=0と、100でSi=2と同じ効果があります。
        ダミーボーンから発光強度を操作したい場合を想定しています。
    译文：
        Z：发光强度。

        效果与 Si 相同，只是指定值的方法不同。
        合适的范围是 -100 至 500。
        效果与 Si=0 时的 -100 和 Si=2 时的 100 相同。
        假设您想操作假骨的发光强度。

◆&ensp;Rx参数讲解<br>&emsp;&emsp;Rx是光芒的角度，只有当x≠0时（即光芒启用时），此数据才可以生效，对比如下：
![Rx对比.jpg](https://s2.loli.net/2024/02/03/vd1OKrLckwVYheZ.jpg)
◆&ensp;Ry参数讲解<br>&emsp;&emsp;Ry是改变光芒的长度，作者建议的范围在-100~100，太长会出现条纹，对比如下
![0.jpg](https://s2.loli.net/2024/02/03/vswaVkr4ELWzJN9.jpg)
&emsp;&emsp;~~(我好像没咋看出0和100的区别，可能是透明通道的锅，MMD里面挺明显)~~ <br>下面是Ry=400，就有很明显的条纹了，但是我加了个Diffusion，会稍微好一点，短范围内可以试试？（第一个图没有加Diffusion，第二个图加了）
![400.jpg](https://s2.loli.net/2024/02/03/oBECcgNZifldxSI.jpg)
![400+Diffusion.jpg](https://s2.loli.net/2024/02/03/Z8mOLzsX4hHoeRD.jpg)
◆&ensp;Rz参数讲解<br>&emsp;&emsp;这个参数就是用来kirakira的闪（呼唰呼唰~~~~~）， 输入的值是以秒为单位的闪烁周期。正数表示正弦波闪烁，负数表示方波闪烁。0代表不闪烁，绝对值越小闪的越快
 ~~（这个就不配图了吧，MarkDown配GIF有点麻烦的说）~~
 ~~（嘴上说着，还是配了）~~
&emsp;&emsp;这个是Ry=1的
![1.gif](https://s2.loli.net/2024/02/03/RcEXBp1sQeHTlDv.gif)
&emsp;&emsp;这个是Ry=0.1的
![0.1.gif](https://s2.loli.net/2024/02/03/fIb3WEJZF6H2jwc.gif)
&emsp;&emsp;这个是Ry=-1的
![-1.gif](https://s2.loli.net/2024/02/03/mN3bFJIK81BdDAt.gif)
&emsp;&emsp;这个是Ry=-0.1的
![-0.1.gif](https://s2.loli.net/2024/02/03/lvxq9ZHbB4pP3Xt.gif)
&emsp;&emsp;~~(不知道0.1和-0.1能不能看出来差别，应该可以。。)~~
&emsp;&emsp;可以将坐标轴系改成附件来修改更加随意的效果，X,Y,Z对应的移动，Rx，Ry，Rz对应的是转动。更改控制类型的方法：在图示红框内连续点击，会有三个参数：
    
    1、LOCAL：轴坐标系，会根据你骨骼的预定轴向为坐标系
    2、GLOBAL：世界坐标系，轴向严格按照上下Y，左右X，前后Z的方向
    3、ACCESSORY：附件控制状态，此时拖拽X，Y，Z或者Rx，Ry，Rz将会改变附件编辑框内的数据
![image.png](https://s2.loli.net/2024/02/03/IuUTd9ygOqWj2Em.png)

---

## MME特效分配栏参数讲解
&emsp;&emsp;当我们加入AL之后，在MME窗口会出现下面这一栏
![image.png](https://s2.loli.net/2024/02/03/Prc3JW7nFYXMiZT.png)
&emsp;&emsp;这一栏便是AL的特效分配栏，其中White.pmx是我们模型的文件名。而后面那一大串路径，是我们的特效文件。之前听过这样一个比喻：.x文件，.fx文件，.fxsub文件，三者的关系就像胶囊一样。x文件是胶囊外面那层皮，fx文件是里面的药，fxsub文件是模型的特异性受体。一般情况下，x文件不是真正起作用的，起作用的是fx文件，二者一般要搭配使用。而单独有效的x文件，比如B站MMD十周年教程里的screen.x，这种就类似于药片，x文件自己有效。对于模型的fxsub文件，相当于特异性受体，有了，可以对模型进行调控，没有，有时候也可以用fx直接强力打击。（不知道能不能看懂）<br>&emsp;&emsp;此时，AL_Object.fxsub调控我们模型，该发光的发光，不该发光的不要发光。当我们去除掉这一个分配，就会和下图一样，整个模型都亮起来了：![正常分配.png](https://s2.loli.net/2024/02/03/I1kmuBwxqFGMsvR.png)
![解除分配.png](https://s2.loli.net/2024/02/03/IbQHmZVpE8hSwzn.png)
&emsp;&emsp;如果我们把前面的勾选去掉，就会发不了光：
![image.png](https://s2.loli.net/2024/02/03/OVjYgh7pZ4iluJk.png)
&emsp;&emsp;其余的相关挂载分配见下表（我常用的）：
    
    AL_Object.fxsub：正常
    AL_BlackMask.fxsub：取消发光，和取消勾选一个结果
    AL_Texture.fxsub：局部纹理高强度发光，详见下文

## 故障排除
&emsp;&emsp;此处借用作者的方法：
    
    出现错误，无法运行。
        →检查 MME 是否为 0.27 或更高版本。
        →再次尝试下载。
        →不幸的是，您的 grabo 很可能与之不兼容。

    错误未出现，但无法正常工作。
        →请检查是否只使用样本和 AutoLuminous 就能正常工作。
        →检查 AutoLuminous.x 的位置、大小等是否为异常值。
        → 再次尝试下载。
        →不幸的是，很有可能抓取器不兼容。
        →如果您怀疑存在错误，请在 Twitter 等网站上报告。

    材质变形无法反映。
        →由于 MME 规范的原因，变形后的颜色无法正常获取。
        自 3.5 版起，镜面反射强度和 Alpha 会被反映。
        在 MMM 中，可以使用材质变形。

    太重，无法正常工作。
        →尝试编辑效果并将 HALF_DRAW 设置为 1。
        图像质量会下降，但会更轻。
        编辑效果并将 HDR_RENDER 设置为 0。
        功能会受到限制，但图像会变得更亮。
        尝试减少采样次数。
        尝试 AutoLuminousBasic。
        考虑替换 ObjectLuminous 或 KeyLuminous。
        更换 PC 或抓取器。

    不想发光的部分会自行发光。
        如果添加的球体发光，请将模型添加到选项文件夹中
        将选项文件夹中的 full_saturate.fx 应用于模型。
        在 "MME 分配 "选项卡中选择 AL_EmitterRT、
        将 "AL_BlackMask.fx "分配给不想发光的模型。
        编辑效果并将 HDR_RENDER 设置为 0。
        将 "KEYCOLOR_NUM "设为 0 以关闭关键色彩发射功能。

    如何编辑配件？
        用记事本打开 X 文件，直接调整数值。
        用记事本打开 X 文件，直接调整数值...
        自述文件的高级部分添加了关于在 PMDE 中编辑附件的内容。

## 恭喜你~ 基础篇到此完结~

---

# 高级篇
&emsp;&emsp;欢迎来到AL的进阶教程！在此篇中，默认你已经会了PE的所有基础教程，并且，熟练掌握各种可以正确修改fx的软件（例如，VSCode，EveryEditor等等），就让我们开始愉快的AL的进阶之旅吧。注：本教程内AL的所有参数均为初始参数，不做任何修改，修改的仅仅是模型。

## 扒扒示例内容的底裤
&emsp;&emsp;首先让我们看看そぼろ様为我们准备了写什么好玩的例子
    
    Samples：
            Sample1.x
            Sample2.pmd
            Sample3.pmx
            Sample4.pmx
            Sample5.pmx
            Sample6.pmx
            Sample6.png
    样品 1.
        一个涂有四种不同颜色的球。
        球的蓝色和粉色部分被设置为发光。

    样本 2
        PMD 版本的样本。
        绿色和黄色被指定为发光颜色。
        您可以尝试使用变形来控制面部表情。

    样本 3
        PMX 版本的样本。 这是一个灰色立方体。
        可以测试 2.0 版的新功能，如顶点发射。

    样本 4.
        PMX 版本的样本。 多板多边形。
        您可以测试顶点发射中的色调变形和 3.0 以来的其他新功能。
        您还可以通过材质变形测试发射强度的变化。

    样本 5.
        这是 PMX 版本的样本。 小球呈螺旋状排列。
        您可以使用 AutoLuminouSetter 测试复杂的顶点发射。

    样本 6.
        这是自 4.0 版起新增的发射序列控制示例。
        同名的 PNG 文件是一个球形样本。
        您还可以尝试 4.0 中的其他变形。
## 附加UV参数讲解
            
    附加 UV1。
    　X：0.2，Y：0.7
    　　表示这是 AutoLuminous 的附加 UV 数据的识别码。
    　　该值为固定值。

    　Z：闪烁周期
    　　以秒为单位指定闪烁周期。
        负值会导致方波闪烁。

    　W：标志
        指定标志。 从以下项目中添加所需的项目。
        曲面的所有顶点的该值必须相等。

    　    　-数字 1：纹理模式。
    　    　　0：标准（纹理乘法）
    　　　1：无纹理乘法。
    　　　2：高强度提取，如果为 UV2 指定了（1,1,1,1,1），则相当于 AL_Texture。
    　　10 位数字：色彩模式。
    　　　00：标准（RGB 规格）
    　　　10 : 将 UV2 的 XYZ 从 RGB 改为 HSV。
    附加 UV2
    　X：红色，Y：绿色，Z：蓝色
    　　指定发射颜色。

    　W：发光强度
    　　指定发光强度。 标准值为 1。


    附加 UV3
    　X：纹理颜色减法。
    　　该值从纹理颜色中减去，如果小于 0 则四舍五入为 0。
    
    　Y：闪烁阶段
    　　以秒为单位指定闪烁阶段。

    　Z：弹出式
    　　按指定值将发光部分向正常方向推出。
    　　此功能可用于隐藏发光对象。


## 扒扒示例3的底裤（可以看到顶点发光以及闪烁的顶点发光）
&emsp;&emsp;3的特殊之处在于，明明是是一个灰色的块块，四个顶点颜色不一样，还有一个角在闪，神奇的呢。（本节是一个大块，根据标题可以看到，本节是顶点发光有关
![示例3.gif](https://s2.loli.net/2024/02/03/17AIfUpokqycwiB.gif)
&emsp;&emsp;打开PE看看参数，映入眼帘的就是 ***追加UV:3*** 
![image.png](https://s2.loli.net/2024/02/03/spPrqSJlynKfamN.png)
&emsp;&emsp;再结合そぼろ様的论述：PMX 版本的样本。 这是一个灰色立方体。可以测试 2.0 版的新功能，如顶点发射。<br>&emsp;&emsp; ~~顶点发射是虾米？？？？我怎么不知道？？？？我在RM怎么没有找到！！小事啦~ 现在我们可就不能光停留在RM的初级版本，我们应该升升级，看看 ***Readme上級編.txt*** 这个RM啦。~~<br>&emsp;&emsp;そぼろ様曾云：PMXのみ、追加UVを用いて頂点ごとの発光制御を行うことができます。材質指定より柔軟に設定できますが、改造やデータ管理は煩雑になります。<br>&emsp;&emsp;意思就是:只有 PMX 允许使用附加 UV 对每个顶点进行发射控制。这样的设置比材料规格更为灵活，但修改和数据管理更为复杂。<br>&emsp;&emsp;由此我们可以得出，只要在PE里面对模型设置好有关的数值，那么我们也可以这样玩~~这样我们就来PE实操一下吧。<br>&emsp;&emsp;首先，根据そぼろ様在RM中写到：
            
    附加 UV1。
    　X：0.2，Y：0.7
    　　表示这是 AutoLuminous 的附加 UV 数据的识别码。
    　　该值为固定值。
&emsp;&emsp;那么也就是说，当某顶点追加UV1的数值中X：0.2，Y：0.7就说明这个是与AL有关的顶点。那么我们来看看，示例3中有哪些是带有AL的“身份证”的呢。导出一份顶点CSV，可以看到
![image.png](https://s2.loli.net/2024/02/03/P59Ei7L1jskWa6B.png)
&emsp;&emsp;4、5、6、7、11、14、23这几个顶点的追加UV1_x,追加UV1_y，都是0.2和0.7的身份代码。那就说明这几个顶点和AL有关，现来看看那个会闪红光的角角吧。分别是11、14、23都是那个角上的三个面的顶点，他们的追加UV1_z,追加UV1_w都是2和0，这两个数据代表的是闪烁和标志，相关解释看上面。<br>&emsp;&emsp;然后，看看追加UV2的参数吧。哇！神奇诶！他们的追加UV2_x,追加UV2_y,追加UV2_z,追加UV2_w的数值，都是0.8,0.03,0.02,1，前面三个是用来调节颜色的，后面一个是发光的倍率，默认要填1，把颜色参数输入到材质那里看看。
![image.png](https://s2.loli.net/2024/02/03/X5s7tpQauMHNfom.png)
&emsp;&emsp;红不红！！！过年就得喜庆点。这样看上去和发的光颜色一样呢（笑<br>&emsp;&emsp;再来看看追加UV3：0,0,0,0,0,好多0啊，为什么呢？因为UV3我们根本没用到啊~其实这个样子你到MMD里面已经成功了，可以发红光闪烁，其余颜色的话，在材质那里调节好颜色之后，把参数复制到UV2的XYZ里面就好，不想闪烁，就把附加UV1里面的Z填成0就好<br>&emsp;&emsp;但是，他只能发出来一种颜色啊，我们当然不满足于此，我们还要随心所欲 ~~mercy~~ 的修改颜色！！！！！！！<br>&emsp;&emsp;接下来，欢迎来到Sample4的世界！
## 扒扒示例4的底裤（可以看到色相修改，表情的使用）
![示例4.gif](https://s2.loli.net/2024/02/03/S2XHUNDFlKhuBLP.gif)
&emsp;&emsp;好欢快，开趴！！！！（懒了，写不动了咋办，碎碎念）
### 色相改变
&emsp;&emsp;首先拆拆这个色相改变，继续用PE打开这个模型，顺手导出一份CSV。好嘛，开屏一张，追加UV:3
![image.png](https://s2.loli.net/2024/02/03/EfzTvauKMVblo2Y.png)
&emsp;&emsp;看看追加，然后通过模型窗，找到我们可以改色相的顶点，老熟人4，5，6，7号
![image.png](https://s2.loli.net/2024/02/03/zpkr4AJ3Ms2HmZc.png)
    
    Vertex,4,-2,7,0.1,0,0,-1,1,0,0,0.2,0.7,0,10,1,1,1,0.5,0,0,0.2,0,0,0,0,0,0,"センター",1,"",0,"",0,"",0,0,0,0,0,0,0,0,0,0
    Vertex,5,2,7,0.1,0,0,-1,1,1,0,0.2,0.7,0,10,1,1,1,0.5,0,0,0.2,0,0,0,0,0,0,"センター",1,"",0,"",0,"",0,0,0,0,0,0,0,0,0,0
    Vertex,6,-2,3,0.1,0,0,-1,1,0,1,0.2,0.7,0,10,1,1,1,0.5,0,0,0.2,0,0,0,0,0,0,"センター",1,"",0,"",0,"",0,0,0,0,0,0,0,0,0,0
    Vertex,7,2,3,0.1,0,0,-1,1,1,1,0.2,0.7,0,10,1,1,1,0.5,0,0,0.2,0,0,0,0,0,0,"センター",1,"",0,"",0,"",0,0,0,0,0,0,0,0,0,0

|    追加UV1_x|   追加UV1_y  |追加UV1_z   |     追加UV1_w|
| ----------- | ----------- | ----------- | ----------- |
|        0.2  |       0.7   |            0|         10  |

&emsp;&emsp;其中追加UV1的0.2，0.7没什么说的，但是，10呢？往上翻翻，10代表HSV，这个SHV是我们改变色相的关键。<br>&emsp;&emsp;继续来看追加UV2

|    追加UV2_x|   追加UV2_y  |追加UV2_z   |     追加UV2_w|
| ----------- | ----------- | ----------- | ----------- |
|       1  |       1   |           1|      0.5  |

&emsp;&emsp;这个xyz好理解，但是为什么追加w是0.5？不是说标准值是1么？宝宝~ 是1没错，但是，咋也不能被规矩限死啊，看看1的下场。
![image.png](https://s2.loli.net/2024/02/03/ZtDI5oY9CvjcOqU.png)
&emsp;&emsp;好大的！！所以0.5就刚刚合适，懂了吧~
&emsp;&emsp;然后看看追加UV3
|    追加UV3_x|   追加UV3_y  |追加UV3_z   |     追加UV3_w|
| ----------- | ----------- | ----------- | ----------- |
|       0  |   0  |         0.2|  0 |

&emsp;&emsp;弹出是什么呢？其实就是法线方向的偏移量，来张图看看吧~
![image.png](https://s2.loli.net/2024/02/03/Tl2Bua6UCc4hSJn.png)
&emsp;&emsp;眼睛好的小伙伴可以看出来，我把一个顶点改成1后，发光的部位就向前走了1个单位，就是这样。
&emsp;&emsp;接下来，就是制作表情~，制作UV表情的步骤建议自己搜搜，我懒了，其实更简单的办法就是，PE打开你要修改的模型，打开示例4，然后在示例4的色相表情上右键，复制，然后在你的要修改的模型那里粘贴，这是最简单的，然后把里面的顶点改成你修改过的就成。然后按照示例4的表情参数抄过去就成。
### 表情系列
&emsp;&emsp;有两种方式，控制材质和控制顶点。其实这个在MMD内重点是名称匹配即可，对于顶点和材质都一样，所以，你做顶点表情，把要改的放进去与做材质表情，把要改的材质放过去，大差不差，只是控制的范围罢了，具体可以看看示例文件以及SOUR的模型。<br>&emsp;&emsp;关于表情，只要名字是以下的，并且在对应控制栏里面填对数据，就可以（比如材质的话，你要在表情控制的材质里面，把反射度开到100以上）(嫌自己一个一个做麻烦的话，可去找找Emil大佬的汉化版插件，当然，你用日语我不反对)
    
    ・LightUp
    ・LightOff
    ・LightBlink
    ・LightBS
    ・LightUpE
    ・LightDuty
    ・LightMin
    ・LClockUp
    ・LClockDown

    通过 "LightUp "和 "LightOff "可以调节灯光强度。
    LightUp "可将光亮度提高三倍。
    如果使用 "LightOff"，灯光会在最大亮度时完全熄灭。
      
    使用虚拟表达式 "LightBlink "和 "LightBS"、
    LightBlink "和 "LightBS "虚拟表达式可用于控制个别型号的灯光闪烁。
    LightBlink "发出正弦波闪烁，"LightBS "发出方波闪烁。
    最大间隔为 10 秒。

    使用 "LightUpE "时，亮度以指数形式增加。
    最大增幅为 400 倍。

    通过 "LightDuty "可以改变闪烁的开/关比例。
    LightMin "可以设置闪烁时的最小亮度。

    "LClockUp "可加快闪烁周期，并通过下述顶点光功能控制光序、
    LClockUp "通过下述顶点光功能加快闪烁和光序列控制的周期时间。
    最大速度可提高六倍。
    "LClockDown "则相反地减慢闪烁周期。 最大速度为 1/6x。

---

## 后记
&emsp;&emsp;就这样吧，有意思的就这样。
