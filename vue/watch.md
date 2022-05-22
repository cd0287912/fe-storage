监听响应式数据源的变化，执行响应的回调函数。

watch 接受三个参数：

- 数据源
- 回调函数
- 可选的配置选项

### 监听 ref

```js
// 监听ref定义的响应式数据
const count = ref(0);
function change() {
  count.value++;
}
watch(count, (count, preCount) => {
  console.log("count valur", count, preCount);
});
```

```js
// 监听多个ref定义的响应式数据
const count = ref(0);
const name = ref("张三");
function change() {
  count.value++;
  name.value += "!";
}
watch([count, name], (value, preValue) => {
  // value，preValue 也是返回数组的形式
  console.log("value", value, preValue);
});
```
