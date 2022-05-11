### JavaScript 有哪些数据类型，它们的区别？

js 的数据类型 有引用数据类型 以及 基础数据类型。

undefined, null , string, number, boolean, object, symbol, bigInt

两种数据类型，存储的位置不同。分为栈内存与堆内存。

### var let const 的区别?

1. let，const 拥有块级作用域
2. 变量提升，var 存在变量提升，let、const 不存在
3. 添加全局属性 var 声明的变量会变为全局属性，let、const 则不会
4. 重复声明 var 声明的变量可以重复声明，let，const 不允许
5. 暂时性死区 var 不存在暂时性死区，let,const 存在不声明无法使用

### new 操作符实现步骤？

1. 创建一个空对象
2. (将构造函数的作用域赋给新对象)把对象的原型指向构造函数原型
3. 将构造函数的 this 指向新对象
4. 返回对象

```js
function mynew(Fun, ...args) {
  // 1.创建一个新对象
  const obj = {};
  // 2.把对象原型指向构造函数的原型
  obj.__proto__ = Fun.prototype;
  // 3.将构造函数的this指向对象
  let result = Fun.call(obj, ...args);
  // 根据值返回对象
  return result instanceof Object ? result : obj;
}
```

### 箭头函数与普通函数的区别？

1. 箭头函数更加简洁
2. 箭头函数没有自己的 this
3. 箭头函数不能改变 this 指向
4. 箭头函数没有 prototype，没有构造函数
5. 箭头函数没有 arguments

### 箭头函数的 this 指向哪⾥？

箭头函数不同于传统 JavaScript 中的函数，箭头函数并没有属于⾃⼰的 this，它所谓的 this 是捕获其所在上下⽂的 this 值，作为⾃⼰的 this 值，并且由于没有属于⾃⼰的 this，所以是不会被 new 调⽤的，这个所谓的 this 也不会被改变。

### 扩展运算符的作用及使用场景？

1. 对象扩展 -> 复制对象，合并对象
2. 数组扩展 -> 复制数组，合并数组，转为参数序列，任何 Iterator 接口的对象，都可以用扩展运算符转为真正的数组

### 解构运算

1. 数组解构。以元素的位置为匹配条件来提取想要的数据
2. 对象解构。以以属性的名称为匹配条件，来提取想要的数据的

### ES6 字符串的扩展

1. 模板字符串
2. 系列方法 includes() startsWith() endsWith()

### ES6 数组的扩展

1. Array.from() Array.of()
2. find() findIndex()
3. includes()
4. fill()

### ES6 对象的扩展

### 创建对象的方式

1. 工厂模式创建对象
2. 构造函数创建对象
3. 原型模式创建对象
4. 结合构造与原型模式创建对象
5. 动态原型模式
6. 寄生构造函数模式

### 继承对象的方式

1. 原型链的方式来实现继承
2. 借用构造函数的方式
3. 原型链和借用构造函数组合起来
4. 原型式继承
5. 寄生式继承
6. 寄生式组合继承

### 垃圾回收机制

1. 引用计数 （常用）
2. 标记清除
