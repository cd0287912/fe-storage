### 1.手写 call/apply

```js
Function.prototype.lvCall = function (context) {
  if (typeof this != "function") {
    throw new Error("there need a function");
  }
  context = context || window;
  const arg = [...arguments].slice(1);
  context.fn = this;
  const result = context.fn(...arg);
  delete context.fn;
  return result;
};

Function.prototype.lvApply = function (context) {
  if (typeof this != "function") {
    throw new Error("there need a function");
  }
  context = context || window;
  context.fn = this;
  let arg = arguments[1];
  let result;
  if (arg) {
    result = context.fn(...arg);
  } else {
    result = context.fn();
  }
  delete context.fn;
  return result;
};
```

### 2.深浅拷贝

1.浅拷贝

- 创建一个新的对象
- 拷贝值，如果属性为一般属性 拷贝的就是基本类型的值 如果属性是引用类型那么拷贝的就是 内存地址

```js
function shallowClone(source) {
  var newObj = {};
  for (var i in source) {
    if (source.hasOwnProperty(i)) {
      newObj[i] = ssource[i];
    }
  }
  return newObj;
}
```
