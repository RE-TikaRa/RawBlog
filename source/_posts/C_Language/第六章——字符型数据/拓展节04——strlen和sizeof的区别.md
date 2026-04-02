---
title: 第六章——字符型数据 拓展节04——strlen和sizeof的区别
date: 2026-02-07 02:21:28
tags:
  - C Language
categories:
  - C_Language
  - 第六章——字符型数据
abbrlink: 91c504ba
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
excerpt: "这是文章摘要 This is the excerpt of the post"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2031-02-07 02:21:28
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---
# strlen和sizeof的区别
1. strlen(s)是计算以s为起始地址的字符串的长度，并作为函数值返回。这一长度不包括字符串结尾的标志’\0’。
2. sizeof(s)是求数组a的长度，包括’\0’，如果数组已经分配了大小N，则sizeof的值就为N.
