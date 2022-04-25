### promise理解和使用

> promise是js中进行异步编程的新的解决方案（旧的方案呢？）
>
> 具体：从语法上来讲：promise是一个构造函数，从功能上讲promise对象用来封装一个异步操作并可以获取其结果

### promise状态改变

1.pendding 变为 resolved

2.pendding变为rejected

说明：

* 无论这两种，且一个promisse对象只能改变一次

* 无论变为成功还是失败，都会有一个数据结构
* 成功的结构数据一般为value，失败的结果数据一般为reason



```js
// 1.创建一个promise对象
const p = new Promise((resolve, reject) => { //执行器函数
	// 2.执行异步操作任务
	// 3.1 如果成功，调用resolve(value)
	// 3.2 如果失败，调用rejecte(reason)
})

p.then(
  value => {},   // 接收得到成功的value数据   --- onResolved
  resonse => {}  // 接收得到失败的reason数据  --- onRejected
)
```

### promise优点

1.指定回调函数的方式更加灵活

​	回调函数方式---> 必须指定回调函数

​	promise方式 ---> 启动异步任务-->返回promise对象-->给promise对象绑定回调函数

2.支持链式调用，解决回调地狱的问题

​	解决方案->promises链式调用

​	终极方案->async/await

#### 如何使用Promise --api

1.Promise构造函数：Promise(excutor){}

- excutor函数： 执行器 (resolve, reject) => {}
- resolve函数：内部定义成功时我们调用的函数 value => {}
- reject函数: 内部定义失败时我们调用的函数 reason => {}
- 说明：excutor会在Promise内部立即同步回调，异步操作在执行器中执行,then 回调时异步的

2.Promise.prototype.then 方法： (onResolved, onRejected) => {}

* onResolved函数： 成功的回调函数 （value） => {}
* onRejected函数： 失败的回调函数 reason => {}
* 说明：指定用于得到成功的value的成功回调和用于得到失败reason的失败回调返回一个新的promise对象

3.Promise.prototype.catch 方法： （onRejected）=> {}

* onRejected函数： 失败的回调函数 （reason）=> {}
* 说明：then()的语法糖，相当于 then(undefined, onRejected)

4.Promise.resolve方法： value => {}

* value： 成功的数据或promise对象
* 说明：返回一个成功/失败的promise对象

5.Promise.reject方法： reason => {}

* reason: 失败的原因
* 说明： 返回一个失败的promise对象

6.Promise.all方法： （promises）=> {}  

- promises: 包含n个promise的数组
- 说明：返回一个新的promise，只有所有的promise都成功才成功，只要有一个失败就直接失败

7.Promise.race方法： promises）=> {}  

- promises: 包含n个promise的数组
- 说明：返回一个新的promise，第一个完成的promise的结果状态就是最终的结果状态

### 注意点

1.改变promise状态和指定回调函数谁先谁后？

- 都有可能，正常情况下是先指定回调函数在改变状态，但也可以先改变状态再指定回调
- 如何先改变状态在指定回调？
  - 在执行器中直接调用resolve() / reject()
  - 延长更长时间才调用then()
- 什么时候才能得到数据？
  - 如果先指定的回调，那当状态发生变化时，回调函数就会调用，得到数据
  - 如果先改变的状态，那当指定回调时，回调函数就会调用，得到数据

2.promise.then()返回的新promise的结果状态由什么决定？

- 简单表达：由then()指定的回调函数执行的结果决定
- 详细表达：
  - 如果抛出异常，新promise变为rejected，reason为抛出的异常
  - 如果返回的是非promise的任意值，新promise变为resolved，value为返回值
    - 如果返回的是另一个新promise，此promise的结果就会成为新promise的结果

```js
new Promise((resolve, reject) => {
  reject(2)
})
  .then(
    (value) => {
      console.log("value1", value)
    },
    (reason) => {
      console.log("reason1", reason)
      return Promise.reject(3)
    }
  )
  .then(
    (value) => {
      console.log("value2", value)
    },
    (reason) => {
      console.log("reason2", reason)
    }
  )
```

3.promise如何串联多个操作任务？

- promise的then()返回一个新的promise，可以看成then()的链式调用
- 通过then的链式调用串联多个同步/异步任务
- 注意：串联异步任务的时候 一定要返回新的promise

4.promise异常穿透？

- 当使用promise的then链式调用时，可以在最后指定失败的回调
- 前面任何操作出了异常，都会传到最后失败的回调中处理（逐层传递）

5.中断promise链？

- 当使用promise的then链式调用时，在中间中断，不再调用后面的回调函数
- 方法：在回调函数中返回一个pendding状态的promise对象