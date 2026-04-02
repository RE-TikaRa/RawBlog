---
title: Linux基础-NANO使用方法
date: 2026-02-10 23:50:52
tags:
  - Linux
  - NANO
categories:
  - Linux基础
abbrlink: 83c08d17
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
sticky:
excerpt: "NANO使用方法"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2031-02-10 23:50:52
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---

## 简介

Nano 是 Linux/Unix 终端里非常常见的轻量级文本编辑器。它最大的特点是直观：打开即可输入，底部直接显示快捷键提示，适合快速改配置、写脚本和处理普通文本。

相比 Vim/Emacs，Nano 学习曲线更平缓；如果你需要的是“快速编辑并保存退出”，Nano 往往更高效。

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 安装与版本检查

多数发行版默认已经安装 Nano，可先检查版本：

```bash
nano --version
```

常见安装方式：

```bash
# Debian / Ubuntu
sudo apt update
sudo apt install nano

# Fedora / RHEL / CentOS Stream
sudo dnf install nano

# Arch Linux
sudo pacman -S nano
```


<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 启动与界面

启动命令：

```bash
nano [文件名]
```

常见用法：

- 打开已有文件：`nano example.txt`
- 创建新文件：`nano newfile.txt`
- 不带文件名启动：`nano`（保存时再命名）

界面结构：

- 顶部状态栏：文件名与修改状态
- 中间编辑区：正文内容
- 底部提示栏：快捷键说明

按键符号约定：

- `^` 代表 `Ctrl`
- `M-` 代表 `Alt`（Meta）

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 常用快捷键

| 快捷键 | 功能 |
| --- | --- |
| Ctrl+X | 退出（会提示是否保存） |
| Ctrl+O | 保存文件（Write Out） |
| Ctrl+W | 查找 |
| Ctrl+\ | 查找并替换 |
| Ctrl+R | 读取文件到当前缓冲区 |
| Ctrl+K | 剪切当前行或选区 |
| Ctrl+U | 粘贴 |
| Ctrl+C | 显示光标位置（行/列） |
| Ctrl+G | 打开帮助 |
| Alt+U | 撤销 |
| Alt+E | 重做 |
| Alt+W | 查找下一个匹配 |

常见导航：

```text
方向键       上下左右移动
Ctrl+F / B   前进/后退一个字符（注意，前进字符是后移光标）
Ctrl+N / P   下一行/上一行
Ctrl+Y / V   上一页/下一页
Alt+\ / Alt+/ 跳到文件开头/结尾
Ctrl+A / E   跳到行首/行尾
```

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 基础操作流程

```bash
nano demo.txt
```

输入内容后：

```text
Ctrl+O   保存
Enter    确认文件名
Ctrl+X   退出
```

若有未保存修改，退出时会提示：

```text
Y  保存并退出
N  不保存退出
```

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 选择、剪切与粘贴

开始标记选区：

```text
Ctrl+^
```

移动光标扩展选区后可执行：

```text
Ctrl+K  剪切当前行或选区
Ctrl+U  粘贴
Ctrl+D  删除光标后的字符
Backspace 删除光标前的字符
```

连续按 `Ctrl+K` 可剪切多行，再用 `Ctrl+U` 一次次粘贴。

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 查找与替换

查找：

```text
Ctrl+W
```

输入关键词回车后可用 `Alt+W` 跳到下一个匹配。

替换：

```text
Ctrl+\
```

依次输入“查找内容”和“替换内容”，然后根据提示选择：

```text
A  全部替换
Y  替换当前
N  跳过当前
```

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 文件与缓冲区操作

读取其他文件内容到当前缓冲区：

```text
Ctrl+R
```

打开多个文件：

```bash
nano file1.txt file2.txt file3.txt
```

缓冲区切换：

```text
Alt+,  上一个缓冲区
Alt+.  下一个缓冲区
```

跳转到指定行列：

```text
Ctrl+_
```

输入 `行号,列号` 后确认。

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 常用启动参数

```text
nano -l file.txt   显示行号
nano -m file.txt   启用鼠标支持
nano -B file.txt   保存时生成备份文件（file.txt~）
nano -v file.txt   只读查看模式
```

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 常用配置（nanorc）

配置文件位置：

- 用户级：`~/.nanorc` 或 `~/.config/nano/nanorc`
- 系统级：`/etc/nanorc`

示例配置：

```text
set linenumbers
set autoindent
set tabsize 4
set mouse
set softwrap
set backup
set constantshow
include "/usr/share/nano/*.nanorc"
```

说明：

- `set linenumbers`：显示行号
- `set autoindent`：新行自动缩进
- `set tabsize 4`：Tab 宽度 4
- `set mouse`：启用鼠标定位
- `set softwrap`：软换行
- `set backup`：保存时创建备份
- `include ...`：加载语法高亮规则

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 常见问题

1. 快捷键无响应：可能被终端快捷键占用，检查终端或 tmux 映射。
2. 无法保存文件：通常是权限不足，使用 `sudo nano 文件名` 或调整权限。
3. 语法高亮失效：检查 `include` 路径是否存在、配置是否生效。
4. 中文乱码：确认文件和终端均为 UTF-8 编码环境。

<div style="width:70%;margin:48px auto;display:flex;align-items:center;justify-content:center;"><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="margin:0 20px;font-size:24px;color:#b8a998;">❖</span><span style="margin:0 10px;font-size:16px;color:#c9bfb3;">◆</span><span style="flex:1;height:2px;background:linear-gradient(90deg,transparent,#b8a998 20%,#afa89f 50%,#b8a998 80%,transparent);opacity:0.5;"></span></div>

## 使用场景

Nano 适合快速编辑系统配置、脚本、日志和临时文本。如果你更看重“立刻能改、立刻能保存退出”，它会是非常顺手的终端编辑器。
