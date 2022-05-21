### 前言

`useEffect` 是自变量 `hook` 之一。它让使用者在函数组件中执行副作用操作。

什么是副作用?

在 react 中视图渲染 UI = f(state)。这是个理想操作，但大部分情况我们会发起异步请求，打印，手动修改 DOM 等等，这些就称之为副作用。

react 中副作用的执行时机，1.state 改变、2.UI render、3.执行副作用。

```ts
function App() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `click ${count} times`;
  });
  return (
    <>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </>
  );
}
```

在 react 中，在 useEffect 中执行副作用的行为。useEffect 接受两个参数，第一个是回调函数，即在副作用的逻辑都写在里面，第二个参数是依赖项，可选参数。该参数决定了副作用逻辑执行的时机。

若第二个参数依赖没有传递，那么每次 UI 渲染后，副作用函数都会执行。

若想定义某一个状态变化时，执行副作用函数，那么依赖项就可以传入依赖某个状态的数组。

当然依赖项也可以传入空数组，表示依赖项不会发生变化，那么副作用函数仅仅在第一次 UI 渲染后执行。

```ts
function App() {
  const [count, setCount] = useState(0);
  const [show, setShow] = useState(false);
  useEffect(() => {
    console.log("UI 每次渲染 都会执行");
  });
  useEffect(() => {
    // 仅仅count发生改变时执行
    document.title = `click ${count} times`;
  }, [count]);
  useEffect(() => {
    // 仅仅show发生改变时执行
    document.title = `show ${show} now`;
  }, [show]);
  useEffect(() => {
    console.log("第一次UI渲染后执行，就不会在执行了");
  }, []);
  return (
    <>
      <h1>{show.toString()}</h1>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>+1</button>
      <button onClick={() => setShow(!show)}>changeShow</button>
    </>
  );
}
```

有时候副作用会留下一些痕迹，我们要清除副作用对程序的影响。

...
