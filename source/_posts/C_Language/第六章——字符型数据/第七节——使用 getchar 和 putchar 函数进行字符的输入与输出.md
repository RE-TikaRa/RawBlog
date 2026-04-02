---
title: 第六章——字符型数据 第七节——使用 getchar 和 putchar 函数进行字符的输入与输出
date: 2026-02-07 02:21:28
tags:
  - C Language
categories:
  - C_Language
  - 第六章——字符型数据
abbrlink: 22d79d1d
thumbnail: "https://s2.loli.net/2025/12/22/nBapAxK8NowjZFP.png"
sticky:
excerpt: "这是文章摘要 This is the excerpt of the post"
banner: "https://s2.loli.net/2025/12/22/uBnZDzxcI7JHCX3.png"
expires: 2031-02-07 02:21:28
password: ""
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---
# 一、核心概念：单字符输入输出的“轻量级选手”  
## 1.1 `getchar` 与 `putchar` 的定义  
- **`getchar`**：从标准输入（键盘）读取一个字符（含空格、换行符），无需格式说明符。  
  ```c  
  char ch = getchar();  // 直接赋值  
  ```  
- **`putchar`**：向标准输出（屏幕）输出一个字符，参数可以是字符常量、变量或 ASCII 码值。  
  ```c  
  putchar('A');         // 输出字符 A  
  putchar(97);          // 输出字符 a（ASCII 码值）  
  ```  

## 1.2 与 `scanf/printf` 的对比  
| 特性               | `getchar/putchar`       | `scanf/printf`            |  
|--------------------|--------------------------|----------------------------|  
| **适用场景**       | 单字符输入输出           | 格式化混合数据输入输出     |  
| **空白处理**       | 直接读取所有字符（含空格、换行） | `%c` 需手动跳过空白符      |  
| **效率**           | 轻量级，适合简单操作     | 灵活但稍复杂               |  

---

# 二、实战应用：典型用法与陷阱  
## 2.1 基础示例：字符回显与过滤  
```c  
char ch;  
while ((ch = getchar()) != '\n') {  // 读取直到换行  
    putchar(ch);                     // 输出字符  
}  
```  
**功能**：逐字符回显输入内容，自动过滤换行符。  

## 2.2 真题解析：输入缓冲区的陷阱  
**题目**：以下代码的输出是什么？  
```c  
#include <stdio.h>  
int main() {  
    char c1 = getchar(), c2 = getchar();  
    printf("c1=%c, c2=%d", c1, c2);  
}  
```  
**输入**：`A`（回车）  
**输出**：`c1=A, c2=10`（`c2` 读取了换行符 `\n` 的 ASCII 码 10）。  

## 2.3 常见错误与修复  
| 错误类型          | 错误示例               | 修复方法                  |  
|-------------------|------------------------|---------------------------|  
| 忽略换行符        | `getchar()` 读取后未处理 `\n` | 使用 `while(getchar() != '\n')` 清空缓冲区  |  
| 混淆函数返回值类型| `char ch = getchar()` 可能截断 | 改用 `int` 类型存储返回值（`getchar` 返回 `int` 以兼容 EOF） |  

---

# 三、进阶技巧：控制字符与调试  
## 3.1 输出控制字符  
`putchar` 可直接输出转义字符：  
```c  
putchar('\n');  // 换行  
putchar('\x07'); // 响铃（ASCII 码 7）  
```  

## 3.2 输入验证与过滤  
**案例**：仅允许输入数字字符：  
```c  
char ch;  
while ((ch = getchar()) != '\n') {  
    if (ch >= '0' && ch <= '9') {  
        putchar(ch);  
    }  
}  
```  
**效果**：输入 `a1b2c3`，输出 `123`。  

---

# 四、调试与优化：避免死循环与缓冲区污染  
## 4.1 清空输入缓冲区  
```c  
int c;  
while ((c = getchar()) != '\n' && c != EOF);  // 丢弃剩余字符  
```  
**用途**：防止前一次输入残留影响后续 `getchar()` 读取。  

## 4.2 处理 EOF（文件结束符）  
`getchar` 在遇到文件结束符（Windows 下为 `Ctrl+Z`，Linux 下为 `Ctrl+D`）时返回 `EOF`（值为 -1）：  
```c  
int ch;  
while ((ch = getchar()) != EOF) {  
    putchar(ch);  
}  
```  

---

# 五、总结：选择的艺术  
- **`getchar/putchar`**：适用于单字符输入输出，简洁高效，无需格式字符串。  
- **`scanf/printf`**：需处理混合数据或格式化时使用，但需注意空白符陷阱。  

🎯 **记忆口诀**：  
“**单字符选 `get/put`，空白陷阱不用愁；混合输入 `scanf` 强，但要记得跳空格！**”  
