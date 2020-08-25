# CSS3新特性

#### 圆角 border-radius

#### 元素阴影 box-shadow

​		[inset] x-offset y-offset  blur-radius spread-radius color

​			insert：为内阴影，是阴影类型的唯一值，可以不加，不加表示外阴影

​			x-offset：向左偏移x轴的值，可以为负数，负数则表示向右偏移x轴的值

​			y-offset：向下偏移y轴的值，可以为负数，负数则表示向上偏移y轴的值

​			blur-radius：阴影模糊半径，可选，只能为正值，值越大，表示元素边缘越模糊，如果为0，则表示不模糊

​			spread-radius：阴影扩展半径，可选，如果为正数，阴影半径则放大，如为负数，阴影半径则缩小。

​			color：阴影的颜色，可选，如果不写，那颜色为浏览器的默认颜色，建议使用rbg颜色，可以设置颜色的透明度。

#### 文字阴影 text-shadow

​	同上

#### 渐变 gradients

​		Linear Gradients（线性渐变） / Radial Gradients（径向渐变）

​			background-image: linear-gradient(direction, color-stop1, color-stop2, ...);

​			background-image: radial-gradient(shape size at position, start-color, ..., last-color);

```css
/*线性渐变*/
background-image: linear-gradient(#e66465, #9198e5); /*上到下*/
background-image: linear-gradient(to right, #e66465, #9198e5); /*左到右*/
background-image: linear-gradient(to right bottom, #e66465, #9198e5); /*左上到右下*/
background-image: linear-gradient(90deg, #e66465, #9198e5); /*角度*/
background-image: repeating-linear-gradient(red, yellow 10%, green 20%) /*重复线性渐变*/
/*径向渐变*/
background-image: radial-gradient(red, yellow, green); /*颜色分布均匀*/
background-image: radial-gradient(red 5%, yellow 15%, green 60%); /*颜色不均匀*/
background-image: radial-gradient(circle, red, yellow, green); /*设置形状 circle（圆形） 或 ellipse（椭圆形，默认）*/
background-image: radial-gradient(closest-side at 60% 55%, red, yellow, black); /*设置大小 closest-side/farthest-side/closest-corner/farthest-corner*/
background-image: repeating-radial-gradient(red, yellow 10%, green 15%); /*重复径向渐变*/ 
```

#### 旋转 transform

​	none：不旋转

​	--- matrix

​	matrix(*n*,*n*,*n*,*n*,*n*,*n*) ：2D转换 / matrix3d(*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*,*n*)：3D转换

​	--- translate （转换）

​	translate(*x*,*y*) / translate3d(*x*,*y*,*z*) / translateX(*x*) / translateY(*y*) / translateZ(*z*)

​	--- scale（缩放）

​	scale(*x*[,*y*]?) / scale3d(*x*,*y*,*z*) / scaleX(*x*) / scaleY(*y*) / scaleZ(*z*)

​	--- rotate（旋转）

​	rotate(*angle*) / rotate3d(*x*,*y*,*z*,*angle*) / rotateX(*angle*) / rotateY(*angle*) / rotateZ(*angle*)

#### 媒体查询

​	@media 媒体类型 and （媒体特性）{你的样式}

​	媒体类型：all、screen（电脑、平板、手机）、print（打印机或打印预览）、speech（屏幕阅读器等发声设备）

​	媒体特性：

```css
/*方法一 */
@media (min-width: 768px) and (max-width: 1024px) {
	.container {
		background-color: orange;				
	}
}
@media (min-width: 1024px){
	.container {
		background-color: pink;
		width: 1090px;
		margin: 0 auto;
	}
}
/*方法二 导入*/
<link rel="stylesheet" href="phone.css" media="(max-width:768px)">
```



#### 多栏布局

