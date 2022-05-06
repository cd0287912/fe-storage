### 前言

useState 是自变量 hook 之一。它的改变会引入视图的重新渲染，函数组件也会重新执行。

### useState

useState 它是利用闭包，在函数内部创建一个当前函数组件的状态，并提供了一个修改改状态的方法。

useState 返回一个数组，第一个值是当前的值，第二个是修改值的方法。

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount(count + 1)}>click</button>
    </div>
  );
}
```

注意：useState 的改变值的方式是覆盖而不是合并，这与 this.setState 是不同的

useState 还可以接受一个函数作为参数，返回一个初始值，这个函数只会在组件首次渲染时执行。

### 状态异步

状态都是异步的，当你去修改状态后，你无法拿到状态最新的值，而之后到下一个事件循环周期执行时，状态才是最新的值。

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  const changeCount = () => {
    console.log(count);
    setCount(count + 1);
    console.log(count);
  };
  return (
    <div>
      <h1>{count}</h1>
      <button onClick={changeCount}>click</button>
    </div>
  );
}
```

### 过时的状态

有时候我们拿到的不是最新的状态的值，比如基于 count 设置新值的时候，我们当前拿到的 count 不是最新值。即所谓的闭包陷阱。

如下，没有正确设置 deps 数组的值，count 始终没有变，但是设置了 deps 也有问题，因为 count 每次改变都会重新生成一个定时器。

解决的办法:1.setCount 接收一个函数来改变值。2. 可以使用 useReducer 来规避 useEffect 里面引用状态变量

```jsx
function App() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    let timer = setInterval(() => {
      setCount(count + 1);
    }, 1000);
    return () => {
      timer && clearInterval(timer);
    };
  }, []);
  return <div>{count}</div>;
}
```
