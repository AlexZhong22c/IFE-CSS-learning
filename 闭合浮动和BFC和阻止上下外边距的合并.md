原博文地址：https://alexzhong22c.github.io/2017/04/01/clearfix-n-bfc/

本文部分内容参考 [那些年我们一起清除过的浮动](http://www.iyunlu.com/view/css-xhtml/55.html) ，但是 一丝冰凉 的这篇文章有很多地方我都不认同，取其精华去其糟粕，所以本文并没有包含那些我所不认同的内容。

## 区分 清除浮动 和 闭合浮动

- 清除浮动：清除对应的英文单词是 clear，对应CSS中的属性是 clear：left | right | both | none；
- 闭合浮动：更确切的含义是使浮动元素闭合，从而减少浮动带来的影响。

两者的区别 [请看Demo](http://www.iyunlu.com/demo/enclosing-float-and-clearing-float/index.html)

闭合浮动主要用来解决**因为子元素浮动导致父元素高度塌陷**的问题。

## 闭合浮动的一些老方法：

1. 在子元素们的最后追加一个`style="clear:both"`的空标签，这个不好
2. 在子元素们的最后追加一个br标签，使用br标签的`clear="all | left | right | none"` 属性，因为一般不建议在HTML中使用br，这个也不好
3. 通过**设置父元素**overflow值设置为hidden；在IE6中还需要触发 hasLayout ，例如 zoom：1；因为最终还是有补不了的bug被大家弃用
4. 通过**设置父元素**overflow值设置为auto，同样也有bug
5. 父元素也设置浮动，缺点是**使得与父元素相邻的元素的布局会受到影响**，不可能一直浮动到body，不推荐使用
6. 父元素设置display:table，盒模型属性已经改变，由此造成的一系列问题，得不偿失，不推荐使用。文章最后还会再介绍到给**父元素的伪元素设置display:table**。

### 7\. 使用`：after`伪元素

> 需要注意的是 :after是伪元素，不是伪类（另外，某些CSS手册里面称之为“伪对象”，不太对）。

由于IE6-7不支持:after，要同时使用 zoom:1触发IE6和IE7的 hasLayout。**在后面的demo中会介绍到。**

- 优点：浏览器支持好，不容易出现怪问题（目前：大型网站都有使用，如：腾迅，网易，新浪等等）
- 缺点：复用方式不当会造成代码量增加
- 建议：定义公共类，以减少CSS代码

### 不要使用方案3和4

方案3、4通过overflow闭合浮动，实际上已经创建了新的 块级格式化上下文，而它们设置的对象都是父元素，这将导致其布局和相对于浮动的行为等发生一系列的变化，闭合浮动只不过是一系列变化中的一个作用而已。所以为了闭合浮动去改变全局特性，这是不明智的，带来的风险就是一系列的bug，比如firefox 早期版本产生 focus，截断绝对定位的层等等。始终要明白，如果单单只是需要闭合浮动，overflow就不要使用，而不是某些文章所说的“慎用”。

### 父级div定义height的方法

- 父级div定义height，这样就**不必闭合浮动**了
- 不推荐使用，只建议高度固定的布局时使用

## 小结

通过对比，我们不难发现，其实以上列举的方法，无非有两类：

其一，通过在浮动元素的末尾添加一个空的元素

其二，通过设置父元素 overflow 或者display：table 属性来闭合浮动，原理就是BFC，下面探讨一下：

## BFC知识

[Block formatting contexts ](http://www.w3.org/TR/CSS21/visuren.html#block-formatting)（块级格式化上下文），以下简称 BFC。在CSS3里面改动后称之为flow root。

### BFC的特性

一丝冰凉 对于BFC的特征的解释非常模糊，甚至不正确。我认为她这部分内容所解释的现象只适用到IE7

通俗地来说就是：

- 创建了 BFC的元素就是一个独立的盒子，里面的子元素不会在布局上影响外面的元素，反过来外面的元素也不影响里面的元素
- 同时BFC仍然属于文档中的普通流

### 如何触发BFC

- float 除了none以外的值 
- overflow 除了visible 以外的值（hidden，auto，scroll ） 
- display (table-cell，table-caption，inline-block) 
- 实际上，用`display:table`来产生匿名框也可以触发BFC，见文章 [A new micro clearfix hack](http://nicolasgallagher.com/micro-clearfix-hack/) 或见本节的备注
- position（absolute，fixed） 
- fieldset元素

> 需要注意的是，display:table 本身并不会创建BFC，但是它会产生匿名框(anonymous boxes)，而匿名框中的display:table-cell可以创建新的BFC，换句话说，触发块级格式化上下文的是匿名框，而不是display:table。所以通过display:table和display:table-cell创建的BFC效果是不一样的。
>
>  fieldset 元素在www.w3.org里目前没有任何有关这个触发行为的信息，直到HTML5标准里才出现。有些浏览器bugs（Webkit，Mozilla）提到过这个触发行为，但是没有任何官方声明。实际上，即使fieldset在大多数的浏览器上都能创建新的块级格式化上下文，开发者也不应该把这当做是理所当然的。CSS 2.1没有定义哪种属性适用于表单控件，也没有定义如何使用CSS来给它们添加样式。用户代理可能会给这些属性应用CSS属性，建议开发者们把这种支持当做实验性质的，更高版本的CSS可能会进一步规范这个。

**由于浏览器的差异：**

- 在支持BFC的浏览器（IE8+，firefox，chrome，safari）通过创建新的BFC闭合浮动；
- 在不支持 BFC的浏览器 （IE6-7），通过触发 hasLayout 闭合浮动。IE6-7的hasLayout 可以等同于 BFC。

## 深入理解伪元素闭合浮动

上面已经列举了7种闭合浮动的方法，通过第三节分析的原理，我们发现其实更多的：对父元素使用display：table-cell，display：inline-block等只要触发了BFC的属性值都可以闭合浮动。从各个方面比较，**方案7**：after伪元素闭合浮动无疑是相对比较好的解决方案了。这种思路的演进历史可以参考文章：https://css-tricks.com/snippets/css/clear-fix/

而最后，方案7里面有两个最优的小方案：

### 最优小方案1：

```
.clearfix:before, .clearfix:after {
content:"."; display:block; height:0; visibility:hidden; clear:both; }

.clearfix { *zoom:1; }
```

1）通过 content:"."生成内容作为伪元素的内容

2）display:block 使生成的元素以块级元素显示,占满剩余空间;

3）height:0 避免生成内容破坏原有布局的高度。

4）visibility:hidden 使生成的内容不可见，并允许可能被生成内容盖住的内容可以进行点击和交互;

5）同时要使用 zoom:1触发IE6和IE7的 hasLayout

**通过分析发现，除了clear：both用来清除浮动的，其他代码无非都是为了隐藏掉content生成的内容，这也就是其他版本的闭合浮动为什么会有font-size：0，line-height：0的缘故。**

**更重要的是，我认为这个方法根本就没产生 BFC 。**

> 另外，不建议将content设置为空字符串""，在firefox 7里面会看到它会产生空隙

### 最优小方案2：

```
.clearfix:before,
.clearfix:after {
    content: " "; /* 1 */
    display: table; /* 2 */
}

.clearfix:after {
    clear: both;
}

.clearfix {
    *zoom: 1;
}
```

1\. 使用content: " " 是为了避免Opera的bug，否则它会在 被清除浮动的元素的顶部和底部 产生一个看得出的空格

2\. 这里对伪元素使用的`display: table;`会产生一个 [anonymous boxes](http://www.w3.org/TR/CSS2/tables.html#anonymous-boxes) 和一个BFC，这个BFC意味着before伪类会阻止上外边距的合并，同时after伪类会闭合浮动。

> 需要注意的是，display:table 本身并不会创建BFC，但是它会产生匿名框(anonymous boxes)，而匿名框中的display:table-cell可以创建新的BFC，换句话说，触发块级格式化上下文的是匿名框，而不是display:table。所以通过display:table和display:table-cell创建的BFC效果是不一样的。

这个小方案的好处是：不用隐藏用content属性产生的内容，并且代码量特别少。

#### Firefox < 3.5版本的问题

Firefox < 3.5禁止在body元素和它的第一个子元素之间插入多余的空格，所以

- 要么对before伪类使用`content:"."`
- 要么额外加上`visibility:hidden`等等属性来隐藏这种情况下所插入的字符(但这也不能解释淘宝网闭合浮动的写法，因为淘宝网主要把它用在after伪类上)

### 设置before伪元素的作用：

设定before伪元素的属性**并不是用来闭合浮动的**，不过它能阻止上外边距的合并，这会带来两个好处：

- 这种清除浮动的方式所表现出来的外貌看上去和 其他的清除浮动的方式(比如overflow:hidden)的 一致。
- 和IE6/7使用zoom:1后的外貌保持一致

毕竟，**使用after伪元素闭合浮动**的时候，下外边距的合并已经被阻止了，为了上下看上去对称，before伪元素也应该这样。

主要译自： [A new micro clearfix hack](http://nicolasgallagher.com/micro-clearfix-hack/)

### 创新方案：零宽度空格

通过查询发现Unicode字符里有一个“零宽度空格”，也就是[U+200B ](http://www.fileformat.info/info/unicode/char/200b/index.htm)，这个字符本身是不可见的，所以我们完全可以省略掉 visibility:hidden了

```
.clearfix:after {content:"200B"; display:block; height:0; clear:both; }
.clearfix { *zoom:1; }
```

在实际开发中，由于存在Unicode字符不适合内嵌CSS的GB2312编码的页面，使用前面两个小方案完全可以解决我们的需求了。

### 别混淆了闭合浮动/BFC/阻止上下外边距的合并

这是一个比较详细的 [demo](https://github.com/AlexZhong22c/IFE-CSS-learning/blob/master/闭合浮动和BFC和阻止上下外边距的合并.html)：

这个demo里面加入了**企图对伪元素用display:block配合content:" "闭合浮动**这种不太恰当的方法。

从这个demo可以看到：

- **使用伪元素闭合浮动**必然会引发的一个效果是阻止下外边距的合并
- BFC必然会引发的一个效果是阻止上下外边距的合并
- 闭合浮动 的方式不只有 触发BFC ，触发BFC 只是其中的一种方法
- 阻止上下外边距合并的方式不只有 触发BFC，触发BFC 只是其中的一种方法
- 而那些能触发BFC的方式可以参考本文前文的说明，其中就说明了浮动会触发BFC
- 单独的display:block并不会触发BFC
- 对伪元素用display:table会触发BFC
- 不应当**企图对伪元素用display:block配合content:" "闭合浮动**，因为这种方式的清除浮动 只有在ie7以下的浏览器里才能阻止上下外边距的合并，所以使用它的话不同浏览器的样式会不统一
- 要小心地对浮动的子元素设置下外边距，因为在IE7以下浏览器里面，如果没有其他子元素撑起父元素的高度，浮动的子元素的下外边距直接被解释为0(这是为了尽量减小页面的高度)，造成样式的不统一