[TOC]

#css布局

##1.display属性
display常用的一些值：

| block        | 指定对象为块元素                            |
| ------------ | ----------------------------------- |
| inline       | 指定对象为行内                             |
| none         | 隐藏对象，不占空间                           |
| inline-block | 行内块                                 |
| list-item    | 列表                                  |
| flex（css3）   | 弹性伸缩盒展示(多栏多列布局,目前只适应firefox和google) |

​    举例说明：

###​	1.display:block

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
	<style>
		span,div{
          background-color:#F60;
          margin-bottom:5px;
          margin-left:5px;
          height:50Px;
        }
	</style>
<div>
	<span style="display: block">加了block属性</span>
	<span style="display: block">加了block属性</span>
	<span style="display: block">加了block属性</span>
	<span>没加block属性</span>
	<span>没加block属性</span>
	<span>没加block属性</span>
</div>
</html>
```

###​	2.dispaly:inline

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
  <style>
      div{
        background-color:#F60;
        margin-bottom:5px;
        margin-left:5px;
        height:50Px;
      }
  </style>
  <div>
      hi,我是第一个div
  </div>
  <div>
      hi,我是第二个div
  </div>
  我现在要加inline属性了<br/>
  <div style="display: inline;">
      hi,我是第一个div
  </div>
  <div style="display: inline;">
      hi,我是第二个div
  </div>
</html>
```

###​	3.display:none

​	同时讲一下与visible:hidden的区别：

​	这两个元素都是隐藏元素的，但是display会在页面上彻底消失，并不占用空间，而visible则会在页面上保留空间

```html
<html>
<head>
  <meta charset="utf-8">
  <title>display:none和visible:hidden的区别</title>
</head>
<body >
  <span style="display:none; background-color:Blue">隐藏区域</span>
  <span style=" background-color:Green">显示区域</span>
  <br />
  <span style="visibility:hidden; background-color:Blue">隐藏区域</span>
  <span style="background-color:Green">显示区域</span>
</body>
</html>
```

###​	4.display:inline-block

```html
<a href="#" style="display:inline;width:100px;height:100px;background:#ccc;">链接一</a>
<a href="#" style="display:inline;width:100px;height:100px;background:#ccc;">链接二</a>

A默认就是一行，所以inline用在这里是废的。宽高度设置也是废的。

<a href="#" style="display:block;width:100px;height:100px;background:#ccc;">链接一</a>
<a href="#" style="display:block;width:100px;height:100px;background:#ccc;">链接二</a>

块状，这里高宽度就生效了，但是因为是块状，前后有换行符，所以这是两行了。

<a href="#" style="display:inline-block;width:100px;height:100px;background:#ccc;">链接一</a>
<a href="#" style="display:inline-block;width:100px;height:100px;background:#ccc;">链接二</a>

这样就是同时达到块状，而且在同一行显示。
```

###​	5.display:list-item:

其实类似于<ol><ul><li>这些标签，区别在于这个适用于比较大的块级列表。

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>

<div>
	<span>aaaa</span>
	<span>bbbb</span>
	<span>cccc</span>
  改变之后：<br/>
    <span style="display:list-item;">aaaa</span>
	<span style="display:list-item;">bbbb</span>
	<span style="display:list-item;">cccc</span>
</div>
</html>
```



## 2.盒模型

以google为例：

 ![盒模型](C:\Users\Shi Qingqing\Pictures\Saved Pictures\盒模型.png)

通俗解释就是：比如我们买了一个iphone,收到了一个很大的快递盒子：

 ![盒子](C:\Users\Shi Qingqing\Pictures\Saved Pictures\盒子.png)



## 3.box-sizing

提到盒模型，之前开发者如果想求出一个div的实际宽度，需要减去padding和border的宽度，才会得到div的实际宽度。

现在css新增了一个box-sizing 的属性，可以免去算数的麻烦。

box-sizing的值有三个：

1.content-box，border和padding不计算入width之内 （default this）

2.border-box，border和padding计算入width之内，其实跟没用并木有神马区别O(∩_∩)O哈！

3.inherit，从父元素继承 box-sizing 属性的值



使用方法：

这个属性有兼容性需要考虑到，因此使用时：

firefox下使用时：

```html
box-sizing:border-box;
-moz-box-sizing:border-box(代表其内核，火狐内核为Gecko Mozilla Firefox)
```

chrome使用时：

```html
box-sizing:border-box;
-webkit-box-sizing:border-box;
```

box-sizing:100px; //for other

****

IE浏览器只支持IE8以上版本。

举例说明：

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>

<style type="text/css">
    .content-box{
        box-sizing:content-box;
        -webkit-box-sizing:content-box;
        width: 100px;
        height: 100px;
        padding: 20px;
        border: 5px solid #E6A43F;
        background: blue;
    }
    .border-box{
        box-sizing:border-box;
        -webkit-box-sizing:border-box;
        width: 100px;
        height: 100px;
        padding: 20px;
        border: 5px solid #3DA3EF;
        background: yellow;
    }
</style>
<div class="content-box">
	第一个div
</div>
<br/>
<div class="border-box">
	第二个div
</div>
</html>
```