```html
<div id="parent">
    <div id="box1">1</div>
    <div id="box2">2</div>
    <div id="box3">3</div>
</div>
```

 1. **float**

    ```css
    /*box都左浮动*/
    #parent > div {
        float: left;
        width: 200px;
        height: 200px;
        text-align: center;
    }
    #box1 {
        background: red;
    }
    #box2 {
        background: yellow;
    }
    #box3 {
        background: green;
    }
    /*box1，2浮动，box3不浮动*/
    #parent > div {
        width: 200px;
        height: 200px;
        text-align: center;
    }
    #box1 {
        float: left;
        background: red;
    }
    #box2 {
        float: left;
        background: yellow;
    }
    #box3 {
        margin-left: 400px;
        background: green;
    }
    ```

 2. #### **inline-block**

    ```css
    #parent > div {
        display: inline-block;
        width: 200px;
        height: 200px;
        text-align: center;
    }
    #box1 {
        background: red;
    }
    #box2 {
        background: yellow;
    }
    #box3 {
        background: green;
    }
    ```

 3. #### **display: flex 弹性布局**

    ```css
    #parent {
    	display: flex;
        flex-direction: row;
    }
    #parent > div{
        width:200px;
        height:200px;
        text-align: center;
    }
    #box1{
        background-color:red;
    }
    #box2{
        background-color:yellow;
    }
    #box3 {
        background-color:blue;
    }
    ```

 4. #### **display: table**

    ```css
    #parent {
        display: table;
    }
    #parent > div{
        display:table-cell;
        width:200px;
        height:200px;
        text-align: center;
    }
    #box1{
        background-color:red;
    }
    #box2{
        background-color:yellow;
    }
    #box3 {
        background-color:blue;
    }
    ```

# CSS中 link 和@import 的区别

- link属于HTML标签，@import是css提供的；
- 页面被加载时，link会同时被加载，@import引用的css会等到页面加载完成再加载；
- @import只在IE5以上才能识别，而link是HTML标签，无兼容问题；
- link方式的样式的权重 高于@import的权重

# 盒子模型

box-sizing: content-box（标准模型） | border-box（IE模型）

content-box - width = content（内容区）

border-box - width - content（内容区）+ padding（内边距）+ border（边框）

# 选择器

**CSS 选择符有哪些？哪些属性可以继承？优先级算法如何计算？ CSS3新增伪类有那些？**

#### 选择器

1.id选择器（ # myid） 

2.类选择器（.myclassname） 

3.标签选择器（div, h1, p） 

4.相邻选择器（h1 + p） 

5.子选择器（ul > li） 

6.后代选择器（li a） 

7.通配符选择器（ * ） 

8.属性选择器（a[rel = "external"]） 

9.伪类选择器（a: hover, li:nth-child）

#### 不可/可继承样式

可继承：font-size、font-family、color、text-indent（首行缩进）[font-*  text-*  list-* color]

不可继承：border、margin、padding、width、height  [background-*  border-*  margin-*  padding-*]

#### 新增伪类

p:first-of-type 选择属于其父元素的首个 <p> 元素。 

p:last-of-type  选择属于其父元素的最后 <p> 元素。 

p:only-of-type  选择属于其父元素唯一的 <p> 元素。 

p:only-child    选择属于其父元素的唯一子元素的每个 <p> 元素。 

p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。 

:enabled  :disabled 控制表单控件的禁用状态。 

:checked        单选框或复选框被选中。

#### 优先级

!important > 内嵌在style属性中的 > id选择器 > 类选择器，伪类选择器，属性选择器 > 元素选择器，伪元素选择器
**优先级就近原则，同权重情况下样式定义最近者为准**

# 清除浮动

**为什么要清除浮动？如何清除？**

原因：

	1. 父元素高度无法撑开，影响与父元素同级的元素
 	2. 与浮动元素同级的非浮动元素会跟随其后
 	3. 若非第一个元素浮动，则该元素之后的元素也需要浮动，否则会影响页面显示的结构

方法：

```css
/*1. 利用clear清除浮动*/
.son {
    clear: left | right | both | auto;
}
```

```html
<!--2. 在父元素后面额外添加标签-->
<div class="parent">
    ...
    <div style="clear:both;"></div>
</div>
```

