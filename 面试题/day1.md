- 谈一谈 `css` 盒模型
- `display` 都有哪些属性
- 块元素和行内元素、行内块元素的区别
- `js` 原型和原型链
- `Person.prototype.constructor` 是什么
- 函数有没有 `__ proto __` 属性
- 谈一谈 `js` 数据类型
- 如何判断数据类型的多种方式，有什么区别，适用场景
- `Promise` 如何一次进行多个异步请求
- `Promise.all` 的返回机制是什么
- 如果想要其中一个请求出错了但是不返回结果怎么办
- `webpack` 打包优化知道多少
- 大前端了解吗
- `koa` 如何启动一个服务器
- `new koa` 都做了什么
- `koa` 洋葱圈模型原理
- `koa` 洋葱圈和 `express` 中间件有什么区别
- 长列表优化，一万条数据不用分页和懒加载，如何提升性能
- 数据请求从发起到接收数据之间发生了什么
- 前端安全了解吗
- `csrf` 和 `xss` 是什么，如何避免
- 前端怎样对用户的数据进行加密传输
- 基于 `md5` 提升安全性

##### 1.谈一谈盒模型

```html
盒模型有 标准盒模型（box-sizing:content-box） 和 IE盒模型(box-sizing:border-box) 两种
盒模型有 margin border padding content组成
标准盒模型中 width\height 是指内容区域的宽高
IE盒模型中 width\height 是指内容区域的宽高+border+padding的宽高

如何获取盒模型对应的宽高
1.DOM节点style属性
element.style.width/height
缺点：只能获取行内样式的，不能获取内嵌和外链的样式
2.通用型
2.1 getComputedStyle (chrome)
getComputedStyle(element).width/height
2.2 currentStyle (IE)
element.currentStyle.width/height (IE)
3.getBoundingClientRect 获取DOM的绝对位置

盒子注意点：
margin塌陷问题
解决方案
BFC（Block Formatting Context）：块级格式化上下文
1.overflow 不为none
2.float 不为none
3.posiiton 不为static
4.display 为 inline-block, table-cell, table-caption, flex, inline-flex

拓展：
DOM元素各种 clientwidth clientLeft offsetLeft 等等 属性知识
```

##### 2.`display` 都有哪些属性

```js
none、block、inline-block、inline、inherit、static、flex、grid、table等等

拓展：
flex
gird
```



