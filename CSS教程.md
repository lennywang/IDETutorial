#### word-break

normal：默认的换行规则。依据各自语言的规则，允许在字间发生换行。

keep-all：对于 CJK（中文，韩文，日文）文本不允许在字符内发生换行。Non-CJK 文本表现同normal

break-all：对于 Non-CJK 文本允许在任意字符内发生换行。该值适合包含一些非亚洲文本的亚洲文本，比如使连续的英文字符断行。

break-word：与break-all相同，不同的地方在于它要求一个没有断行破发点的词必须保持为一个整体单位。

 ![break-all与break-word对比](https://github.com/lennywang/Img/raw/master/wordbreak.png)

#### pointer-events

auto：与pointer-events属性未指定时的表现效果相同。

none：元素永远不会成为鼠标事件的target。

对应的脚本特性为**pointerEvents**。

```html
<style>
	a[href="http://example.com"] {
		pointer-events: none;
	}
</style>

<ul>
	<li><a href="https://developer.mozilla.org/">MDN</a></li>
	<li><a href="http://example.com">一个不能点击的链接</a></li>
</ul>
```

#### border-radius

border-*-radius = `border-top-left-radius`,`border-top-right-radius`,`border-bottom-right-radius`,border-bottom-left-radius

* border-radius属性提供 2 个参数，参数间以`/`分隔，每个参数允许设置 1~4 个参数值，第 1 个参数表示水平半径或半轴，第 2 个参数表示垂直半径或半轴，如第 2 个参数值省略未定义，则直接复制第 1 个参数值。
* 水平半径或半轴：如果提供全部四个参数值，将按`上左 top-left`、`上右 top-right`、`下右 bottom-right`、`下左 bottom-left`的顺序作用于四个角；提供三个，第一个用于`top-left`，第二个用于`top-right`和`bottom-left`，第三个用于`bottom-right`；提供两个，第一个用于`top-left`和`bottom-right`，第二个用于`top-right`和`bottom-left`；只提供一个，将用于全部的四个角。

![border-radius属性设置两个参数](https://github.com/lennywang/Img/raw/master/border-radius.png)

> md文件插入图片遇到的问题和解决办法  https://blog.csdn.net/u012150360/article/details/78475479



#### :before

“伪元素”，顾名思义。它创建了一个虚假的元素，并插入到目标元素内容之前或之后。著作权归作者所有。
商业转载请联系作者获得授权,非商业转载请注明出处。

```css
p.box {
  width: 300px;
  border: solid 1px white;
  padding: 20px;
}

p.box:before {
  content: "#";
  border: solid 1px white;
  padding: 2px;
  margin: 0 10px 0 0;
}	

<p class="box">Other content.</p>

```

![before伪元素](https://github.com/lennywang/Img/raw/master/before.png)

语法规范

1. 伪元素如果没有设置“content”属性，伪元素是无用的
2. 插入的元素在默认情况下是[内联元素] 。为了给插入的元素赋予高度，填充，边距等等，你通常必须显式地定义它是一个块级元素。著作权归作者所有。
3. 伪元素必须是被应用元素的子元素。

> 参考网址：http://www.w3cplus.com/css3/learning-to-use-the-before-and-after-pseudo-elements-in-css.html

 ***

#### div 居中

```html
<style type="text/css">
.main {
    text-align: center;
    background-color: #fff;
    border-radius: 20px;
    width: 1000px;
    height: 40px;
    line-height: 40px;
    margin: auto;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    font-size: 22px;
    font-weight: bold;
}

.spanI {
    color: #fda775;
    cursor: pointer;
}
</style>

<div class="main">
  <span class="spanI">content</span>  
</div>

```










 ![break-all与break-word区别](https://github.com/lennywang/Img/raw/master/wordbreak.png)
