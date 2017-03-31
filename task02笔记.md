原博文地址：https://alexzhong22c.github.io/2017/04/01/ife-css-task02/

## CSS选择器优先级

在文章 [CSS选择器优先级](https://alexzhong22c.github.io/2017/03/31/css-selectors-specificity/) 中我整合了这部分笔记。

## H5加id的观点

虽然语义化标签好用，但是当它需要加id的时候还是加吧：id="header"

## list-style-xxx

我们常用list-style，实则它是一个 简写属性。

### list-style-type

而`list-style-type`在CSS2中的新特性需要至少IE8的支持，所以我们一般只使用它在CSS1中的内容。况且，很少人提及list-style在移动设备浏览器上的支持，所以不能乱用。

另外，任何的版本的 Internet Explorer （包括 IE8）都不支持属性值 "decimal-leading-zero"、"lower-greek"、"lower-latin"、"upper-latin"、"armenian"、"georgian" 或 "inherit"。

可以使用的有：

- none

用于无序列表的：

- disc 实心圆
- circle 空心圆
- square 实心方块

用于有序列表的：

- decimal 数字
- lower-alpha、upper-alpha
- lower-roman、upper-roman

### list-style-position

默认值是outside，和inside的区别，看一下 [demo](http://www.w3school.com.cn/tiy/t.asp?f=csse_list-style-position) 马上就清楚

### list-style-image

使用图像来替换列表项的标记。

这个属性指定作为一个有序或无序列表项标志的图像。图像相对于列表项内容的放置位置通常使用 list-style-position 属性控制。

注释：**请始终规定一个 "list-style-type" 属性以防图像不可用。**

```
ul {
  list-style:square outside url('/i/arrow.gif');
}
```

## border-collapse

默认值是separate，不会忽略border-spacing和empty-cells属性。

collapse会忽略border-spacing和empty-cells属性。

注释：如果没有规定 !DOCTYPE，则 border-collapse 可能产生意想不到的结果。

## text-indent

直接参考：http://ued.ctrip.com/blog/text-indent-summing-up.html

其总结就是：

1\.text-indent只用于div，p这样的元素上，像image、input、inline-block、inline元素绝对不用。

2\.text-indent的值如果子元素也要用到父元素的值，用px单位，而绝不用em。

## 禁止用户选择文字

一般情况下用`user-select:none`，

IE6-9不支持该属性，但支持使用标签属性 `onselectstart="return false;"` 来达到 `user-select:none` 的效果；Safari和Chrome也支持该标签属性；

直到Opera12.5仍然不支持该属性，但和IE6-9一样，也支持使用私有的标签属性 `unselectable="on"` 来达到 `user-select:none` 的效果；unselectable 的另一个值是 off；

除Chrome和Safari外，在其它浏览器中，如果将文本设置为 `-ms-user-select:none;`，则用户将无法在该文本块中开始选择文本。不过，如果用户在页面的其他区域开始选择文本，则用户仍然可以继续选择将文本设置为 `-ms-user-select:none;` 的区域文本；

**所以，“禁止用户选择文字”一般是用来引导用户在界面的操作，而不能用来 控制用户的行为 或者 重度依赖这个trick。**

参考： [user-select-css88](http://www.css88.com/book/css/properties/user-interface/user-select.htm) 说明很完备。

```html
<body>
前方的文字<div class="test" onselectstart="return false;" unselectable="on">选择我试试，你会发现怎么也选择不到我，哈哈哈哈</div>
</body>
```

CSS代码：

```css
.test{
  -webkit-user-select:none;
  -moz-user-select:none;
  -o-user-select:none;
  user-select:none;
  /*onselectstart和unselectable在html那里*/
}
```

**另外，结合JavaScript代码来实现禁止效果，效果会更好。**

例如：http://stackoverflow.com/questions/2700000/how-to-disable-text-selection-using-jquery

## text-align

[text-align--CSS88](http://www.css88.com/book/css/properties/text/text-align.htm) 还介绍了单行文字怎么应用justify

## fieldset

看到一篇文章介绍 [Extjs FieldSet组件](http://canfly2010.iteye.com/blog/678584) 的文章很有趣，这个组件的目的是将fieldset的边框去掉或者改变内边距。

学到的一个知识是：

> fieldset默认是带边框的，而legend默认一般显示在左上角。但在某些场合或许不愿意让fieldset和legend的默认样式或默认布局影响设计方案中的美观。
>
> 解决方法：在CSS中将fieldset的border设置为0，legend的display设置为none即可。

