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

这段 React 函数组件代码存在一个经典的闭包陷阱问题，会导致 count 永远停留在初始值 0，组件每秒都只渲染 1
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
