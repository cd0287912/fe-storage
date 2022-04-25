#### flex 简介

> flex 是弹性布局，是常见的布局方式之一。

任意容器都可以指定为 flex 布局-行内和块级

```css
.box {
  display: flex;
}
.box {
  display: inline-flex;
}
```

容器默认存在两根轴：水平的主轴和垂直的交叉轴。
容器的所有子元素为容器的成员。
flex 分为容器属性和成员属性两部分。

#### 容器属性

##### flex-direction

> 决定排列的方向

- row (默认值)
- row-reverse
- column
- column-reverse

##### flex-wrap

> 是否换行-不换行会挤压元素

- nowrap (默认值)
- wrap note:第一行在上面
- wrapreverse note: 第一行在下面

##### flex-flow

> flex-direction 和 flex-wrap 的简写方式

- 默认为 row nowrap

##### justify-content

> 主轴上的对齐方式

- flex-start (默认) 左对齐
- flex-end 右对齐
- center 居中
- space-around
- space-between

##### align-items

> 交叉轴的对齐方式

- flex-start 交叉轴起点对齐
- flex-end 交叉轴终点对齐
- center 交叉轴居中对齐
- baseline 第一行文字基线对齐
- tretch (默认) 子元素未设置高度或设为 auto，将占满整个容器的高度

##### align-content

> 多跟轴线的对齐方式。若只有一跟轴线，则不起作用

- flex-start 交叉轴起点对齐
- flex-end 交叉轴终点对齐
- center 交叉轴居中对齐
- space-around 每根轴线两侧的间隔都相等
- space-between 与交叉轴两端对齐，轴线之间的间隔平均分布
- stretch (默认) 轴线占满整个交叉轴

#### 成员属性

##### order

> 元素的排列顺序。数值越小，排列越靠前，默认为 0

#### flex-grow

> 定义元素的放大比例。默认为 0，即存在剩余空间，也不放大

#### flex-shrink

> 定义元素的缩小比例。默认为 1，即空间不足，元素将缩小

#### flex-basis

> 定义了在分配多余空间之前，项目占据的主轴空间. 默认为 auto，即元素本身的大小

#### flex

> flex 属性是 flex-grow, flex-shrink 和 flex-basis 的简写，默认值为 0 1 auto。后两个属性可选.该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

#### align-self

> align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性。默认值为 auto，表示继承父元素的 align-items 属性，如果没有父元素，则等同于 stretch。该属性可能取 6 个值，除了 auto，其他都与 align-items 属性完全一致。

- auto
- flex-start
- flex-end
- center
- baseline
- tretch (默认) 子元素未设置高度或设为 auto，将占满整个容器的高度

[flex 练习 青蛙小游戏](http://flexboxfroggy.com/)

[阮一峰 flex 理论篇](https://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

[阮一峰 flex 实践篇](https://www.ruanyifeng.com/blog/2015/07/flex-examples.html)