解释：

第一个div:

​	实际宽度为：100px+20+20+5+5=150px

​	内容宽度为：100px

第二个div:

​	实际宽度为：100px

​	内容宽度为: 100px-20-20-5-5 = 50px

ps:可以打开google中的盒模型查看



## 4.position

position的值：

| static(default) | 默认值，没有定位，所有的left\top\bottom\right\z-index都会失效 |
| --------------- | ---------------------------------------- |
| absolute        | 绝对定位，可以把元素放在任何想放的位置                      |
| relative        | 相对定位，相对于元素的正常位置进行定位                      |
| fixed           | 根据浏览器窗口来进行元素的定位                          |
| inherit         | 从父元素继承position的值                         |

举例：

### 1.position:static

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
<style>
	.static{
		position:static;
		height:400px;
		width:400px;
		background:yellow;
		left:80px;
		top:80px;
	}
</style>
<div class="static">
	static定位,可以看见left和top并没有生效，元素出现在了常规的位置，并不会被重新定位
</div>
</html>
```

 ### 2.position:absolute

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
<style>
	.static{
		position:static;
		height:400px;
		width:400px;
		background:yellow;
		left:80px;
		top:80px;
	}
	.absolute{
		position:absolute;
		height:200px;
		width:200px;
		background:red;
		left:100px;
		top:80px;
	}
</style>
<div class="static">
	static定位
</div>
<div class="absolute">
	absolute定位，可以看到并不受页面中其他元素的影响，可以随意定位
</div>
</html>
```

 	### 3.position:relative

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
<style>
	.static{
		position:static;
		height:400px;
		width:400px;
		background:yellow;
	}
	.relative{
		position:relative;
		height:400px;
		width:400px;
		background:red;
		bottom: -50px;
	}
</style>
<div class="static">
	这是div的正常定位
</div>
<div class="relative">
	这个div相对于正常位置的div向下移动50px
</div>
</html>
```

	### 4.position:fixed

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
<style>
	.static{
		position:static;
		height:400px;
		width:400px;
		background:yellow;
	}
	.fixed{
		position:fixed;
		height:400px;
		width:400px;
		background:red;
		left:100px;
		top:200px;
	}
</style>
<div class="static">
	这是div的正常定位
</div>
<div class="fixed">
	fixed属性,这时会发现不管如何拉动浏览器的滚动条，这个div的位置都不会发生变动。
	<br/>
	所以他是以body为定位时的对象，总是根据浏览器的窗口来进行元素的定位
</div>
</html>
```



## 5.float浮动

注意：使用float属性的一定是块级元素，不可以是行内元素。如果使用float,则默认给元素加了一个display:block

float的值：

| left    | 向左浮动                |
| ------- | ------------------- |
| right   | 向右浮动                |
| none    | 默认值，元素不会发生浮动        |
| inherit | 任何版本的IE浏览器均不支持这一属性值 |

举例说明:

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
<style>
	.div1{
		width:400px;
		height:100px;
		border:1px solid #F00
	}
	.div2{
		float:left;
		width:150px;
		border:1px solid #00F;
		height:50px
	}
	.div3{
		float:right;
		width:150px;
		border:1px solid #00F;
		height:50px
	}
</style>
<div class="div1">
	<div class="div2">
		向左浮动
	</div>
	<div class="div3">
		向右浮动
	</div>
</div>

</html>
```



## 6.clear控制浮动

clear属性的值：

| left    | 在左侧不允许浮动元素。     |
| ------- | --------------- |
| right   | 在右侧不允许浮动元素。     |
| both    | 在左右两侧均不允许浮动元素。  |
| none    | 默认值，允许浮动        |
| inherit | 所有IE版本均不支持这一属性值 |

### 1.clear:both


```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
<style>
	.div1{
		width:500px;
		background-color: yellow;
		border:1px solid #F00;
		padding:10px;
	}
	.div2{
		float:left;
		width:200px;
		border:1px solid #00F;
		height:150px
	}
	.div3{
		float:right;
		width:200px;
		border:1px solid #00F;
		height:150px;
		
	}
	.clear{clear:both;}
</style>
<div class="div1">
	<div class="div2">
		float left盒子
	</div>
	<div class="div3">
		float right盒子
	</div>
	<div class="clear"></div>
</div>

