#### 1. js 预编译的题目

```js
function fn(a, c) {
  console.log(a) // function
  var a = 123
  console.log(a) // 123
  console.log(c) // function
  function a() {}
  if (false) {
    var d = 678
  }
  console.log(d) // undefined
  console.log(b) // undefined
  var b = function () {}
  console.log(b) // function
  function c() {}
  console.log(c) // function
}
fn(1, 2)
```

> // 预编译
> // 作用域的创建阶段 预编译的阶段
> // 预编译的时候做了哪些事情
> // js 的变量对象 -> AO 对象 -> 供 js 引擎自己去访问
> // 1.创建 AO 对象
> // 2.找到形参和变量的声明 作为 AO 对象的属性名值为 undefined
> // 3.实参和形参相统一
> // 4.找到函数声明 会覆盖变量的声明
>
> AO:{
> a: undefined 1 function
> c: undefined 2 function
> d: undefined
> b: undefined
> }

#### 2. this 指向

```js
var name = 222
var a = {
  name: 111,
  say: function () {
    console.log(this.name)
  },
}

var fun = a.say
fun() // -> fun.call(window)
a.say() // -> a.say.call(a)

var b = {
  name: 333,
  say: function (fun) {
    fun()
  },
}
b.say(a.say) // fun.call(window)
b.say = a.say
b.say() // 333
```

#### 3.箭头函数

箭头函数继承自父执行上下文中的 this

```js
var x = 11
var obj = {
  x: 22,
  say: () => {
    console.log(this.x)
  },
}
// 11

var obj = {
  birth: 1990,
  getAge: function () {
    var b = this.birth
    var fn = () => new Date().getFullYear() - this.birth
    return fn()
  },
}
obj.getAge()
```

#### 4.js 作用域

作用域：一般指一个变量的作用范围

```
全局作用域
(1)全局作用域在页面打开时被创建，页面关闭时被销毁
(2)编写script标签中的变量和函数，作用域为全局，在页面任何位置都能访问
(3)全局作用域中有全局对象window，代表一个浏览器窗口，由浏览器创建，可以直接调用
(4)全局作用域中声明的变量和函数会作为window对象的属性和方法保存

函数作用域
(1)调用函数时，函数作用域被创建，函数执行完毕，函数作用域被销毁
(2)每调一次函数就会创建一个新的函数作用域，他们相互独立
(3)函数作用域中可以访问全局作用域的变量，函数作用域外无法访问函数作用域内的变量
(4)函数作用域中访问变量、函数时，会在自身作用域中查找，若没有查到，会在上一级作用域中查找，直到全局作用域

深层理解
执行上下文
- 当函数代码执行前期，会创建一个执行期上下文的内部对象AO（作用域）
- 这个内部的对象是预编译的时候创建出来的 因为当函数被调用时 会先进行预编译
- 在全局代码执行的前期会创建一个执行期的上下文的对象GO

函数作用域预编译
- 创建ao对象AO{}
- 找形参和变量声明 将变量和形参名 当做AO对象的属性名 值为undivided
- 实参形参相统一
- 在函数体里面找函数声明 值赋予函数体

全局作用域的预编译
- 创建GO对象
- 找变量声明 将变量名作为GO对象的属性名 值为undefined
- 找函数声明 值赋予函数体
```

### 5.闭包

```
https://www.bilibili.com/video/BV1sN411974w?p=9
```

### 6.防抖 --- 定时器、闭包

```js
当持续触发事件 一定时间内没有再触发 事件处理函数才会执行
如果设定的时间到来之前 又一次触发了事件 则重新开始延时
function debounce(fn, delay){
	let timer = null
	return function(...args){
		timer && clearInterval(timer)
		timer = setTimeout(() => {
			fn.applay(this, args)
		}, delay)
	}
}
```

### 7.节流

```js
function throttle1(fn, delay) {
  let timeOut = null
  return function (...args) {
    if (!timeOut) {
      fn.call(this, ...args)
      timeOut = setTimeout(() => {
        timeOut = null
      }, delay)
    }
  }
}

function throttle2(fn, delay) {
  let pre = +new Date()
  return function (...args) {
    let now = +new Date()
    if (noe - pre >= delay) {
      fn.apply(this, args)
      pre = now
    }
  }
}
```
