原博文地址：https://alexzhong22c.github.io/2017/03/27/ife-css-task01/

task01其实就是对HTML的学习，对应的代码其实就是task02的[demo](https://alexzhong22c.github.io/IFE-CSS-learning/task02.html)的HTML部分。

## 细节问题总结

### i/b/em/strong元素

`<em>` 用于对文本内容进行强调，强调位置的不同通常会改变句子的含义。如果仅仅在语态或语气上为了突出某一个文本，那应该使用`<i>`。

但如果为了突出某一部分的重要性、严重性或紧急性，那应该使用 `<strong>`。根据 W3C 对 `<b>`元素的说明，`<b>`元素应当是在其他标签都不合适的情况下最后一个考虑使用的标签。

相同的，在考虑使用 `<i>` 之前，也要想想是否用` <em>`、`<strong>`、`<dfn>` 或 `<mark>` 等元素更合适。

### 单标签要闭合吗

一句话总结，xhtml严格要求空标签必须自闭合，html5又不要求自闭合但是兼容xhtml的自闭合写法。

### alt属性

为了写优雅的代码：img元素记得加alt属性。

### 表单控件

- name对于radio很重要；name对于checkbox很重要
- 对于表单中的单选radio控件和复选checkbox控件以及下拉框select控件，可以为radio, checkbox添加checked属性以及为option添加selected属性让其默认选中

### H5加id的观点

虽然语义化标签好用，但是当它需要加id的时候还是加吧：id="header"

------

### form元素

和表单相关的元素都由 form元素 包着，一个form代表一个表单。

### fieldset元素

通常用来对表单的相关元素进行分组，如果不需要分组就可以直接不用fieldset这一层。

HTML5 中新增了一些 fieldset元素 的新属性：disabled、form、name，而HTML 4.01 中不支持这些属性。

**目前，这些新属性被浏览器们支持得都很差。不建议fieldset使用任何属性。**

### legend元素

legend元素 代表一个用于表示 它的父元素`<fieldset> ` 的内容的标题。

```
<form>
  <fieldset>
    <legend>Title</legend>
    <input type="radio" name="radio" id="radio"> <label for="radio">Click me</label>
  </fieldset>
</form>
```
### label元素

label元素 表示用户界面中项目的标题。

```
<form>
  <label for="GET-name">Name:</label>
  <input id="GET-name" type="text" name="name">
  <input type="submit" value="Save">
</form>
```

#### 使用 label配合控件使用：

在下面这个例子中，点击label会选中对应的input控件。靠的就是 for属性 和 id属性 产生的联系。

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

## H5新标签和被H5拥抱的老元素们

- 在HTML5之后，哪些新标签可以放心使用、哪些老标签需要继续使用？
- 这个demo用到的标签的详细介绍？

这些话题的主要内容都写到了我的博客里： [H5新标签和被H5拥抱的老元素们](https://alexzhong22c.github.io/2017/03/28/h5-new-ele/)