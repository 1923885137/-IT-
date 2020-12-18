# 继承

> 如果一个元素的某个属性没有层叠值，则可能会继承祖先某个元素的值

> 继承一般是顺着DOM树向下传递的

<img src="D:\互联网专业知识\css\imgs\IMG_20201217_160604.jpg" style="zoom: 33%;" />

## 可以被继承的属性

> 默认情况下，只有特定的一些属性能被继承，通常是跟文本相关的属性

> color,font,font-family,font-size,font-weight,font-variant,font-style,line-height,letter-spacing,text-align,text-indent
>
> text-transform,white-space,word-spacing

注：

1.**font-variant** 属性设置小型大写字母的字体显示文本，这意味着所有的小写字母均会被转换为大写，但是所有使用小型大写字体的字母与其余文本相比，其字体尺寸更小。

2.**text-transform** 属性控制文本的大小写。

3.**white-space** 属性设置如何处理元素内的空白。

4.**word-spacing** 属性增加或减少单词间的空白（即字间隔）

> 还有列表属性：list-style,list-style-type,list-style-position,list-style-image

>  表格的边框属性中的border-collapse和border-spacing

1.**border-collapse** 属性设置表格的边框是否被合并为一个单一的边框，还是象在标准的 HTML 中那样分开显示。

2.**border-spacing** 属性设置相邻单元格的边框间的距离（仅用于“边框分离”模式）。

> div边框等属性默认不可继承

## 特殊值：inherit和initial

### 1.inherit

> 有时候，我们想用继承代替层叠值，就可以使用inherit关键字，该元素的该属性就会继承父元素的值

```css
.footer a{
    color:inherit;
}
//作用在于，子属性会跟着父属性一起变
```

### 2.initial

> 有时候我们需要撤销作用于某个元素的样式，恢复其默认值，可以使用initial关键字来实现

>  好处在于：元素的默认值不都是一致的，如width：auto  color：black，在修改的时候使用initial会更方便

> 注：display的默认值是inline，不管应用于哪个元素，它的initial都不会变为block，因为initial重置为属性的初始值而不是元素的初始值

# 简写属性

> 用于给多个属性赋值的属性，如font，可以用于设置多个字体属性

## 1.font

> 顺序为font-style,font-weight,font-size,font--height,font-family

```css
*{
    font:italic bold 18px/1.2 "Helvetica","Arial",sans-serif;
}
```

## 2.background

> 摘引链接：https://blog.csdn.net/wjnf012/article/details/80222339 ----[爱编程的兔子](https://blog.csdn.net/wjnf012)

> - background-color*/\*背景颜色（CSS1）\*/* 
> - background-image*/\*背景图片（CSS1）\*/* 
> - background-position*/\*背景图片的位置（CSS1）\*/* 
> - background-size*/\*背景图片的大小（CSS3）\*/* 
> - background-repeat*/\*背景图片重复方式（CSS1）\*/* 
> - background-origin*/\*背景图片的定位区域（CSS3）\*/*
> -  background-clip*/\*背景背景图片绘画区域（CSS3）\*/* 
> - background-attachment*/\*背景图片是否固定或随着页面其余部分滚动（CSS1）\*/*

> **background: color image position/size repeat origin clip attachment initial | inherit;**

## 3.border

> border-width,border-style,border-color

> border-width是上，右，下，左四个边框宽度的简写属性（顺时针）这同样适合于padding，margin

## 4.box-shadow text-shadow background 只支持水平和 垂直两个属性

```css
box-shadow: 10px 2px #6f9090;
//阴影向右偏移10px，向下偏移2px
```



## 4.简写属性的一些弊病

> 1.简写属性会默认覆盖其它样式

  我们在写简写属性的时候，可以省略一些值，只写我们关注的值。但这样做，在渲染的时候还是会设置省略的值，即他们隐式地被设置为了初始值，会默默覆盖在其它地方定义的样式。如，在简写font属性的时候，若省略font-weight，那么字体粗细就会被设置为normal。

```css
h1 {
    font-weight:bold;
}
.title {
    font: 32px Helvetica,Arial,sans-serif;
}
//<h1 class = "title">的标题并不会被加粗
```

> 2.上下左右

```css
padding: 1em 2em;//上下 左右
padding: 1em 2em 1em;//上 左右 下 这种设置方式是需要特别注意的
padding :1em 2em 1em 2em;//上 右 下 左
//这三者是等价的
```

