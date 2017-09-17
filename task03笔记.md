原博文地址：https://alexzhong22c.github.io/2017/09/17/ife-css-task03/

> task03任务要求：
>
> - 调节浏览器宽度，固定宽度和自适应宽度的效果始终符合预期。
> - 改变中间一栏的内容长度，以确保在中间一栏较高和右边一栏较高时，父元素的高度始终为子元素中最高的高度。
>
> 这个任务中，懒于去上网找图片素材，直接引用了别人复仇者联盟的图片素材。

我们先总览本文内各种实现的思路：

1. 按照普通顺序编写HTML
   1. 运用margin
   2. 用BFC
2. 先加载main栏的HTML **（重点）**
   1. 双飞翼布局
   2. 圣杯布局

## 按普通顺序编写HTML

一般来说我们 **按照普通顺序编写HTML** ：此时先写子栏的代码，再写main栏的代码。

此时，如果想要形成三栏的布局，思路可再细分为二：

### 要么运用margin形成三栏的布局

[demo](https://alexzhong22c.github.io/IFE-CSS-learning/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E6%8C%89%E6%99%AE%E9%80%9A%E9%A1%BA%E5%BA%8F%E7%BC%96%E5%86%99/1%E6%99%AE%E9%80%9A%E6%96%B9%E6%B3%95-%E7%94%A8margin%E5%88%86%E5%BC%80.html) --  [源码](https://github.com/AlexZhong22c/IFE-CSS-learning/blob/master/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E6%8C%89%E6%99%AE%E9%80%9A%E9%A1%BA%E5%BA%8F%E7%BC%96%E5%86%99/1%E6%99%AE%E9%80%9A%E6%96%B9%E6%B3%95-%E7%94%A8margin%E5%88%86%E5%BC%80.html)

### 要么用BFC形成三栏的布局

[demo](https://alexzhong22c.github.io/IFE-CSS-learning/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E6%8C%89%E6%99%AE%E9%80%9A%E9%A1%BA%E5%BA%8F%E7%BC%96%E5%86%99/2%E4%BD%BF%E7%94%A8BFC%E6%96%B9%E6%B3%95.html) --  [源码](https://github.com/AlexZhong22c/IFE-CSS-learning/blob/master/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E6%8C%89%E6%99%AE%E9%80%9A%E9%A1%BA%E5%BA%8F%E7%BC%96%E5%86%99/2%E4%BD%BF%E7%94%A8BFC%E6%96%B9%E6%B3%95.html)

## 先加载main栏的HTML

我们希望页面中间的main栏的内容最先被浏览器加载呈现，这样页面就更加主次合理，所以前端圈里面出现了这么种思路。

**原理：**

- 定义main-content宽度为100%（如果在IE6里不定义100%，会有点小问题，亲们自己可以一试）
- main 左浮动，宽度为100%
- sub 左浮动，宽度190，左外边距为-100%（此处是关键：浮动情况下，负的外边距会导致DIV上移，而使用-100%可以确使它移动到最左侧。)
- extra 左浮动，宽度230，左外边距为-230px（道理同上，注意的是，负的左外边距值一定要大于或等于该DIV的宽度，才能靠到上一行去）

当只使用负左外边距的方法时，能够实现**先加载main栏**，但是main栏的内容会被挡住：

[demo](https://alexzhong22c.github.io/IFE-CSS-learning/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E5%85%88%E5%8A%A0%E8%BD%BDmain%E6%A0%8F/1main%E7%9A%84%E5%86%85%E5%AE%B9%E8%A2%AB%E6%8C%A1%E4%BD%8F.html) --  [源码](https://github.com/AlexZhong22c/IFE-CSS-learning/blob/master/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E5%85%88%E5%8A%A0%E8%BD%BDmain%E6%A0%8F/1main%E7%9A%84%E5%86%85%E5%AE%B9%E8%A2%AB%E6%8C%A1%E4%BD%8F.html)

> 因此，解决 main栏的内容被挡住 的思路可再细分为二：
>
> 1.**双飞翼布局**
>
> 2\. **圣杯布局**
>
> 而在本文的最后，会介绍其他的方式来实现 三栏等高的 先加载main栏的 三栏式布局。

### 双飞翼布局

淘宝的双飞翼布局：在原来的基础上多套了一层div，并且增设margin。[2-1淘宝双飞翼布局demo](https://alexzhong22c.github.io/IFE-CSS-learning/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E5%85%88%E5%8A%A0%E8%BD%BDmain%E6%A0%8F/2-1%E5%8F%8C%E9%A3%9E%E7%BF%BC%E5%B8%83%E5%B1%80.html) --  [源码](https://github.com/AlexZhong22c/IFE-CSS-learning/blob/master/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E5%85%88%E5%8A%A0%E8%BD%BDmain%E6%A0%8F/2-1%E5%8F%8C%E9%A3%9E%E7%BF%BC%E5%B8%83%E5%B1%80.html)

#### 好处：

- 可以实现主要的内容先加载的优化
- 兼容目前所有的主流浏览器，包括IE6在内

#### 缺点：

- 位置不灵活，同时css对位置的控制很强

### 圣杯布局

圣杯布局的特点是它使用了padding和相对定位，当然它也使用了负左外边距。[2-2圣杯布局demo](https://alexzhong22c.github.io/IFE-CSS-learning/task03三栏布局/先加载main栏/2-2圣杯布局.html) --  [源码](https://github.com/AlexZhong22c/IFE-CSS-learning/blob/master/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E5%85%88%E5%8A%A0%E8%BD%BDmain%E6%A0%8F/2-2%E5%9C%A3%E6%9D%AF%E5%B8%83%E5%B1%80.html)

#### 好处：

- 可以实现主要的内容先加载的优化
- 位置比较灵活：毕竟它是用 相对定位 实现的
- main部分是自适应宽度的，很容易在定宽布局和流体布局中切换。
- 任何一栏都可以是最高栏，不会出问题。
- 只需要针对ie6来hack：`zoom:1` ，兼容目前所有的主流浏览器，包括IE5.5

#### 缺点：

- 当浏览器宽度过窄时，子栏可能会消失，extra栏的内容可能会跑到主栏里面。

[证明圣杯布局内部灵活的demo](https://alexzhong22c.github.io/IFE-CSS-learning/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E5%85%88%E5%8A%A0%E8%BD%BDmain%E6%A0%8F/2-2-X%E8%AF%81%E6%98%8E%E5%9C%A3%E6%9D%AF%E5%B8%83%E5%B1%80%E5%86%85%E9%83%A8%E7%81%B5%E6%B4%BB.html) -- [证明圣杯布局内部灵活的源码](https://github.com/AlexZhong22c/IFE-CSS-learning/blob/master/task03%E4%B8%89%E6%A0%8F%E5%B8%83%E5%B1%80/%E5%85%88%E5%8A%A0%E8%BD%BDmain%E6%A0%8F/2-2-X%E8%AF%81%E6%98%8E%E5%9C%A3%E6%9D%AF%E5%B8%83%E5%B1%80%E5%86%85%E9%83%A8%E7%81%B5%E6%B4%BB.html)

## // 实现三栏等高的其他方法

### float + box-sizing + background-clip

.main元素的border区域为两侧定宽列的所在区域，实现伪等高效果；设置.main的padding和background-clip来实现元素间隔。两侧元素通过负margin调整到.main元素的border区域

缺点: 兼容性不好，用到了CSS3的属性，应该至少要ie9

### 绝对定位

设置子元素的top:0;bottom:0;使得所有子元素的高度都和父元素的高度相同，实现等高效果

### flex布局

flex中的伸缩项目默认都拉伸为父元素的高度，可实现等高效果。通过改变伸缩项目的order，可以实现元素顺序调换的效果

缺点: 兼容性不好

------

参考： 

[详解 CSS 七种三栏布局技巧](https://zhuanlan.zhihu.com/p/25070186?refer=learncoding)