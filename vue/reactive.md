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

### shallowReactive()

接收复杂数据类型。对浅层的属性生成响应式的转换,对深层次的属性不具备响应式。

```js
const person = shallowReactive({
  name: "mike",
  hobby: ["work", "game"],
  job: {
    j1: {
      name: "IT",
    },
  },
});
function change() {
  person.name = "alan";
}
function changeHobby() {
  person.hobby[0] = "xxx"; // not work
}
function changeJon() {
  person.job.j1.name = "teacher"; // not work
}
```

### readonly()

接受一个对象（不论是响应式还是一般的）或是一个 ref，返回一个原值的只读代理

```js
let person = reactive({
  name: "mike",
  age: 18,
  job: {
    j1: {
      name: "IT",
    },
  },
});
person = readonly(person);
function change() {
  person.name = "alan"; //not work
}
```

```js
let person = ref("mike");
person = readonly(person);
function change() {
  person.value = "alan"; //not work
}
```

### shallowReadonly()

与 readonly 类型，它是浅层次的只读。

```js
let person = reactive({
  name: "mike",
  age: 18,
  job: {
    j1: {
      name: "IT",
    },
  },
});
person = shallowReadonly(person);
function change() {
  person.name = "alan"; //not work
}
function changeJob() {
  person.job.j1.name = "alan"; //work
}
```
