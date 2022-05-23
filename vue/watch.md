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

```js
// 监听ref定义的响应式引用对象
const person = ref({
  name: "mike",
  age: 18,
});
function change() {
  person.value.name += "alan";
}
watch(person, (value, oldValue) => {
  // can't watch
  console.log("person.name", value, oldValue);
});
/* 
  无法watch监听，因为person是一个RefImpl所包裹的类型。
  解决：
  1. 监听person.value，使之变为监听person的Proxy（内部为reactive所定义，默认深度监听）
  2. 使用deep为true，使之变为深度监听
*/
```

### 监听 reactive

```js
/* 
  监听reactive所定义的响应式对象全部属性
  注意点：
  1. value 与 oldValue 的值相同，无法正确读取oldValue的值。因为是同一个引用
  2. reactive监听强制开启深度监听，deep配置无效
*/
const person = reactive({
  name: "mike",
  age: 18,
});
function change() {
  person.name = "alan";
  person.age = 20;
}
watch(person, (person, oldPerson) => {
  console.log("person", person, oldPerson);
  // {name: 'alan', age: 20}  {name: 'alan', age: 20}
});
```

```js
/* 
  监听reactive所定义的响应式对象某个属性，注意使用函数返回
  注意点：
  1. 能正确读取oldValue的值
*/
const person = reactive({
  name: "mike",
  age: 18,
});
function change() {
  person.age = 20;
}
watch(
  () => person.age,
  (age, oldAge) => {
    console.log("person.age", age, oldAge);
  }
);
```

```js
/* 
  监听reactive所定义的响应式对象某些属性，注意使用数组函数返回
  注意点：
  1. 能正确读取oldValue的值
*/
const person = reactive({
  name: "mike",
  age: 18,
});
function change() {
  person.age = 20;
  person.name = "alan";
}
watch([() => person.age, () => person.name], (value, oldValue) => {
  console.log("person", value, oldValue);
});
```

```js
/* 
  监听reactive所定义的响应式对象的某个对象属性
  注意点：
  1. 监听深层次对象需要 deep 为true 才能监听
  2. 无法正确读取oldValue的值。因为是同一个引用
*/
const person = reactive({
  name: "mike",
  age: 18,
  job: {
    j1: {
      salary: 20,
    },
  },
});
function change() {
  person.job.j1.salary += 1;
}
watch(
  () => person.job,
  (value, oldValue) => {
    console.log("person.job", value, oldValue);
    //  j1: {salary: 21} ，j1: {salary: 21}
  },
  { deep: true } // 监听深层次对象需要 deep 为true 才能监听
);
```

总结：

1. 监听 reactive 所定义的响应式对象时，默认监听的是所有属性，deep 配置无效且 oldValue 无效，因为是同一引用
2. 监听 reactive 所定义的响应式对象某个基础数据类型时，使用函数返回，且 oldValue 有效
3. 监听 reactive 所定义的响应式对象某个引用数据类型时，使用函数返回, deep 配置有效，但是 oldValue 无效，因为是同一引用

可选的选项配置：

- immedidate 在监听器创建时，立即触发回调
- deep 若源对象是对象，则深度遍历，以便在深层级变更时启动回调
- flush 回调函数的刷新时机
- onTrack / onTrigger：调试侦听器的依赖

### watchEffect

立即运行一个函数，同时响应式的追踪其依赖，依赖改变时，重新执行。