```css
/*3. 父元素上使用after伪类*/
#parent:after {
    content: '';
    clear: both;
    display: block;
}
```

```css
/*4. 利用overflow清除浮动*/
#parent {
    overflow: auto;
    display: inline-block;
}
```

# 垂直居中

```html
<div class="parent">
    <div class="son"></div>
</div>
```

```css
/*1. margin: auto + position: absoulte*/
.parent {
    width: 400px;
    height: 400px;
    position: relative;
    .son {
        position: absoulte;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        margin: auto;
    }
}
```

```css
/*2. margin-top margin-left 负值（需知道子元素宽高）*/
.parent {
    width: 400px;
    height: 400px;
    position: ralative;
    .son {
        position: absoulte;
        top: 50%;
        left: 50%;
        width: 100px;
        height: 100px;
        /* transform: translate(-50%, -50%); */
        margin-top: -80px;
        margin-left: -50px;
    }
}
```

```css
/*3. flex*/
.parent {
    display: flex;
    align-items: center;
    justify-content: center; /*水平居中*/
}
```

```css
/*4. table-cell(未脱离文档流)*/
.parent {
	display: table-cell;
    vertical-align: middle;
    text-align: center;
}
```

# 水平居中

```css
text-align: center;

margin: 0 auto;

position:absolute +left:50%+ transform:translateX(-50%);

display:flex + justify-content: center;
```

# 用纯CSS创建一个三角形的原理是什么

```css
width: 0;
height: 0;
border-top: 40px solid transparent;
border-left: 40px solid transparent;
border-right: 40px solid transparent;
border-bottom: 40px solid #ff0000;
```

```css
/*下拉框三角*/
.box {
  width: 0;
  height: 0;
  border: 6px solid transparent;
  position: absolute;
  left: 100px;
  top: 50px;
}

.box1 {
  border-bottom: 6px solid #000;
}

.box2 {
  border-bottom: 6px solid #fff;
}
```

# display:none与visibility：hidden的区别

display: none;  不显示对应的元素，在文档布局中不再分配空间（回流+重绘）

visibility: hidden;  隐藏对应的元素，在文档布局中仍保留原来的空间（重绘）

# BFC规范（块级格式化上下文）

BFC规定了内部的Block Box如何布局。
定位方案：
内部的Box会在垂直方向上一个接一个放置。
Box垂直方向的距离由margin决定，属于同一个BFC的两个相邻Box的margin会发生重叠。
每个元素的margin box 的左边，与包含块border box的左边相接触。
BFC的区域不会与float box重叠。
BFC是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
计算BFC的高度时，浮动元素也会参与计算。
满足下列条件之一就可触发BFC
根元素，即html
float的值不为none（默认）
overflow的值不为visible（默认）
display的值为inline-block、table-cell、table-caption
position的值为absolute或fixed

# 上下margin重合的问题

在重合元素外包裹一层容器，并触发该容器生成一个BFC。

```html
<div class="aside"></div>
<div class="text">
	<div class="main"></div>
</div>
```

```css
.aside {
    margin: 20px;
}
.main {
    margin: 20px;
}
.text {
    overflow: hidden; /* 重点，使.main形成一个BFC */
}
```

# CSS优化、提高性能的方法有哪些

避免过度约束

避免**后代选择符**

避免**链式选择符**

使用紧凑的语法

避免不必要的命名空间

避免不必要的重复

最好使用表示语义的名字。一个好的类名应该是描述他是什么而不是像什么

**避免！important，可以选择其他选择器**

尽可能的精简规则，你可以合并不同类里的重复规则

# px pt em rem

px	像素

pt	印刷行业常用的单位(磅)，等于1/72英寸，表示绝对长度

em	em是相对长度单位，基于父级元素的font-size计算字体大小

rem	相对于html根元素，既可以做到只修改根元素就成比例地调整所有字体大小，又可以避免字体大小逐层复合的连锁反应