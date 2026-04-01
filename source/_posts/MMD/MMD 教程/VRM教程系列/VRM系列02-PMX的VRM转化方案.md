---
title: VRM系列02-PMX的VRM转化方案
categories:
  - MMD
  - MMD 教程
  - VRM教程系列
abbrlink: 93a98ac8
date: 2024-06-09 10:57:59
tags: 
  - PMX
  - VRM
---
## 前言
&emsp;&emsp;是我习惯性的PMX转为VRM方案，用到了Unity，虽然有人说Blender插件也能做，但是我不习惯用Blender，于是用了Unity。本教程基于Windows10系统，不同系统或是软件版本间差异请自行百度，同时，此教程是我个人的方案展示，请自行斟酌是否适用。 ***还有就是，请一定要遵守原作者的RM！！！！！***

<!--more-->

---

&emsp;&emsp;【附加】：截止到写稿，非常不建议使用aplaybox的在线转换，除非你自己能修，也愿意花时间去修，展示如下，图一是Blender中的渲染，可以见到miku的表情有问题，图二是VSeeFace，可以见到透明关系有问题：
![无修改转换展示01.png](https://s2.loli.net/2024/06/10/Jt4RmPG1inzVso5.png)
![无修改转换展示02.png](https://s2.loli.net/2024/06/10/GqdHf53KJPsVMx1.png)
&emsp;&emsp;综上，如果你非常有耐心，去一点一点修复，也不是不能用，但你有那功夫，还不如把教程看完<br>&emsp;&emsp;【附加2】：针对下文中没有secondary的情况，据我了解后得知是我操作顺序有误，secondary是VRM的，所以，建议的操作流程是，修改完贴图着色之后就导出一遍VRM，然后再导入，然后再在这个VRM基础之上修正物理和表情，导出的方法下文表情修正前有，可以翻翻自己看。在修改物理前如果没有导出VRM，那就不会有secondary，所以，导出VRM，再导入，这样，就会有secondary了。不建议自己添加secondary组。 ***综上，操作步骤建议是第一步——第二步——第四步——第三步——第五步——第四步。不建议自己添加secondary组！！第一遍第三步之后导入VRM，那时候就有了Secondary，就不用创建了！！！！***

---
## Stuff
&emsp;&emsp;Model：REM's SEKAI Style Hatsune Miku VS - ver.1.2<br>&emsp;&ensp;&emsp;&emsp;By：REMmaple<br>&emsp;&emsp;Model：YYB Hatsune Miku_10th<br>&emsp;&ensp;&emsp;&emsp;By：REMmaple<br>&emsp;&ensp;&emsp;&emsp;Tex Editor：三雾

---

## 准备
&emsp;&emsp;1、[Unity](https://unity.cn/)：版本均可，只要与所使用的UniVRM插件所兼容即可<br>&emsp;&ensp;&emsp;&emsp;&emsp;&emsp;&emsp;（建议同时注册好UnityID方便后续使用）<br>&emsp;&emsp;2、[UniVRM](https://github.com/vrm-c/UniVRM)：最新版就好<br>&emsp;&emsp;3、[MMD4Mecanim](http://stereoarts.jp/)：同样是最新版就好<br>&emsp;&emsp;4、[PmxEditor](https://kkhk22.seesaa.net/category/14045227-1.html)：非必须，用来修改和检查PMX有没有错误<br><br>&emsp;&emsp;此处所有的下载链接均是官方网址，若下载困难，此处可以提供截止到写稿为止windows平台最新版本软件或是我用的版本的百度网盘的下载方式，其中UnityHub和Unity这两个东西，就相当于游戏启动器和游戏本体的关系大致，选择一个下载即可。当然，我更推荐于UnityHub，可以免去引擎安装时的BUG，并且修改和创建新项目都很方便。
### 资源包下载：
&emsp;&emsp;[点击下载](https://pan.baidu.com/s/187sXRmK9fsmKL3Ad-U6C6A?pwd=rwa7)

---

## 关于准备项目的一些附加事项
&emsp;&emsp;1、关于Unity的版本：<br>&emsp;&ensp;&emsp;&emsp;版本必修与插件适配，像是UniVRM插件版本介绍页中写道 ***“The UniVRM supports Unity 2021.3 LTS or later.”*** 则是要求版本必须2021.3长期支持版及之后的版本。故在选择是切记选择合适的版本。<br>&emsp;&emsp;2、关于UniVRM的版本：<br>&emsp;&ensp;&emsp;&emsp;因为VRM现在有0.x和1.0两个版本，所以本插件也有两个版本。

    VRM 1.0：
    VRM_Samples
    VRM 0.x：
    UniVRM_Samples

&emsp;&ensp;&emsp;&emsp;所以请根据自己需要下载（我一般是都下载，两个插件不冲突）
![image.png](https://s2.loli.net/2024/06/10/NumwoEnAQgzlUpK.png)

---

## 操作步骤
### &emsp;&emsp;第一步：新建Unity项目以及骨骼修复
&emsp;&emsp;选择 ***“3D-核心模板”*** ，按图示填写后，点击 ***“创建项目”*** 
![image.png](https://s2.loli.net/2024/06/10/trY4cvApKI6f5yQ.png)
&emsp;&emsp;等他自己初始化项目完成，完成后会自动打开，没自动打开的话可以自己点一下
![image.png](https://s2.loli.net/2024/06/10/fKPUdhQy35qRDVg.png)
&emsp;&emsp;打开项目之后会有这个界面
![image.png](https://s2.loli.net/2024/06/10/zIer6cVGiWHDlUp.png)
&emsp;&emsp;将我们下载的插件一个一个拖进来安装好（插件后缀是.unitypackage）
&emsp;&emsp;UniVRM.unitypackage这个拖进去会打开这个界面，点击全部后点击导入即可
![image.png](https://s2.loli.net/2024/06/10/5Qo49aPDMvilswH.png)
&emsp;&emsp;VRM.unitypackage这个拖进去会打开这个界面，点击全部后点击导入即可（注：不管是否勾选，点一下全部点击导入就好）
![Clip_2024-06-10_12-14-47.png](https://s2.loli.net/2024/06/10/7tigUvqQr2maVj4.png)
&emsp;&emsp;MMD4Mecanim.unitypackage这个拖进去会打开这个界面，点击全部后点击导入即可
![Clip_2024-06-10_12-20-15.png](https://s2.loli.net/2024/06/10/aZUwLNpcxfXAiIK.png)
&emsp;&emsp;出现这个点击“yes”即可
![image.png](https://s2.loli.net/2024/06/10/pzXyuG9OEBQoRfN.png)
&emsp;&emsp;然后右键新建两个文件夹来放我们的模型，一个放MMD模型，另一个放导出的VRM模型
![image.png](https://s2.loli.net/2024/06/10/tln1WACVZS8M2f9.png)
&emsp;&emsp;然后双击打开我们存放MMD模型的文件夹，把我们需要修改的模型包括贴图一整个文件夹塞进去，这时文件架构就变成了

    Assets
        ├─Mode-MMD
        │  └─REM式プロセカ風初音ミクVS - ver.1.2
        │      └─REM's SEKAI Style Hatsune Miku VS - ver.1.2
        │          └─REM's SEKAI Style Hatsune Miku VS - ver.1.2
        │              ├─albd
        │              ├─omake
        │              └─spt
&emsp;&emsp;熟悉REM式的MIKU这个模型的同学，就可以看出来，把这个拖进来就是把REM式MIKU这所有的文件夹直接塞在了Assets文件夹下我们刚刚创建的存放MMD模型的文件夹下。<br>&emsp;&emsp;然后找到我们的PMX模型
![image.png](https://s2.loli.net/2024/06/10/G6v5QdJy3EpgO2W.png)
&emsp;&emsp;此时我们要用REM式プロセカ風初音ミクVS.pmx这个模型来创建VRM，所以我们点击同名的REM式プロセカ風初音ミクVS_袖無し.MMD4Mecanim.asset，就是模型后面那个蓝色的立方体图标的那个文件。（图片中选中的那个文件），在右边打开的信息窗中，首先 ***阅读模型声明*** ，然后把下面三个可选项都勾选。然后点击 ***Argee***
![image.png](https://s2.loli.net/2024/06/10/MWiE68v1oInP7qa.png)
&emsp;&emsp;在下面这个窗口中点 ***Process*** 
![image.png](https://s2.loli.net/2024/06/10/AGMt3Ss5qLbBzIZ.png)
&emsp;&emsp;会出现这个窗口，不用管，等一小会，他会自己关掉，然后Unity会开始走进度条，继续等一下
![image.png](https://s2.loli.net/2024/06/10/dvIGslJPb2joaKy.png)
![image.png](https://s2.loli.net/2024/06/10/BwzxQs6C8ePrXpg.png)
&emsp;&emsp;然后我们的资产管理器就多了一堆东西
![image.png](https://s2.loli.net/2024/06/10/nxVGXf1O3jWdpP5.png)
&emsp;&emsp;接下来我们把那个带一个看起来像播放键的东西塞到我们的层级里面，这样你就发现了我们屏幕中出现了一只MIKU，如下图：
![image.png](https://s2.loli.net/2024/06/10/m64pTjay7sPNLk5.png)
&emsp;&emsp;然后点击 ***Rig*** ，选择 ***人型*** 
![Clip_2024-06-10_13-42-42.png](https://s2.loli.net/2024/06/10/hZROS9MboqXaHJv.png)
&emsp;&emsp;然后点击 ***应用***
![Clip_2024-06-10_13-44-14.png](https://s2.loli.net/2024/06/10/UDemZrMx3nSBEJw.png)
&emsp;&emsp;等他走完进度条之后点 ***配置***，然后点 ***配置 Avatar*** 
![image.png](https://s2.loli.net/2024/06/10/MX8SuTIyctxZghO.png)
&emsp;&emsp;在这个界面里，对关节处的骨骼做一个校正（就是，点一下小绿人身上的每一个圈圈，看看模型是否对应到，比如点小绿人的左肩，看看骨骼是否对应到MIKU的左肩，不对的点击列表修改就行，没有对应的就选最上面的None）
![image.png](https://s2.loli.net/2024/06/10/EjeDihCp5WqA86t.png)
对应完之后往下翻一下，先点击 ***Apply*** ，再点击 ***Done***
![image.png](https://s2.loli.net/2024/06/10/C2OqisXPWNUVnjZ.png)
### &emsp;&emsp;第二步：材质修复
&emsp;&emsp;但是看起来衣服的颜色还有肤色什么的有点小差别，unity中有点偏黄（大概
![image.png](https://s2.loli.net/2024/06/10/QrkMuzi62cyJmwW.png)
![image.png](https://s2.loli.net/2024/06/10/OdFIgQKa8ycfn2T.png)
&emsp;&emsp;接下来解释调整材质的时间了，先来到 ***Materials*** 文件夹下
![image.png](https://s2.loli.net/2024/06/10/nCriu5zsR6g9vU4.png)
&emsp;&emsp;首先全选材质，然后在 ***Shader*** 中选择 ***VRM***，然后再选择 ***MTOON*** 
![image.png](https://s2.loli.net/2024/06/10/Od3vcKgPsRyfakY.png)
&emsp;&emsp;然后根据MMD中的模型细节进行调整就好，每一项参数和每一个材质都可以单独实施（说不定会碰撞到不一样的火花）
![image.png](https://s2.loli.net/2024/06/10/WpT8BrsJxV6IDLe.png)
&emsp;&emsp;基础参数讲解如下：

    Rendering：渲染
      Mode：模式
        Rendering Type：渲染类型
          Opaque：不透明
          Cutout：剪切
          Transparent：透明
          TransparentWithZWrite：使用ZWrite透明
        Cull Mode：关于透明的遮挡方式（我自己感觉
          Back：背面剔除
          Front：正面剔除 
          Off：关闭
      Color：颜色
        Texture：纹理
          Lit Color,Alpha：发光色彩，透明
          Shade Color：阴影颜色
      Lighting：光照
        Shading Toony：TOONY 着色
        Normal Map：法线映射
      Emission：发光
        MatCap：球面朝向映射
      Rim：边缘光
        Color：边缘光颜色
        Lighting Mix：光照混合
        Fresnel Power：菲涅耳功率
        Lift：提升
      OutLine：轮廓线
        Width：宽度
          mode：模式
            None：没有一个
            WorldCoordinates：世界坐标
            ScreenCoordinates：屏幕坐标
        Color：颜色

![image.png](https://s2.loli.net/2024/06/10/3o7hZIeiY9NKPxG.png)
### &emsp;&emsp;第三步：物理修复
&emsp;&emsp;接下来就是调整一些细节了，比如：物理<br>&emsp;&emsp;展开层级下的 ***U_Char*** 选择 ***secondary*** ，~~若没有，自己创建一个对象与这个同名也行~~ ***这里先导出VRM，再导入VRM！！！！*** 
![image.png](https://s2.loli.net/2024/06/10/y3Qb5ZEtJuhSYCg.png)
&emsp;&emsp;接下来我们先做头发之类的物理效果，选择第一个后会出现这样的东西![image.png](https://s2.loli.net/2024/06/10/IPrYmcnfHNpkt68.png)
&emsp;&emsp;基础参数讲解：

| 原文 | 翻译 | 作用 |
|---|---|---|
| 注释 | 注释 | 用来写名字之类的 |
| Gizmo Color | 修改器颜色 | 用来看那个碰撞球的颜色 |
| Settings | 设置 | 就，，设置 |
| Stiffness Force | 刚度力 | 感觉像MMD的阻尼那种东西，这个值越大，越不容易被触发物理效果 |
| Gravity Power | 重力功率 | 重力大小，相同质量的东西，越大掉的越快 |
| Gravity Dir | 重力方向 | 就。。方向 |
| Drag Force | 阻力 | 个人感觉也和阻尼差不多诶。。。 |
| 中心 | 中心 | 不知道咋描述，自己试试 |
| Root Bones | 根骨骼 | 就是想让哪些骨骼产生物理效果 |
| Collision | 碰撞 | 碰撞球 |
| Hit Radius | 命中半径 | 碰撞球的大小 |
| Collider Groups | 碰撞器组 | 与骨骼产生交互的地方 |
| Update Type | 更新类型 | 不建议动 |

&emsp;&emsp;小提示：对于那种父子级相联系的一串骨骼，直接把父级塞到Root Bones中就行，子级不用设置，这样一大串就做完了，如下图所示
![image.png](https://s2.loli.net/2024/06/10/e6oDryZBQYp18ES.png)
&emsp;&emsp;其余你们自己添加，然后设置参数就好，然后按下图所示的步骤应用参数。
![image.png](https://s2.loli.net/2024/06/10/EOnXj6VsFMRguyS.png)
&emsp;&emsp;接下来设置四肢之类的碰撞体积<br>&emsp;&emsp;选中我们要添加的骨骼，我这里以腿为展示，添加组件，选择成 ***VRM Spring Bone Collider Group*** ，然后就会有下图
![image.png](https://s2.loli.net/2024/06/10/kz4HU8YhPZA7Dnt.png)
&emsp;&emsp;之后就添加碰撞球啊，调整大小和位置啊什么的，由于骨骼长度问题，而这个也只有球状的碰撞，所以难免会在一个骨骼上添加多个球，添加球的逻辑为：尽量不要重复，稍微大于材质表面一点点就好，球与球之间尽量不要有重叠部分，然后继续和上一步一样，应用参数。但是此刻那个黄色的物理和这个紫色的碰撞体积之间依旧不会发生交互，所以需要设置一下，回到需要和这个紫色球发生碰撞的组，就刚才设置了黄色球的地方，把我们的设置了紫色球的骨骼拖到Collider Groups上面即可。
![image.png](https://s2.loli.net/2024/06/10/Km1zABTqSWtkoab.png)
### &emsp;&emsp;第四步：导出与再次导入
&emsp;&emsp;处理好这些就可以先导出一遍了（导出之后才可以做表情），导出先选中模型，然后点VRM0，然后如果是Apose，就点一下这个TPOSE（不管是不是Apose，其实都建议点一遍）
![image.png](https://s2.loli.net/2024/06/10/TGnlcbf8BQ3gXoF.png)
&emsp;&emsp;然后点Export VRM0.X，在弹出的窗口中如实填写信息，我用YYB 10th MIKU演示如下：
![image.png](https://s2.loli.net/2024/06/10/XvGe2HJUcibWO4l.png)
&emsp;&emsp;其余例如缩略图等按照自己喜好便可，填写完成之后点最下面export即可，然后等待一段时间，就可以看到导出的模型了。<br>&emsp;&emsp;将层级中的模型删掉。把导出的VRM继续塞到 ***Assets*** 中，然后把这个拖到层级那里。
![image.png](https://s2.loli.net/2024/06/10/wbnvOZMeqmdSE1j.png)
&emsp;&emsp;这样就导入成功了
### &emsp;&emsp;第五步：修复表情
&emsp;&emsp;然后找到名字中含有BlendShapes的文件夹，比如此刻我的就是YYB Hatsune Miku_10th_v1.02_toonchange.BlendShapes，打开之后会看到这种东西。
![image.png](https://s2.loli.net/2024/06/10/IDdtrHbRv7LgWYB.png)
&emsp;&emsp;选中BlendShape，将AEIOU这几个表情在下面对应修一下，对应表情，比如点一下“A”，然后在U_Char_2里面把あ拉倒最大，然后IUEO等等，口型必须其余看心情，流程如下：
![image.png](https://s2.loli.net/2024/06/10/nPK5kThbXwIH2yq.png)
&emsp;&emsp;这些做完之后就完了，就可以到出啦~ 导出方法和刚才一样，这里就不再写啦~~ 祝各位玩得愉快

---

## 后记
&emsp;&emsp;1、如何添加许可证：<br>&emsp;&ensp;&emsp;&emsp;首先在UnityHub上登录你的账号，如果是第一次使用，大概率会出现如下所示，如果没有下图一的图示，请参照本步骤后续几张图，打开许可证界面后从第二步开始继续操作
![image.png](https://s2.loli.net/2024/06/10/tT72RAr8v4ZeJMm.png)
![image.png](https://s2.loli.net/2024/06/10/dORryQaIGixzLeg.png)
![image.png](https://s2.loli.net/2024/06/10/Sn6coi8sdZw1x47.png)
&emsp;&ensp;&emsp;&emsp;点击 ***管理许可证*** ，再打开的窗口中点击 ***添加*** 
![image.png](https://s2.loli.net/2024/06/10/3e8VdOLIfNUukph.png)
&emsp;&ensp;&emsp;&emsp;点击 ***获取免费的个人版许可证***
![image.png](https://s2.loli.net/2024/06/10/daNgETMYDwKb7LR.png)
&emsp;&ensp;&emsp;&emsp;点击 ***同意并取得个人版授权***
![image.png](https://s2.loli.net/2024/06/10/kvgCVXGbaUwNiyj.png)
&emsp;&emsp;2、遇到无法创建项目的情况，尝试取消勾选版本管理
![image.png](https://s2.loli.net/2024/06/10/MHayECXigFKjeIN.png)
&emsp;&emsp;3、如果在配置骨骼时遇到如下报错，并且点击配置没有任何反应

    Cannot configure avatar, inspector is locked
    UnityEngine.GUIUtility:ProcessEvent (int,intptr,bool&)

![Clip_2024-06-10_18-59-18.png](https://s2.loli.net/2024/06/10/qhv5gducpmso9Kx.png)
&emsp;&emsp;可以把这个锁点一下，然后就正常了
![Clip_2024-06-10_19-04-13.png](https://s2.loli.net/2024/06/10/bwdjZaTg56VGLkf.png)