---
# flex布局学习
---
## 关于flex布局

> 学习 Flex 布局，你只要学习几个 CSS 属性，就可以写出简洁优雅复杂的页面布局。
<!--more-->
![fle](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-1.jpg)

## Flex布局是什么？
在 flex 容器中默认存在两条轴，水平主轴(main axis) 和垂直的交叉轴(cross axis)，这是默认的设置，当然你可以通过修改使垂直方向变为主轴，水平方向变为交叉轴，这个我们后面再说。

在容器中的每个单元块被称之为 flex item，每个项目占据的主轴空间为 (main size), 占据的交叉轴的空间为 (cross size)。

这里需要强调，不能先入为主认为宽度就是 main size，高度就是 cross size，这个还要取决于你主轴的方向，如果你垂直方向是主轴，那么项目的高度就是 main size。

Flexbox 布局依赖于 flex directions ，简单的说： Flexbox 是一个布局模块，而不是一个属性。采用Flexbox的元素，称为 Flex容器 （flex container），它的所有子元素 （flex item）自动成为容器成员。

跟 LinearLayout 类似， Flexbox 也存在两个方向的布局：主轴（main axis）和副轴（cross axis也称交叉轴），可以简单的理解为 LinearLayout 的水平布局和垂直布局。主轴的开始位置（与边框的交叉点）叫做 main start ，结束位置叫做main end ；交叉轴的开始位置叫做cross start ，结束位置叫做 cross end 。项目默认沿主轴排列。单个项目占据的主轴空间叫做 main size，占据的交叉轴空间叫做 cross size 。

---------------------


### Flex 容器：

Flexbox是Flexible Box的缩写，意为”弹性布局”，它为盒状模型提供了很大的灵活性，让任何一个容器都可以指定为Flex布局。

---
下面代码块分别生成一个块状或行内的 flex 容器盒子。简单说来，如果你使用块元素如 div，你就可以使用 flex，而如果你使用行内元素，你可以使用 inline-flex。
```
.container {
    display: flex | inline-flex;       //可以有两种取值
}


```
Webkit内核的浏览器，必须加上-webkit前缀。

```
.box{
  display: -webkit-flex; /* Safari */
  display: flex;
}
```
**注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。**
---
## Flexbox的属性
Flexbox的属性可以分为 **flex container**属性 和 **flex item** 属性 两类。他们分别对应**父容器**和**子元素**，下面让我们分别看一下他们都是怎么回事。

### 1. flex container 属性（容器的属性）主要包含一下几个方面

 - flex-direction
 - flex-wrap
 - flex-flow
 - justify-content
 - align-content
 - align-items

#### 1.1 flex-direction：属性决定主轴的方向（即项目的排列方向）

```
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

有四个值可以选择：

 - row(默认值)： 主轴为水平方向，起点在左端
 - row-reverse: 主轴为水平方向，起点在右端
 - column : 主轴为垂直方向，起点在上沿
 - column-reverse: 主轴为垂直方向，起点在下沿
![flx](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-2.png)

#### 1.2 flex-wrap属性： 决定容器内项目是否可换行
默认情况下，项目都排在主轴线上，使用 flex-wrap 可实现项目的换行。
```
.container {
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```
- nowrap （默认值）：不换行 
![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-3.png)

- wrap：换行，第一行在上方。
-![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-4.jpg)

- wrap-reverse：换行，第一行在下方。
![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-4.png)



#### 1.3 flex-flow: flex-direction 和 flex-wrap 的简写形式
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为 row || nowrap（“||”代表flex-direction和flex-wrap必须至少有一个，二者之间使用空格隔开，相应的属性请看上面）

```
.box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
```
默认值为: row nowrap，感觉没什么卵用，老老实实分开写就好了。这样就不用记住这个属性了

#### 1.4 justify-content：定义了项目在主轴的对齐方式

```
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```
它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。

- flex-start（默认值）：左对齐
- flex-end：右对齐
- center： 居中
- space-between：两端对齐，项目之间的间隔都相等。
- space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-5.jpg)

#### 1.5 align-content属性: 定义了多根轴线的对齐方式，如果项目只有一根轴线，那么该属性将不起作用
align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

```
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```
该属性可能取6个值。


- flex-start：与交叉轴的起点对齐。
- flex-end：与交叉轴的终点对齐。
- center：与交叉轴的中点对齐。
- space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
- space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- stretch（默认值）：轴线占满整个交叉轴。
![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-5.png)

#### 1.6 align-items属性: 定义了项目在交叉轴上的对齐方式
align-items属性定义项目在交叉轴上(副轴)如何对齐。
```
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```
它可能取5个值。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。


- flex-start：交叉轴的起点对齐。
- flex-end：交叉轴的终点对齐。
- center：交叉轴的中点对齐。
- baseline: 项目的第一行文字的基线对齐。
- stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-6.png)


### 2. flex item（子元素属性）
以下6个属性设置在项目上：
-  order
- flex-grow
- flex-shrink
- flex-basis
- flex
- align-self

#### 2.1 order属性：定义项目在容器中的排列顺序，数值越小，排列越靠前，默认值为 0
默认情况下子元素的排列方式按照文档流的顺序依次排序，而 order 属性可以控制排列的顺序，负值在前，正值在后（和一维坐标系是相似的），按照从小到大的顺序依次排列。 
```
.item {
    order: <integer>;
}
```
![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-9.png)
#### 2.2 flex-grow属性
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

```
.item {
  flex-grow: <number>; /* default 0 */
}
```
![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-10.png)
如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
#### 2.3 flex-shrink属性
flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

```
.item {
  flex-shrink: <number>; /* default 1 */
}
```
![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-11.jpg)

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。

#### 2.4 flex-basis属性
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

```
.item {
  flex-basis: <length> | auto; /* default auto */
}
```
它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

#### 2.5 flex属性
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

```
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```
该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。
#### 2.6 align-self属性
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

```
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```
![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-12.png)

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

# Demo
当屏幕宽度小于 640px 时，调整 Flexbox 的属性以实现第四个元素移动到最前面的效果，而不要改动第一个元素的边框颜色与高度实现。

```
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <title>task10</title>
  <style>
    .container {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .item {
      flex: 0 0 auto;
      width: 150px;
      border: 1px solid #f00;
    }
    .item1 {
      height: 120px;
    }
    .item2 {
      height: 100px;
    }
    .item3 {
      height: 40px;
    }
    .item4 {
      height: 200px;
      border-color: #0f0;
    }
    @media screen and (max-width: 640px) {
      .container {
        display: flex;
        align-items: flex-start;
        flex-wrap: wrap;
      }
      .item4 {
        order: -1;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="item item1">宽度 150px, 高度 120px, 边框颜色 #f00</div>
    <div class="item item2">宽度 150px, 高度 100px, 边框颜色 #f00</div>
    <div class="item item3">宽度 150px, 高度 40px, 边框颜色 #f00</div>
    <div class="item item4">宽度 150px, 高度 200px, 边框颜色 #0f0</div>
  </div>
</body>
</html>
```

![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-demo1.jpg)

![在这里插入图片描述](https://raw.githubusercontent.com/dcpnonstop/blogpic/master/flex-demo2.jpg)




v参考：
<br>
[Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
<br>
---

[30 分钟学会 Flex 布局](https://zhuanlan.zhihu.com/p/25303493)
