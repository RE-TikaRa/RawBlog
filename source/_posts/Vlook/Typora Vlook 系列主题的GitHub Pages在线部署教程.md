---
title: Typora Vlook 系列主题的GitHub Pages在线部署教程
date: 2026-02-10 00:58:09
tags:
  - Typora
  - Vlook
categories:
  - Vlook
abbrlink: 8443937e
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
sticky:
excerpt: "Typora Vlook 系列主题的GitHub Pages在线部署教程"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2028-02-10 00:58:09
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---

## 写在前面

{% notel blue NOTE %}

本文以 **VLOOK V2026.1** 为例。  

全文中的 `<yourhost>` 均表示你的站点地址。开始前请先确认站点类型，再进行替换。

{% endnotel %}

1. **自定义域名（根域）**：若将 `username.github.io` 绑定到 `custom.com`，则 `<yourhost>` 填写为 `custom.com`（不是 GitHub 原始域名）。
2. **自定义域名（项目路径）**：若站点地址为 `username.github.io/仓库名`，则 `<yourhost>` 填写为 `custom.com/仓库名`。
3. 在线字体下载：[点击下载](https://github.com/MadMaxChow/openfonts/releases/download/V2.0/web-font-V2.0.tar.gz)
4. 下文将 `VLOOK-released-V20xx.x` 统称为 **VLOOK 项目目录**。
5. 需要部署的目录统称为 **站点根目录**。
6. ==本文对应版本：V2026.1==

---

## Typora 端配置

### 1) 主题设置

1. 在 VLOOK 项目目录中找到 `themes-live` 文件夹，选择要使用的主题（可单选，也可全部）。
2. 将主题文件中的 `<yourhost>` 替换为你的实际站点地址（例如 `custom.com`）。
3. 把修改后的主题复制到 Typora 的主题目录。

![Theme.png](https://free.picui.cn/free/2026/02/10/698a2f57269f6.png)

![ThemeFolder.png](https://free.picui.cn/free/2026/02/10/698a2f571827a.png)

### 2) 导出设置

1. 在 VLOOK 项目目录中找到 `plugin-live` 文件夹，打开 `plugin-live.txt`。
2. 使用 VS Code 或其他文本编辑器，将 `<yourhost>` 替换为你的实际站点地址（例如 `custom.com`）。
3. 按照 Vlook-live 的说明将配置导入 Typora，并选择你刚刚修改的主题。

![plugin-live.txt.png](https://free.picui.cn/free/2026/02/10/698a2f5724b47.png)

![Vlook-Live.png](https://free.picui.cn/free/2026/02/10/698a2f5a63e83.png)

---

## 站点根目录配置

### 1) 复制 V2026.1 资源

1. 在 VLOOK 项目目录中找到 `themes-live\V2026.1` 和 `plugin-live\V2026.1`。
2. 将这两个 `V2026.1` 文件夹复制到站点根目录。
3. 将这些文件夹内 **所有 CSS 文件** 的 `<yourhost>` 统一替换为你的实际站点地址（例如 `custom.com`）。

![css.png](https://free.picui.cn/free/2026/02/10/698a2f56ac0cb.png)

### 2) 配置字体文件

1. 在站点根目录创建 `fonts` 文件夹。
2. 下载字体包：[点击下载](https://github.com/MadMaxChow/openfonts/releases/download/V2.0/web-font-V2.0.tar.gz)。
3. 解压后将其中的 `s` 和 `v` 两个文件夹复制到 `fonts` 目录下。

![fonts.png](https://free.picui.cn/free/2026/02/10/698a2f56e7926.png)

---

## 完成与发布

1. 至此，VLOOK 在线部署所需配置已完成。
2. 后续写作建议参考 Vlook 官方示例。
3. 导出时选择 `vlook-live`，生成 HTML 后推送到仓库。
4. 最后启用 **GitHub Pages**，即可访问站点。

## 可参考的项目结构

```mermaid
flowchart LR
    A[站点根目录] --> B(V2026.1 文件夹)
    A --> C(fonts 文件夹)
    C --> D[s文件夹]
    C --> E[v文件夹]
    B --> |包含| F(fs-xxx-min.css)
    B --> |包含| G(vlook-xxx.css)
    B --> |包含| K(xxx.js)
    B --> |包含| L(lang 文件夹)
    K --> M(VLOOK 项目目录中<br>plugin-live\V2026.1<br>路径下的所有内容)
    L --> M
    A --> I(_post 文件夹)
    I --> J(可存放其他文章 HTML，在 index.html 中使用相对路径引用)
    A --> H(index.html)
    TIP01(GitHub Pages 必需入口，可作为首页使用) --> H
```
