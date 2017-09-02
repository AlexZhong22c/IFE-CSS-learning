原博文地址：https://alexzhong22c.github.io/2017/03/27/ife-css-task01/

## 常见问题总结

### 和强调相关的元素

`<em>` 用于对文本内容进行强调，强调位置的不同通常会改变句子的含义。如果仅仅在语态或语气上为了突出某一个文本，那应该使用`<i>`。

但如果为了突出某一部分的重要性、严重性或紧急性，那应该使用 `<strong>`。根据 W3C 对 `<b>`元素的说明，`<b>`元素应当是在其他标签都不合适的情况下最后一个考虑使用的标签。

相同的，在考虑使用 `<i>` 之前，也要想想是否用` <em>`、`<strong>`、`<dfn>` 或 `<mark>` 等元素更合适。

### 单标签要闭合吗

一句话总结,xhtml严格要求空标签必须自闭合,html5又不要求自闭合但是兼容xhtml的自闭合写法。

### alt属性

为了写优雅的代码：img元素记得加alt属性

### 表单控件

- name对于radio很重要；name对于checkbox很重要
- 对于表单中的单选radio控件和复选checkbox控件以及下拉框select控件，可以为radio, checkbox添加checked属性以及为option添加selected属性让其默认选中

------

### form元素

创建 HTML 表单：

```
<form>
  <label for="GET-name">Name:</label>
  <input id="GET-name" type="text" name="name">
  <input type="submit" value="Save">
</form>
```

### fieldset元素

fieldset元素 通常用来对表单的相关元素分组

```
<form>
  <fieldset>
    <legend>Title</legend>
    <input type="radio" name="radio" id="radio"> <label for="radio">Click me</label>
  </fieldset>
</form>
```

### legend元素

HTML的`<legend>`元素（也称为HTML的域说明元素（or HMTL
 Legend Field Element））代表一个用于表示它的父元素`<fieldset> `的内容的标题。

### label标签

label标签，为input元素定义标注，改进了表单控件的可用性，当你点击到label标签时，会自动聚焦到对应控件上。

#### 使用 label  "for" 属性 bind input "id"

```
<label for="User">Click me</label>
<input type="text" id="User" name="Name" />
```

------

### 和按钮相关的元素

在一个页面上画一个按钮，有四种办法：

- `<input type="button" /> `这就是一个按钮。如果你不写javascript 的话，按下去什么也不会发生。
- `<input type="submit" />` 这样的按钮用户点击之后会自动提交 form，除非你写了javascript 阻止它。
- `<button> `这个按钮放在 form 中也会点击自动提交，比前两个的优点是按钮的内容不光可以有文字，还可以有图片等多媒体内容。（当然，前两个用图片背景也可以做到）。它的缺点是不同的浏览器得到的 value 值不同；可能还有其他的浏览器兼容问题（[葛亮]()）。
- 其他标签，例如 a, img, span, div，然后用图片把它伪装成一个按钮。

type="button"和type="submit"各写一个，绑个alert或者dom操作。可以发现：button如果没别的，就会一动不动；submit如果没别的，就会刷新页面（应该是一闪然后保持原页面）；sb绑了dom，就是js的效果一闪，然后保持原页面。可以写js事件来绑定button，js是客户端的。但submit的实质作用是提交给服务端的，不是写个js阻止就能完事。

### dl dt dd元素

严格来说定义列表只用来**标记字典或术语表**这样的结构，也有一说是它也可以用来标记对话。在实践中，如果有一系列的“标题 + 详情”这样的结构，使用定义列表也勉强说得过去。但实际上是有更好的标记方式，比如 hx + div/p 本身就表达了标题与详情的对应关系；如果一定要强调这一系列数据的并列关系，可以在外围使用 ul 或 ol。

http://know.webhek.com/html5/html-dl-dt-dd.html

http://www.cnblogs.com/duhuo/p/5656511.html

## Content categories内容分类

