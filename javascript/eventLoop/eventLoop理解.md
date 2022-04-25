### eventLoop理解

js是单线程，解释下语言

事件循环机制由三部分组成:调用栈、消息队列、微任务队列



1.event-loop开始的时候，会全局一行一行的执行遇到函数调用 会压入到栈中被压入的函数被称之为帧 ，当函数返回后会从调用栈中弹出

```js
function fun1(){
	console.log(1)
}
function fun2(){
	console.log(2)
	fun1()
	console.log(3)
}
fun2()

// 1,2,3
```

2.js的异步操作，比如fetch、setTimeout、setInterval压入到调用栈中的时候里面的消息会进去到消息队列中去，消息队列中，会等到调用栈清空之后再执行

```js
function func1(){
	console.log(1)
}
function func2(){
	setTimeout(() => {
		console.log(2)
	},0)
	func1()
	console.log(3)
}
func2()
// 1,3,2
```

3.promise、async、await的异步操作的时候会加入到微任务中去 会在调用栈清空的时候立即执行，调用栈中加入的微任务会立马执行

```js
var p = new Promise((resolve, reject) => {
  console.log(4)
  resolve(5)
})
function func1(){
  console.log(1)
}
function func2(){
  setTimeout(() => {
    console.log(2)
  },0)
  func1()
  console.log(3)
  p.then(value => {
    console.log(value)
  })
}
func2()
// 4,1,3,5,2
微任务里面的消息会比消息队列里面的消息先执行
```

