---
title: 第七章——函数 预读节——C程序结构函数
tags:
  - C Language
categories:
  - C_Language
  - 第七章——函数
thumbnail: 'https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png'
excerpt: 这是文章摘要 This is the excerpt of the post
banner: 'https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png'
abbrlink: e38903bc
date: 2026-02-07 02:21:28
expires: 9999-12-31 23:59:59
sticky:
---
# C语言程序结构
1. 一个C语言程序可以包含多个源程序文件。
2. 一个源程序文件中可以包含多个函数。
3. C语言程序有且仅有一个主函数`main`作为程序的入口。
4. 函数是C语言程序的基本单位。
5. 程序执行从`main()`函数开始，在`main()`函数中结束。
6. 程序只会执行在`main()`函数中定义的内容，其他函数需要通过调用的方式执行。
7. 函数之间不能嵌套定义。
8. 函数之间可以嵌套调用。

# C语言程序基本结构展示
![C.png](https://s2.loli.net/2025/06/09/2mcSKJO3Q8C9pfl.png)

# C语言函数分类

## 1.从用户角度
 - 标准函数（库函数）：由系统提供
 - 用户自定义函数

## 2.从函数形式
 - 无参函数
 - 有参函数

# 库函数（标准函数）
&emsp;&emsp;系统提供的已设计好的函数
![.png](https://s2.loli.net/2025/06/09/Zjqci3nHWfBLCoK.png)

# 使用库函数应注意

1. 函数功能
2. 函数参数的数目和顺序，及各个参数的意义和类型
3. 函数的返回值的意义和类型
4. 需要使用的包含文件
5. 调用库函数时，必须要使用`#include <头文件名.h>`
6. 标准库函数的调用形式：`函数名(参数表)`