Content categories 这个话题的主要内容都写到了我的博客里： [内容分类--谈谈H5标签](https://alexzhong22c.github.io/2017/01/25/h5-new-ele/)

这里拿出一些比较重要的内容来讲：

### 分节内容模型

在当前的大纲中创建一个[分节](https://developer.mozilla.org/en-US/docs/Sections_and_Outlines_of_an_HTML5_document)，此分节将定义[`header`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/header)元素、[`footer`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/footer) 元素和标题元素（[heading content](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/Content_categories#Heading_content)）的范围。

#### article元素

`<article>`元素表示文档、页面、应用或网站中的**独立结构**，其意在成为**可独立分配的或可复用的结构**，如在发布中，它可能是论坛帖子、杂志或新闻文章、博客、用户提交的评论、交互式组件，或者其他独立的内容项目。

用时要特别注意内容的独立性：一般独立完整的内容才使用article元素，如果只是一段内容的话应该是用section元素。

> 使用说明：
>
> - 当`<article>`元素嵌套使用时，则该元素代表与外层元素有关的文章。例如，代表博客评论的`<article>`元素可嵌套在代表博客文章的`<article>`元素中。
> - `<article>`元素的作者信息可通过[`address`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/address)元素提供，但是不适用于嵌套的`<article>`元素。
> - `<article>`元素的发布日期和时间可通过[`time`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/time)元素的`pubdate`属性表示。

#### section元素

- 用于定义文章中的**章节**(通常应该有标题和段落内容)


- 用来定义文档中特定的内容区块，可视为一个区域分组元素。


- 用一句话来概括它的作用就是：给内容分段，给页面分区


- 注意它与div的区别，div强调在形式上的独立性，section强调的是内容上的独立性，注意它的语义。

> article和section对比：
>
> 1\. 语义不同：
>
> - article元素是独立完整的内容，section元素页面内容分块
>
> 2\. 相同点：
>
> 本质上都是带有语义的div块元素 　　　　
>
> 分别可以看做`<div id="section">`和`<div id="article">`

#### aside元素

- aside元素通常用来设置**侧边栏**
- 用于定义article元素之外的内容，前提是这些内容与article元素内的内容相关。
- 同时也可嵌套在article元素内部使用，作为主要内容的**附属信息**。比如与内容有关的参考资料，名词解释等。

#### nav元素

- 用来定义目录、导航栏
- 并非所有的超链接都放在nav元素中，通常只把一个文档中的主导航栏放在nav中。
- 通常一个页面导航可以这样写：

```html
<nav>
  <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

或者：

```html
<div id="nav">
   <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</div>
```

### 标题内容模型

定义了分节的标题，而这个分节可能由一个明确的分节内容元素直接标记，也可能由标题本身隐式地定义。

属于此分类的元素有：h1到h6和 [`hground`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/hgroup)

> 注意：尽管[`header`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/header)可能包含一些标题内容，但[`header`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/header)并不是标题内容本身。

### 表单相关内容模型

拥有表单父节点（exposed by a **form** attribute）的元素。

一个表单父节点可以是form元素，也可以是其id在表单属性中被指定了的元素。

**thead/tobody/tfoot标签bug挺多的，暂时不要用！！**

`caption`标签必须紧随 table 标签之后

### 其他比较常用的元素

#### header元素

`<header>`元素表示一组引导性的帮助，可能包含标题元素，也可以包含其他元素，像logo、分节头部、搜索表单等。

#### footer元素

**HTML `<footer> `元素**表示最近一个[章节内容](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Sections_and_Outlines_of_an_HTML5_document#Defining_Sections_in_HTML5)或者[根节点](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Sections_and_Outlines_of_an_HTML5_document#Sectioning_root)（sectioning root ）元素的页脚。一个页脚通常包含该章节作者、版权数据或者与文档相关的链接等信息。

> - `<footer>`元素内的作者信息应包含在[`address`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/address) 元素中。
> - `<footer>`元素不是章节内容，因此在[outline](https://developer.mozilla.org/en-US/docs/Sections_and_Outlines_of_an_HTML5_document)中不能包含新的章节。

------

#### time元素

- time元素代表24小时中的某个时刻或某个日期，表示时刻允许出现时差。它可以定义很多格式的日期和时间
  - datetime属性。代表中日期和时间之间要用“T”文字分隔，“T”表示时间，请注意倒数第二行，时间加上Z文字表示给机器编码时使用UTC标准时间，表示向机器编码另一地区时间，如果是编码本地时间，则不需要添加时差。
  - pubdate属性是个可选标签。加上它搜索引擎/浏览器就可以很方便的识别出那个日期是文章、新闻的发表日期。

```
<time datetime="2015-10-22">2015年10月12日</time>
<time datetime="2015-10-22T20:00">2015年10月12日晚上8点</time>
<time datetime="2015-10-22T20:00Z">2015年10月12日晚上8点</time>
<time datetime="2015-10-22T20:00+09:00">美国时间2015年10月12日8点</time>
```

#### address元素

- 通常用来说明作者的**联系信息**，例如名字、E-mail、电话、地址等。
- address元素中的内容会以斜体显示。
- 如果单纯只有作者名的内容建议用`em`

------

- `一般图片有caption时才使用figure元素和figcaption元素`
- 另外，当文档中的一些嵌入式内容，比如引用的图片，插图，表格，代码段等，可以作为独立的单元，当这部分转移到附录中或者其他页面时不会影响到主体，这样的元素都可以放在`<figure>`元素内，而且可以搭配其子元素`<figcaption>`作很好的元素说明或者备注信息

#### figure元素

figure元素是一个媒体组合元素，也就是对其他的媒体元素进行组合，比如：图像、图标等等。

#### figcaptio元素

用来给figure元素定义标题。

#### video元素

- src属性：音频地址
- loop属性：是否重复播放
- autoplay属性：是否自动播放
- controls属性：添加控制
- poster属性：在视频加载完成前显示什么
- 当然这个元素对于个别浏览器会有些隐性的小问题