### ref()

- ref 函数接受一个值,包裹这个值返回一个响应式 ref 对象,并且通过.value 来访问,通常使基础数据类型数据具有响应式.
- 若将一个对象赋值给 ref，那么这个对象将通过 reactive() 转为具有深层次响应性的对象。
- 模板中不需要.value,会自动解包

```vue
<script setup lang="ts">
import { ref } from "vue";
let message = ref("hello");
const change = () => {
  message.value = "word";
};
</script>
<template>
  <div>{{ message }}</div>
  <button @click="change">change</button>
</template>
```

### shallowRef()

> 在 ref 中传入对象,底层会通过 reactive()进行转化，使其每个对象属性具有响应式，若不想每个对象都具有响应式，节约性能，那么则使用 shallowRef，shallowRef 不会深层次的递归使其每个属性转为响应式，只会对象本身具有响应式

```vue
<script setup lang="ts">
import { shallowRef } from "vue";
let user = shallowRef({
  name: "张三",
});
const change = () => {
  // user.value.name = "李四"   //not valid
  user.value = {
    name: "李四",
  };
};
</script>
<template>
  <div>{{ user.name }}</div>
  <button @click="change">change</button>
</template>
```

### triggerRef()

> 在上个列子 shallowRef 中，改变 user.value.name = "李四"，不会生效、因为 shallowRef 是浅层的 ref，若想使其生效，必须搭配 triggerRef(ref)使用，强制触发视图刷新

### customRef()

> 创建一个自定义的 ref，显式声明对其依赖追踪和更新触发的控制方式。

```vue
function myRef<T>(value: T) {
  return customRef((trank, trigger) => {
    return {
      get() {
        trank();
        return value;
      },
      set(newValue: T) {
        value = newValue;
        trigger();
      },
    };
  });
}
```

- `customRef()` 预期接受一个工厂函数，这个工厂函数接受 `track` 和 `trigger` 两个函数作为参数，并应该返回一个带 `get` 和 `set` 方法的对象。
- 一般来说，`track()` 应该在 `get()` 方法中调用，而 `trigger()` 应该在 `set()` 中调用。然而，你对它们该怎么调用、需不需要调用都有完全的控制权。
