---
title: css布局
date: 2016-10-24T11:05:15.000Z
updated: 2016-10-24T11:05:15.000Z
tags:
  - css
description: css布局技巧。
photos: 'http://oizt3fjv8.bkt.clouddn.com/css_no7.jpg'
---

# flex布局
**注：设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。水平为主轴，垂直为交叉轴**
下面6个属性用于父元素上：

```bash
flex-direction 项目的排列方向：
        row（默认值）：   主轴为水平方向，起点在左端。
        row-reverse：    主轴为水平方向，起点在右端。
        column：         主轴为垂直方向，起点在上沿。
        column-reverse： 主轴为垂直方向，起点在下沿.

flex-wrap 换行：
        nowrap（默认）：   不换行。
        wrap：            换行，第一行在上方。
        wrap-reverse：    换行，第一行在下方。

justify-content 主轴对齐方式：
        flex-start（默认值）：左对齐
        flex-end：           右对齐
        center：             居中
        space-between：      两端对齐，项目之间的间隔都相等。
        space-around：       每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

align-items 交叉轴对齐方式：
        flex-start：   交叉轴的起点对齐。
        flex-end：     交叉轴的终点对齐。
        center：       交叉轴的中点对齐。
        baseline:      项目的第一行文字的基线对齐。
        stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

align-content 多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用,值：
        flex-start：   与交叉轴的起点对齐。
        flex-end：     与交叉轴的终点对齐。
        center：       与交叉轴的中点对齐。
        space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
        space-around： 每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
        stretch（默认值）：轴线占满整个交叉轴。

flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
```

以下6个属性设置在子元素上：

```bash
order         在项目的排列顺序。数值越小，排列越靠前，默认为0。
flex-grow     项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
              如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
flex-shrink   项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
              如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。
flex-basis    可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。
align-self    允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，值与align-items相同。

flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。
```
