### reactive()

接受复杂的数据类型。对深层次的属性生成响应式的转换
自动解包任何 ref 的属性，并保持响应性，除了响应式数组或 Map 这样原生集合类型中为 ref 的元素时，不会解包，仍需.value

```js
const age = ref(20);
const user = reactive({
  name: "张三",
  age,
});

const change = () => {
  user.name = "李四";
  age.value++;
  console.log(user); // 李四  21
};
```

### readonly()

接受一个对象（不论是响应式还是一般的）或是一个 ref，返回一个原值的只读代理

### shallowReactive()

接收复杂数据类型。对浅层的属性生成响应式的转换
