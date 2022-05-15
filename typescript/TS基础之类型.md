### 常见类型

---

### 原始类型 number | string | boolean

这三个类型是最基本的类型:

- number: 表示所有数字
- string: 表示任意字符串
- boolean: 表示布尔值 true | false

```ts
let a: number = 123;
let b: string = "123";
let c: boolean = true;
```

### 字面量类型

字面量是指将类型设置为具体的数值或字符串等等

一般字面量类型没什么用，但是与联合类型结合或者与非字面量类型结合就十分有用

注意：boolean 其实就是一种联合类型

```ts
let d: 123;
let sex: "male" | "female";
```

### any 类型

表示任意类型，可以被赋予任意值

```ts
let a: any = 123;
a = "hello";
a = true;

let b: string;
b = a; // ok
```

### unknown 类型

表示任意类型，是类型安全的 any

```ts
let a: unknown = 123;
a = "hello";
a = true;

let b: string;
b = a; // error  不能将类型“unknown”分配给类型“string”
```

### void 类型

表示空，一般表示函数没有返回值

```ts
function greet(name: string): void {
  console.log("name is " + name);
}
```

### never 类型

表示不会返回结果，连空这个结果都没有

```ts
function greet() {
  throw new Error("there is a error");
}
```

### object 类型

表示一个对象类型，需要简单的列出它的属性和对应的类型

```ts
type Sex = "male" | "female";

interface Person {
  name: string;
  age: number;
  sex: Sex;
  salary?: number;
  [key: string]: any;
}

const p1: Person = {
  name: "张三",
  age: 18,
  sex: "male",
  salary: 3000,
  friends: ["李四", "王五"],
};
```

- 使用?表示对象属性是否可选
- [key:string]: any 表示还有任意的 keys 属性

在下面的章节会详细剖析对象类型

### array 类型

表示数组，且有一致的类型元素

```ts
let numberArr: number[] = [1, 2, 3];
let stringArr: Array<string> = ["hello", "word"];
```

### tuple 类型

表示固定长度的数组

```ts
let tup: [string, number] = ["hello", 99];
```

### function

函数类型需要知道 函数参数的类型，以及返回值的类型

匿名函数 ts 会根据上下文自动推断

```ts
function greet(name: string): string {
  return "hello " + name;
}

type Green = (name: string) => string;
const green2: Green = (name) => {
  return name;
};

let stringArr: Array<string> = ["hello", "word"];
stringArr.forEach((item) => {
  console.log(item.length);
});
```

### enum 类型

表示一个枚举类

```ts
enum Gender {
  Male,
  Female,
}

interface Person {
  name: string;
  sex: Gender;
}

const person: Person = {
  name: "张三",
  sex: Gender.Male,
};
```

### Union 类型

一个联合类型是由两个或者更多类型组成的类型，表示值可能是这些类型中的任意一个。这其中每个类型都是联合类型的成员（members）。

```ts
let age: string | number = 123;
age.toString(); // ok
age.toLocaleLowerCase(); // error
```

定义一个 age 可是以 string 或者是 number。当操作一个联合类型时，必须对没个成员都有效或者是对其类型收窄。

### 定义类型的方式

---

### 类型别名 type

```ts
type Point = {
  x: number;
  y: number;
};
type ID = number | string;
```

### 接口 interface

```ts
interface Point {
  x: number;
  y: number;
}
```

type 与 interface 的区别:

1. interface 通过 extends 继承扩展，type 通过 & 结合扩展
2. interface 可以通过定义同名的方式新增字段，type 则不可以

### 类型断言

---

有时候我们比 ts 编译器更知道一个值的类型，我们可以使用类型断言。

断言表示更具体。

```ts
const canvasDom = <HTMLCanvasElement>document.getElementById("#canva");
const canvasDom = document.getElementById("#canva") as HTMLCanvasElement;
```

我们知道 DOM 为 HTMLCanvasElement 而不仅仅是 HTMLElement，我们就可以使用断言，更加精确其类型。类型断言会被编译器移除，并且不会影响任何运行时的行为。

可以使用 <> 或者 as 断言，在 tsx 中仅支持 as 断言。

### 非空断言操作符 (后缀!)

TypeScript 提供了一个特殊的语法，可以在不做任何检查的情况下，从类型中移除 null 和 undefined，这就是在任意表达式后面写上 ! ，这是一个有效的类型断言，表示它的值不可能是 null 或者 undefined：

```ts
function liveDangerously(x?: number | null) {
  // No error
  console.log(x!.toFixed());
}
```

当你明确的知道这个值不可能是 null 或者 undefined 时才使用 ! 。
