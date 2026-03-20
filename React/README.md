#### 请你谈一谈对React Fiber架构的理解

React Fiber 是 React 16 引入的一种新的渲染架构，在React16之前，在同一个上下文中React会收集所有setState放入更新队列中，随后进入render阶段，会基于旧的Virtual Dom树构建出一棵新的Virtual Dom树，并通过diff算法实行函数递归，标记出新旧两棵虚拟Dom树的不同之处，并在commit阶段统一更新到真实的Dom树上，这个过程是同步且不可中断的，如果组件树较大，会长时间占用主线程，导致用户的点击、输入等高优先级任务无法及时响应，从而出现卡顿。而在React16之后，引入了React Fiber架构，它将原本同步不可中断的递归更新，拆分成一个个可中断的任务单元（Fiber）。在 render 阶段，React 会逐步构建 Fiber 树并进行 diff，这个过程是可以被打断和调度的；而在 commit 阶段，才会一次性更新 DOM，从而保证 UI 一致性。

#### 请指出以下代码可能会出现什么问题，以及如何修复。

```javascript
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      setCount(count + 1);
    }, 1000);
  }, []);

  return <div>{count}</div>;
}
```

这段 React 函数组件代码存在一个经典的闭包陷阱问题，会导致 count 永远停留在初始值 0，组件每秒都只渲染 1<br>
使用函数式更新 setCount(prev => prev + 1)可以修复这个问题

#### 组件之间的状态同步
1. 父子组件之间如何实现状态同步
通过props传递状态和回调函数

2. 同级组件之间如何实现状态同步
将状态提升到最近的公共父组件，然后再通过 props 传递

3. 两个相距很远的组件如何实现状态同步
使用React Context API；使用全局状态管理(Redux，Mobx)

#### 如何理解React 18 中的 Concurrent Mode
Concurrent Mode 是 React 18 默认启用的一种内部渲染机制，可以让 React 的渲染任务变得可中断、并发执行，以提高页面在用户交互时的流畅度。

传统模式：React 渲染是同步的，不可中断。如果组件树很大、渲染耗时，整个页面会卡顿，不能及时响应用户操作。

并发模式：React 将渲染变成可中断的异步任务，可以“分片”执行。当用户有更高优先级的交互，如点击、输入时，React 可以暂停当前渲染任务，优先处理这些任务。

#### 讲一讲你对React的虚拟Dom和diff算法的理解

相比于使用document.querySelector的方式直接操作dom，React则是使用虚拟Dom的形式，虚拟Dom本质上是一个用JavaScript表示的对象，存储节点的描述信息，当状态发送改变时，React并不会直接更新真实的dom节点，而是先更新虚拟Dom，并生成一颗新的虚拟Dom树，通过diff算法比对新旧两棵虚拟Dom树，计算出最小的差异，并批量更新到真实的Dom树上，避免了频繁操作真实 DOM 带来的性能问题。

#### 谈谈你对React高阶组件的理解

React高阶组件HOC本质上是一个函数，它接收一个组件作为参数，并返回一个新的增强后的组件。

#### 讲讲你对useMemo、useCallback、React.memo()的理解

useMemo 是 React 的一个 Hook函数，用来缓存函数计算的结果，它的第二个参数是一个依赖数组，只有当数组中的状态发送改变时，才会重新计算函数的值，可以避免组件在每次渲染时都重复执行函数的性能开销。
useCallback 也是 React 的一个 Hook函数，用来缓存函数实例，避免在组件每次渲染时都创建一个新的函数。
React.memo() 是 React 提供的一个高阶组件HOC，它接受一个组件作为第一个参数，第二个参数则是一个自定义的比较函数，可以通过前后props是否发送变化来决定是否重新渲染传入的组件。

#### 谈一谈你对受控组件和非受控组件的理解

受控组件是指表单元素的值完全由 React 组件的 state 来控制，组件状态是数据的唯一来源，符合 React “单向数据流”设计理念；
非受控组件指表单元素自身维护状态，React 不直接控制表单元素的值，React 通过 ref 访问 DOM 节点来获取或设置表单的当前值。

#### 谈一谈类组件和函数式组件

类组件是React16之前的写法，而React16之后官方更加推荐使用函数式组件了，能够更好的和react hooks进行搭配，且不需要考虑this的问题。

#### React组件接受两个prop，要求其中一个prop变化时，组件不重新渲染，另一个prop变化时重新渲染

使用 React.memo + 自定义比较函数 <br>
```tsx
import React from 'react';

const MyComponent = (props) => {
  console.log('组件渲染了');
  return (
    <div>
      <p>a: {props.a}</p>
      <p>b: {props.b}</p>
    </div>
  );
};

const arePropsEqual = (prevProps, nextProps) => {
  return prevProps.b === nextProps.b;
};

const MemoizedMyComponent = React.memo(MyComponent, arePropsEqual);

// 父组件使用示例
const ParentComponent = () => {
  const [a, setA] = React.useState(0);
  const [b, setB] = React.useState(0);

  return (
    <div>
      <button onClick={() => setA(a + 1)}>修改 a（{a}）</button>
      <button onClick={() => setB(b + 1)}>修改 b（{b}）</button>
      <MemoizedMyComponent a={a} b={b} />
    </div>
  );
};

export default ParentComponent;
```

#### React中JSX.Element和React.FC之间的区别？

JSX.Element是一段jsx代码的类型，是函数式组件的返回值的类型；React.FC是函数式组件的类型。

#### React将虚拟Dom更新到真实Dom的时机？

在 React 中，虚拟 DOM 更新到真实 DOM 的时机，本质上发生在 commit 阶段。React 的更新流程其实可以分成 两个阶段：Render 阶段、Commit 阶段、只有在 Commit 阶段，React 才会真正操作真实 DOM

#### React渲染列表时，加key和不加key的利弊？

在 React 中，key 的作用核心是：帮助 React 在 diff 过程中识别哪些元素是“同一个”节点。这直接影响 性能、DOM 复用、组件状态是否保留。<br>
旧：A B C，新：B C D，如果不加key，React会把A → B，B → C，C → D，结果会有3次Dom的更新，如果加了key，React 只需要删除A，新增D，结果只有2次Dom操作，可以复用Dom且保留组件的state，性能更优

#### 有哪些办法可以拿到React State的最新状态？

1、 setState 的函数式更新
2、useEffect 依赖数组
```javascript
const [count, setCount] = useState(0)

useEffect(() => {
  console.log(count) // 每次 count 变化都能拿到最新值
}, [count])
```
3、useReducer
```javascript
// 第一步：定义 reducer 函数
// state = 当前状态，action = 你发出的指令
function reducer(state, action) {
  switch (action.type) {
    case 'increment': return state + 1
    case 'decrement': return state - 1
    case 'reset':     return 0
  }
}

// 第二步：使用
const [count, dispatch] = useReducer(reducer, 0)
//                                            ↑ 初始值

// 第三步：通过 dispatch 发指令，而不是直接 setState
<button onClick={() => dispatch({ type: 'increment' })}>+</button>
<button onClick={() => dispatch({ type: 'decrement' })}>-</button>
<button onClick={() => dispatch({ type: 'reset' })}>重置</button>
```







