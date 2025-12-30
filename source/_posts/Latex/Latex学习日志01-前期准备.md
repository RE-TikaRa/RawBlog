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
LaTeX 是基于 TeX 的排版系统，用纯文本加命令写作，排版统一且可复用。它会编译为高质量 PDF，尤其适合公式、参考文献和长文档，也便于后期统一调整格式。写作时可更专注内容，把样式交给工具处理。本文记录在 Windows 11 上使用 Tectonic + VS Code + LaTeX Workshop 的前期准备流程。

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 准备清单
- Tectonic（LaTeX 引擎）
- VS Code
- LaTeX Workshop 插件
- 环境变量 Path（用于命令行调用）

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 安装 Tectonic
1. 打开 [Tectonic](https://tectonic-typesetting.github.io/en-US/) 官网，点击 `Install Tectonic 0.15.0` 进入安装页面。

![image-20251228011823010](https://s2.loli.net/2025/12/28/3elv2oatsxZgmYb.png)

2. 我更推荐在 GitHub Release 下载。点击 [find the latest released binaries on GitHub](https://github.com/tectonic-typesetting/tectonic/releases/tag/tectonic@0.15.0) 进入发行页。

![image-20251228012511285](https://s2.loli.net/2025/12/28/4PCzItrV68sagBY.png)

3. 在发布页找到 `Assets`。

![Assets](https://s2.loli.net/2025/12/28/Rn1QDBi3Cj2LNyg.png)

4. Windows 11 x64 建议下载 `tectonic-0.15.0-x86_64-pc-windows-msvc.zip`（官方 MSVC 原生构建，兼容性最好）。

![image-20251228013233070](https://s2.loli.net/2025/12/28/WU738GftNuLdqkF.png)

5. 解压后将 `tectonic.exe` 放到固定路径，例如 `C:\Tectonic`。
6. 把该路径加入系统环境变量 `Path`。

![image-20251228014324129](https://s2.loli.net/2025/12/28/ReU58Z6z7FwsTuC.png)

7. （可选）命令行验证：`tectonic --version`。

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 安装 VS Code 与 LaTeX Workshop
在 VS Code 扩展中搜索并安装 LaTeX Workshop 插件。

![image-20251228014633517](https://s2.loli.net/2025/12/28/zbS2J97xGIoYdMc.png)

安装完成后，使用快捷键 <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> 打开用户设置（JSON）。

![image-20251228020954286](https://s2.loli.net/2025/12/28/W5dylr1eZMQqfvH.png)

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 配置 LaTeX Workshop

找到下面类似的配置，没有的话可以直接复制并按需调整。注意 JSON 语法，不确定就发给 AI 帮你检查。
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
      "tools": ["tectonic"]
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

完成后保存即可。之后保存 `.tex` 文件会自动调用 Tectonic 编译，并在 VS Code 内部预览 PDF。