</html>
```

### 2.clear:left和clear:right

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
<style>
	div{
		width:100px;
		height:20px;
		background-color:yellow;
		border:1px solid red;
	}

</style>
	<h3>如何让四个div显示为两行</h3>
	<div style="float:left;"></div>
	<div style="float:left;"></div>
    <div style="float:left;clear:left;">
    </div><div style="float:left;"></div>
</html>
```

或者：

你会发现在第二个div后面加clear:right了但是并没有起作用，那是因为按照代码执行顺序来说，此时第三个div并没有被加载进来，所以并木有起作用，只要在第三个div加clear:left就ok了

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
<style>
	div{
		width:100px;
		height:20px;
		background-color:yellow;
		border:1px solid red;
	}

</style>
    <div style="float:left;"></div>
	<div style="float:left;clear:right;"></div>
    <div style="clear:left;float:left;"></div>
    <div style="float:left;"></div>
</html>
```

## 7.清除浮动:clearfix hack

不懂的童鞋可以去百度一下css hack,CSS hack的目的就是使你的CSS代码兼容不同的浏览器

举例说明：

当我们需要清除浮动的时候，一般会在div标签结束之前加一个空的标签

```html
<div style="clear:both"></div>
```

虽然只是加了个空标签，但却改变了html的结构

现在只需要在浮动元素的父元素上加一个class=“clearfix”

```html
clearfix{overflow:hidden;zoom:1;}
```

备注：overflow:hidden不显示超过对象尺寸的内容

​	zoom:1放大一倍

示例参考：http://zh.learnlayout.com/clearfix.html



## 8.百分比宽度

可以让浏览器自适应宽度

```html
<!DOCTYPE html>
<html>
	<head>
	<meta charset="utf-8">
	</head>
<style>
	div{
		width:80%;
		height:150px;
		background-color:yellow;
		border:1px solid red;
	}

</style>
    <div>
    	百分比宽度,此时无论怎么变化浏览器的显示窗口，宽度都会变为显示屏宽度的80%
    </div>
	
</html>
```

但是，当窗口非常小的时候，内容会被不友好的显示，选择一种适合的方式。

参考示例：http://zh.learnlayout.com/percent.html

## 9.媒体查询

“响应式设计”，可以让网站针对不同的浏览器和设备自己调整布局。

语法：

```html
@media screen and (min-width:600px) {
  .......
}
```

是指适用于所有计算机彩色屏幕，当最小宽度为600px时执行下列css，前提是使用百分比布局

参考示例：http://zh.learnlayout.com/media-queries.html



## 10.column

这个属性可以让你很轻松的实现多行文字的多列布局

语法：column: [ [column-width](http://www.w3chtml.com/css3/properties/multi-column/column-width.html) ] || [ [column-count](http://www.w3chtml.com/css3/properties/multi-column/column-count.html) ] 每列宽，列的数量

```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
<meta charset="utf-8" />
<style>
body{font:14px/1.5 georgia,serif,sans-serif;}
p{margin:0;padding:5px 10px;background:#eee;}
h1{margin:10px 0;font-size:16px;}
.test{
	width:628px;
	border:10px solid #000;
	-webkit-columns:200px 3;
	columns:200px 3;
}
.test2{
	border:10px solid #000;
	-webkit-columns:200px;
	columns:200px;
}
</style>
</head>
<body>
<h1>列数及列宽固定:</h1>
<div class="test">
	<p>This module describes multi-column layout in CSS. By using functionality described in this document, style sheets can declare that the content of an element is to be laid out in multiple columns. </p>
	<p>On the Web, tables have also been used to describe multi-column layouts. The main benefit of using CSS-based columns is flexibility; content can flow from one column to another, and the number of columns can vary depending on the size of the viewport. Removing presentation table markup from documents allows them to more easily be presented on various output devices including speech synthesizers and small mobile devices.</p>
</div>
<h1>列宽固定，根据容器宽度分布列数:</h1>
<div class="test2">
	<p>This module describes multi-column layout in CSS. By using functionality described in this document, style sheets can declare that the content of an element is to be laid out in multiple columns. </p>
	<p>On the Web, tables have also been used to describe multi-column layouts. The main benefit of using CSS-based columns is flexibility; content can flow from one column to another, and the number of columns can vary depending on the size of the viewport. Removing presentation table markup from documents allows them to more easily be presented on various output devices including speech synthesizers and small mobile devices.</p>
</div>
</body>
</html>
```



## 11.flexbox快速布局神器

参考学习网址：http://www.w3cplus.com/css3/a-guide-to-flexbox.html

​			 http://zh.learnlayout.com/flexbox.html



## 12.css框架

一些常见的css框架

1.[BootMetro](http://www.codeceo.com/article/bootmetro-bootstrap-css.html) - Metro风格的CSS框架

2.[purecss](http://purecss.io/)

3.[bootstrap](http://v3.bootcss.com/)

