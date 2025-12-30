---
title: LaTeX学习日志01-前期准备
thumbnail: 'https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png'
excerpt: LaTeX学习日志01-前期准备 包括安装，环境配置等
banner: 'https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png'
password: ''
abstract: '有东西被加密了, 请输入密码查看.'
message: '您好, 这里需要密码.'
wrong_pass_message: '抱歉, 这个密码看着不太对, 请再试试.'
wrong_hash_message: '抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.'
expires: '10000-01-01 07:59:59'
tags:
  - LaTeX
categories:
  - Latex
abbrlink: 828fd9e
date: 2025-12-27 07:54:10
sticky:
---

## 前言
LaTeX 是基于 TeX 的排版系统，用纯文本加命令写作，排版更统一，避免反复调样式。它会编译成高质量 PDF，尤其适合公式、参考文献和长文档，也便于后期统一调整格式。写作时可以更专注内容，把样式交给工具处理。本次我们将使用 [Tectonic](https://tectonic-typesetting.github.io/en-US/) 这个 LaTeX 引擎，加上 LaTeX Workshop 这个 VS Code 插件来学习使用。

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 安装 Tectonic
打开 [Tectonic](https://tectonic-typesetting.github.io/en-US/) 的官网，点击 `Install Tectonic 0.15.0`，进入下载安装页面。

![image-20251228011823010](https://s2.loli.net/2025/12/28/3elv2oatsxZgmYb.png)

它会自行判断你的电脑环境，给出相应的下载方式，不过我更推荐在 `GitHub` 页面下载。点击 [find the latest released binaries on GitHub](https://github.com/tectonic-typesetting/tectonic/releases/tag/tectonic@0.15.0) 进入 GitHub 发行页。

![image-20251228012511285](https://s2.loli.net/2025/12/28/4PCzItrV68sagBY.png)

打开发布页后，往下翻找到 `Assets`。

![Assets](https://s2.loli.net/2025/12/28/Rn1QDBi3Cj2LNyg.png)

如果电脑环境是 Windows 11 x64（Ryzen 9），那么选择 [tectonic-0.15.0-x86_64-pc-windows-msvc.zip](https://github.com/tectonic-typesetting/tectonic/releases/download/tectonic@0.15.0/tectonic-0.15.0-x86_64-pc-windows-msvc.zip) 是最佳选择。MSVC 版本是官方 Windows 原生构建，兼容性最好。点击后会下载一个压缩包，内容如下图：

![image-20251228013233070](https://s2.loli.net/2025/12/28/WU738GftNuLdqkF.png)

把这个文件放在一个自己能清楚记住的位置，我放在了 `C:\Tectonic`，即在 C 盘下创建一个 Tectonic 文件夹来存放这个 exe。然后把这个路径加入环境变量。

![image-20251228014324129](https://s2.loli.net/2025/12/28/ReU58Z6z7FwsTuC.png)

至此 Tectonic 引擎就配置好了，但只有引擎还不够。我们需要 VS Code 和 LaTeX Workshop 来使用它。打开 VS Code 的扩展，搜索并安装 LaTeX Workshop 插件。

![image-20251228014633517](https://s2.loli.net/2025/12/28/zbS2J97xGIoYdMc.png)

安装完成后，使用快捷键 <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> 打开用户设置（JSON）。

![image-20251228020954286](https://s2.loli.net/2025/12/28/W5dylr1eZMQqfvH.png)

找到下面类似的配置，没有的话可以直接复制我的，再按需调整。注意 JSON 语法，不确定就发给 AI，让它帮你检查。
```json
{
    "workbench.editorAssociations": {
        "*.pdf": "latex-workshop-pdf-hook"
    },
    "latex-workshop.intellisense.biblatexJSON.replace": {},
    "latex-workshop.latex.tools": [
        {
            "name": "tectonic",
            "command": "tectonic",
            "args": [
                "--synctex",
                "--keep-logs",
                "--print",
                "%DOC%.tex"
            ],
            "env": {}
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "tectonic",
            "tools": [
                "tectonic"            ]
        }
    ],
    "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",
    "[latex]": {
        "editor.formatOnSave": false
    },
    "latex-workshop.latex.autoBuild.run": "onSave",
    "latex-workshop.latex.autoBuild.interval": 500
}
```

到此设置就完成了。欢迎来到 LaTeX 的规范化世界。
