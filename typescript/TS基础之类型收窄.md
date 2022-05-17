类型收窄指联合类型中，确定某一具体的类型。

### typeof 类型保护

`typeof` 返回运行时一个值的基本类型信息。

- string
- number
- bigint
- boolean
- symbol
- undefined
- object
- function

注意 `null` 类型 `typeof` 值为 `object`。

```ts
function printAll(strs: string | string[] | null) {
  if (typeof strs === "string") {
    console.log(strs.toUpperCase());
  }
  if (typeof strs === "object") {
    strs.join(); // error maybe is null
  }
}
```

### 真值收窄

在 js 中，如 `''`、`null`、`undefined`、`NaN`、`0` 都会进行隐式转换为 `false`，其他的为 `true`。

所以我们可以用是否真值来进行类型的约束。

```ts
function printAll(strs: string | string[] | null) {
  if (strs) {
    // ...   strs type is string or string[]
  }
}
```

注意空字符串隐式转换也为 false。

### 等值收窄

等值收窄指可以使用 `===`、`!==`、`==`、`!=` 去收窄类型。

```ts
function printAll(strs: string | string[] | null) {
  if (strs !== null) {
    // ...   strs type is string or string[]
  }
}
```

js 中的宽松操作如 `==` 、`!=` ，也可以进行类型收窄。在 JavaScript 中，通过 ` == null` 这种方式并不能准确的判断出这个值就是 `null`，它也有可能是 `undefined` 。对 `== undefined` 也是一样，不过利用这点，我们可以方便的判断一个值既不是 `null` 也不是 `undefined` 。

```ts
function printAll(strs: string | null | undefined) {
  if (strs != null) {
    // ...   strs type is string
  }
}
```

### in 操作符收窄

在 js 中一个 `in` 操作符判断属性是否存在于目标对象中。TypeScript 也可以通过这个收窄类型。

```ts
type Bird = { fly: () => void };
type Dog = { run: () => void };

function move(animal: Bird | Dog) {
  if ("fly" in animal) {
    // animal type is Bird
  }
}
```

### instanceof 收窄

在 js 中 `instanceof` 判断对象的类型。TypeScript 也可以通过这个收窄类型。

```ts
function format(time: Date | string) {
  if (time instanceof Date) {
    // time type is date
  }
}
```

### 赋值语句 收窄

```ts
let age: number | string;
age = 20;
age.toFixed();
age = "18";
age.toUpperCase();
age = true; // error
```

### 控制流收窄

```ts
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return new Array(padding + 1).join(" ") + input;
  }
  return padding + input;
}
```

判断中进入第一个条件判断，有 return 语句，那么代码就不会往下执行。那么剩余代码的类型可判断为 `string` 。
