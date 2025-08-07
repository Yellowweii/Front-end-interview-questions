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