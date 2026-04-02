---
title: VRM系列01-VRM转换FBX的若干事项
date: 2024-04-01 13:00:32
tags:
  - VRM
  - FBX
categories:
  - MMD
  - MMD 教程
  - VRM教程系列
abbrlink: 7a433340
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
excerpt: "这是文章摘要 This is the excerpt of the post"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2026-04-01 13:00:32
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---

# 前言
&emsp;&emsp;最近在群里潜水的时候，看到了有人问VRM如何转换成FBX。我心想，拿BL直接转不就好了，结果有人告诉我不能直接转，会丢贴图，我还不信，去试了一下，结果是真的，然后研究了一下，发现了一个转换的好方法。本方法分两种：正常版和歪门邪道版，可以都看一下然后选择自己喜欢的就行。（截止到写稿，非常不建议使用aplaybox的在线转换，除非你自己能修，也愿意花时间去修）

<!--more-->

---

# 问题查看
&emsp;&emsp;首先来看一看这个VRM直接转FBX（使用VRM插件直接导入，然后用better FBX勾选复制纹理导出）
![导入.png](https://s2.loli.net/2024/04/01/qnisZvdej68QTg7.png)
![复制纹理better.png](https://s2.loli.net/2024/04/01/TKfFzblNd9tOu7H.png)
&emsp;&emsp;显而易见的贴图没了，众所周知，FBX允许存储贴图文件，那问题出在哪里呢，不急，我们换到VRM的节点与FBX的对比看看
![VRM节点.png](https://s2.loli.net/2024/04/01/Z3crOXu7GHidK5R.png)
![FBX节点.png](https://s2.loli.net/2024/04/01/VN1vUkXJSK7qBC2.png)
&emsp;&emsp;非常恐怖的节点，但是可以看出了问题，VRM全部是由MTOON的节点进行渲染，而FBX只有原理化BSDF。那么也就是说，我只要把MTOON的全部换成FBX的就好。

---

# 正常篇
&emsp;&emsp;正如上文中所说FBX和VRM节点不同导致的，那么我们只要换节点就好了。导入VRM，然后删节点，把对应节点换过去就好。就像下图这样（为了方便我换几个意思一下就行）
![image.png](https://s2.loli.net/2024/04/01/whupi9vJKe576Cb.png)
&emsp;&emsp;然后转换试试
![image.png](https://s2.loli.net/2024/04/01/LplYv2cG3gVIPRA.png)
&emsp;&emsp;看起来不错，正常篇就先到这

---

# 后记（VRM系列）
&emsp;&emsp;我们在直接连完材质节点后，发现如果说是白模用shader的底色做了修改，那么在此处重连节点会有一定几率变成白模，那么可以将节点连接成这样
![image.png](https://s2.loli.net/2024/04/02/B4bvycnxtkGdLhF.png)
&emsp;&emsp;在中间加一个
![image.png](https://s2.loli.net/2024/04/02/F2DN7SAPkQigJTn.png)
&emsp;&emsp;然后把你在shader中的HSV什么的复制过来就成
&emsp;&emsp;（补充：在测试之后仍有一定几率是白模，所以，可以先去PS之类的直接处理好贴图再塞回来，这样会方便很多）

---

# 歪门邪道篇（未经测试，BUG有几率）
&emsp;&emsp;首先呢，我们现将自己的VRM后缀改成 ***.glb*** 然后导入。
![image.png](https://s2.loli.net/2024/04/01/oRKgC6AmNZUy3af.png)
&emsp;&emsp;这下所有的MTOON节点就换掉了，然后，我们在这里选择解包资源，
![image.png](https://s2.loli.net/2024/04/01/VWPqOb5tUaMs4hv.png)
&emsp;&emsp;在弹出选项里选择第二个，这样我们就能在Blender根目录下找到一个 ***textures*** 的文件夹，这个是贴图文件夹。如果找不到，推荐使用everything搜一下
![image.png](https://s2.loli.net/2024/04/01/Iehqnx1QOyBXNgM.png)
&emsp;&emsp;接下来我们回到BL，找到脚本，，然后下载这个脚本
    
    https://github.com/LadyAska/Blender

    这个脚本的用途是用于在Blender中自动化材质设置的Python脚本。它遍历所有的材质，如果材质使用了节点系统，它会进行一些操作来修改这些材质。

    首先，它定义了一些变量，包括mixshader（混合着色器节点）、transparent（透明BSDF节点）、light（光线路径节点）、emission（发射节点）、image（纹理图像节点）和output（输出材质节点）。

    然后，它检查是否存在mixshader和output节点，如果不存在，则跳过当前循环。
    
    接下来，它创建一个新的"Principled BSDF"节点，并移除image、light和emission节点的输出链接。
    
    然后，它将image节点的输出连接到新创建的principled节点的输入，并将principled节点的输出连接到output节点的输入。
    
    最后，它移除了unnecessary的节点，包括mixshader、transparent、light和emission节点。
    
    在最后一部分，它尝试将所有的图片文件的路径设置为'C:/Blender/textures/*.png'，如果出现异常，则忽略。<br>&emsp;&emsp;

![image.png](https://s2.loli.net/2024/04/01/CGjQeq1AJtHhN64.png)
&emsp;&emsp;点脚本，然后点打开，然后把刚才下载的PY文件塞进来
![image.png](https://s2.loli.net/2024/04/01/j2hRrPeZH4qFmJl.png)
&emsp;&emsp;点一下那个播放按钮就可以批量转换材质了
![image.png](https://s2.loli.net/2024/04/01/ftiyQajSCkJN2sl.png)
&emsp;&emsp;导出配置和我的一样就行，基本就木有啥问题啦~

---

# 后记（glb系列）
## BUG修复01
&emsp;&emsp;进过多次测试后，我发现，如果说是VROID的shader底色那一块做了修改，而模型贴图没改，那么打包出来的贴图也是没有shader的（也就是原始贴图之类的）。然后在glb那一块批量处理完之后我发现了一个节点
![image.png](https://s2.loli.net/2024/04/01/TkaRSZ8qfuzBrIv.png)
&emsp;&emsp;又在用miu老师的Vroid2Pmx做转换时，看到了这么一句话
![截图.png](https://s2.loli.net/2024/04/01/5bZyDokOifNdT8t.png)

    **WARNING**
    由于基本颜色不是白色，因此执行加法合成。材料名称:NO0_001_01_Bottoms_01_CLOTH

&emsp;&emsp;突然就明白了这个东西，将原始图一改成图二后
![image.png](https://s2.loli.net/2024/04/01/x9AWKlvJRICufZT.png)
![image.png](https://s2.loli.net/2024/04/01/EejkGX1SFOAhrcJ.png)
&emsp;&emsp;原始的白模也就修复成功了
## BUG修复02
&emsp;&emsp;针对于此处的白模，还有一种处理方式就是修改贴图，因为在miu老师的Vroid2Pmx中就是做了加法合成，那么我们可以在提取好贴图之后去PS之类的重新正片叠底一下颜色，此处这个为最后处理办法，将处理好的贴图再去BL贴一下，但是会比较麻烦。
