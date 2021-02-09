# <div align="center" style="color:red">VS Code 使用 Markdown 编写文档 </div>

## 第二级标题

### 第三级标题

**加粗**
*斜体*

***斜体加粗***

~~删除线~~

> 这是引用的内容
>> 这是引用的嵌套

以下是添加分割线的两种方法，3个符号以上即可

<center>居中</center>

<p align="left">左对齐</p>

$$y = k x + b \tag{1}$$

$\sum$ $\sum_{i=1}$ $\sum_{i=1}^{n}$ $\sum_{i=1}^{n}{n*(n+1)}$

$\alpha$ $\beta,\gamma$

$$\gamma,\Gamma$$

**说明：**$表示独立成行，$$表示独站一行居中，{}代表一个域，反斜杠\转义，首字母大写表示大写，其他的特殊符号如下

$\oplus$ $\check X$ $\acute X$ $\grave X$ $\vec X$ $\bar X$ $\hat X$ $\tilde Y$ $\dddot Y$ $\mathring X$

$$\frac{a}{b}$$
$\int_{a}^{b}$ $\iint dx dy=\sigma$ $\iiint dx dy dz=\sigma$

$\overline A$ $\xrightarrow{abc}$ $\lim_{t \to 0}x \to 0$ $\sqrt{n}$

***
---
以下是添加图片的语法，图片alt就是显示在图片下面的文字，相当于对图片内容的解释。
图片title是图片的标题，当鼠标移到图片上时显示的内容。title可加可不加
***
![图片alt](https://upload-images.jianshu.io/upload_images/6966151-870bb6a8ba4978ab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp "图片title")
***
超链接，title可加可不加
***
[超链接名](超链接地址 "超链接title")
***
如下可在新页面中打开

<a href="超链接地址" target="_blank">超链接名</a>
***

- 无序列表样式
  
+ 样式二

* 样式三
  
***

1. 有序列表

***

1. 一级列表  

    1. 二级列表

        1. 三级

***
表格

姓名|技能|排行
--|--|--
刘备|哭|大哥
关羽|打|二哥
张飞|骂|三弟

***
单行代码

`create database hero;`
***
代码块

```html/css
    function fun(){

    echo "Markdown 语法练习教程！";
}
fun();
```

<font color="red">中间写上想说的话</font>

行内标记`hello world`独立格式$md$

- [ ] 选项一
- [x] 选项二

<p style="color: #AD5D0F;font-size: 30px; font-family: '宋体';">内联样式</p>
