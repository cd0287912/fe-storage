### 前言

在前面中我们说了执行可执行代码，会产生一个执行上下文。每一个执行上下文都有三个属性:

- **变量对象(Variable object，VO)**
- **作用域链(Scope chain)**
- **this**

这篇我们就讲讲 this

**this 的指向，是在函数被调用的时候确定的。也就是执行上下文被创建时确定的，且在函数执行过程中，this 一旦被确定，就不可更改了。**

简单例子:

```js
var name = "张三";
var person = {
  name: "李四",
};
function fn() {
  console.log(this.name);
}
fn();
fn.call(person);
```

### 全局中的 this

全局中 this 就指向 window 一种情况，比较简单

```js
console.log(this); // Window
```

### 函数中 this

在一个函数上下文中，this 由调用者提供，由调用函数的方式来决定。如果调用者函数，被某一个对象所拥有，那么该函数在调用时，内部的 this 指向该对象。如果函数独立调用，那么该函数内部的 this，则指向 undefined。但是在非严格模式中，当 this 指向 undefined 时，它会被自动指向全局对象。

```js
// 为了能够准确判断，我们在函数内部使用严格模式，因为非严格模式会自动指向全局
function fn() {
  "use strict";
  console.log(this);
}

fn(); // fn是调用者，独立调用
window.fn(); // fn是调用者，被window所拥有
```

从结论中我们可以看出，想要准确确定 this 指向，找到函数的调用者以及区分他是否是独立调用十分关键。

```js
// demo1
var a = 20;
function fn() {
  console.log(this.a);
}
fn();
```

```js
// demo2
var a = 20;
function fn() {
  function foo() {
    console.log(this.a);
  }
  foo();
}
fn();
```

```js
// demo3
var a = 20;
var obj = {
  a: 10,
  c: this.a + 20,
  fn: function () {
    return this.a;
  },
};

console.log(obj.c);
console.log(obj.fn());
```

在 demo03 中，对象 obj 中的 c 属性使用 this.a + 20 来计算。这里我们需要明确的一点是，单独的{}不会形成新的作用域，因此这里的 this.a，由于并没有作用域的限制，它仍然处于全局作用域之中。所以这里的 this 其实是指向的 window 对象。

```js
// demo4
var a = 20;
function foo() {
  var a = 1;
  var obj = {
    a: 10,
    c: this.a + 20,
    fn: function () {
      return this.a;
    },
  };
  return obj.c;
}
console.log(foo()); // ？
console.log(window.foo()); // ?
```

```js
// demo5
var a = 20;
var foo = {
  a: 10,
  getA: function () {
    return this.a;
  },
};
console.log(foo.getA()); // 10

var test = foo.getA;
console.log(test()); // 20
```

```js
// demo6
var a = 20;
function getA() {
  return this.a;
}
var foo = {
  a: 10,
  getA: getA,
};
console.log(foo.getA()); // 10
```

```js
// demo7
function foo() {
  console.log(this.a);
}

function active(fn) {
  fn(); // 真实调用者，为独立调用
}

var a = 20;
var obj = {
  a: 10,
  getA: foo,
};

active(obj.getA);
```
