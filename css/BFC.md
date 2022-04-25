#### BFC 是什么?

> BFC 全称：Block Formatting Context， 名为 "块级格式化上下文"。简单来说就是，BFC 是一个完全独立的空间（布局环境），让空间里的子元素不会影响到外面的布局。

#### 如何触发 BFC?

触发 BFC 使用 css 属性

- overflow:auto | hidden | scroll (非 visible)
- position: absolute | fixed (非 relative)
- float : left | right （非 none）
- display : inline-block | table-cell | table-caption | flex | grid
  (非 none | inline | block)

#### BFC 解决的问题

- 子元素浮动引起的父元素高度塌陷
- margin 边距重叠
- margin 塌陷
- float 文字环绕
- 元素被浮动元素覆盖
