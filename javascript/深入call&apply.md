### 简介

> call 和 apply 都是改变 this 指向，并立即执行.两者的区别是传入的参数的方式不同

```js
const foo = {
  value: "foo",
}
function bar() {
  console.log(this.value)
}
bar() // undefined
bar.call(foo) // foo
```

### call 实现

函数才有 call 和 apply 方法，所以我们在其原型上实现

```js
Function.prototype.myCall = function (context, ...args) {
  if (context === null) context = globalThis
  if (!(typeof context != "object")) context = Object(context)
  // context 目标this上下文
  // 原理是目标函数在其context上下文实现代码的执行，那么这是this指向就是这个context上下文
  const symbol = Symbol("key")
  context[symbol] = this
  try {
    return context[symbol](...args)
  } finally {
    delete context[symbol]
  }
}
```

注意点:

- 传入的 context 上下文，其类型是否满足在其属性上挂执行函数
- context 的属性要满足唯一，不能覆盖原对象
- 要有参数，要有返回值,并且删除挂载的对象属性

### apply 实现

```js
Function.prototype.Myapply = function (context, args) {
  if (context === null) context = globalThis
  if (!(typeof context != "object")) context = Object(context)
  const symbol = Symbol("key")
  context[symbol] = this
  try {
    return context[symbol](...args)
  } finally {
    delete context[symbol]
  }
}
```
