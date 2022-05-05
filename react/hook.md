### 前言

在 react16.8 的版本中引入了 hook，可以说直接起飞了。

hook 是在函数组件中勾入状态管理以及其他特性的媒介。

### 解决的问题

- 逻辑复用
- 简化组件复杂度（逻辑拆分）
- 避开 class 中 this 等难以理解的概念

### 规则

- 只能在函数组件中使用
- 只能在函数最外层调用 Hook。不要在循环、条件判断或者子函数中调用。
- 自定义 hook 以 use 开头

### 内置 hooks 分类

2x + 1 = y 等式，自变量 x 变化可以导致 因变量 y 的变化。hooks 可以类比 x 数据改变引起视图的改变

#### 自变量 hooks

- useState
- useReducer
- useContext

#### 因变量 hooks

- useMemo
- useCallback
- useEffect

#### 特殊的 useRef

接下来我们会分别介绍这些 hooks 的用法与注意点
