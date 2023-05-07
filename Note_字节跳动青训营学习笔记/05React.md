[ 前端与 React | 青训营笔记]

# React简介

> 用于构建用户界面的Javascript库

特点：声明式 组件化 跨平台编写

解决影响Web性能的两大难题

- 等接资源加载时间
- 大部分情况下浏览器单线程执行

几大场景 ：

1.用户突然没网了
----------------

 使用离线缓存、服务端渲染、优雅降级等技术来保证用户体验。

2.JS执行与UI绘制无法同时进行
----------------------------

 将一个重任务，拆分成多个分轻任务

 React的调度器 协调器 渲染器

- React中的调度器负责协调任务的优先级，以便在多个任务之间分配CPU时间，确保高优先级任务在低优先级任务之前完成。调度器的核心思想是时间切片，即将一个大的任务分割成多个小的任务，每次只执行一小部分，以便让浏览器有时间响应用户的交互事件。
- 协调器则负责处理React元素的更新，比较新旧两个元素的差异，生成需要更新的DOM节点，并将更新的任务提交给渲染器。
- 渲染器则负责将React元素渲染成浏览器可识别的DOM节点，更新DOM节点的属性和内容，以及处理用户交互事件等任务。React支持多个渲染器，比如ReactDOM用于在浏览器中渲染React元素，React Native用于在移动端渲染原生组件。

总结 ：React可以快速响应，复用性强，声明式编程，跨平台的；但是需要配套学习状态管理，路由工具

```js
import 
```

# React 开发Web应用组件

1.数据
------

 使用React状态（state）来管理组件内部的数据状态。

2.通信
------

  props 父子组件
  context redux组件信息共享
  props和状态适用于组件之间的数据通信，而Context和Redux适用于跨组件的数据共享和状态管理。使用不同的通信方式可以根据具体的场景来选择，以达到最佳的性能和可维护性。

3.UI
----

  数据决定视图
  通过Ref获取到DOM
  组件的渲染结果应该由组件的数据状态决定
  尽量避免直接操作DOM元素，而是应该通过修改组件的数据状态来实现组件的交互和动态效果。

4.性能
------

 React.memo()、useCallback()、useMemo()等，来提高应用的性能。

Class 组件
可以管理自己的状态（state）和属性（props），并且可以使用组件的生命周期方法来处理组件的初始化、更新和销毁等过程

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/af5d4d2e6685437e85ee289580dd6d60~tplv-k3u1fbpfcp-watermark.image?)

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/33f605dfd81c435a81806caad89e3b5b~tplv-k3u1fbpfcp-watermark.image?)

### Class组件

Class组件的简单代码
可以显示一个计数器和一个按钮，每次点击按钮后，计数器的值会加1：

```js
import React from 'react';
class Counter extends React.Component {
    constructor(props) {
        super(props);
        this.state = { count: 0 };
    }
    handleIncrement() {
        this.setState(prevState => ({
            count: prevState.count + 1
        }));
    } render() { return (<div> <h1>Count: {this.state.count}</h1> <button onClick={() => this.handleIncrement()}>Increment</button> </div>); }
} export default Counter;

```

### 函数式组件

特点 没有生命周期  借助Hook  return JSX
---------------------------------------

React函数式组件使用Hook来管理状态和副作用，通过return语句返回JSX元素，不需要像class组件那样定义render()方法和生命周期方法

在函数式组件中，不能使用this关键字来访问组件的状态和属性，而是应该通过函数的参数来访问。另外，函数式组件的代码比class组件的代码更简洁，但是它缺少了状态管理的功能，只能通过props来获取和更新数据。

```js

import React from 'react';

function Greeting(props) {
  const currentTime = new Date().toLocaleTimeString();
  return (
    <div>
      <h1>Hello, {props.name}!</h1>
      <p>The current time is {currentTime}.</p>
    </div>
  );
}

export default Greeting;
```

关于组件
--------

函数式 相较于 Class的优点
-------------------------

 相较于class组件，函数式组件不需要定义类、构造函数和生命周期方法等，减少了代码量和学习成本。支持自定义hook，逻辑复用方便

组件和hook的关系
----------------

  将UI拆分成多个独立的单元，这些单元组合可以构成多个视图展示。组件是React应用的基本构建块，用于封装UI元素和逻辑。组件可以是class组件或函数式组件，它们都可以使用props属性来接受数据和事件处理程序，以及使用state状态来管理内部状态。Hook贴近组件内运行的各种概念，用于在函数式组件中使用状态和其他特性，例如生命周期方法、访问DOM元素、订阅事件等

# [ 前端与 React | 青训营笔记] 2.0

> 为什么不能用windows对象？
>
> react hooks 给状态管理库的设计带来了哪些新思路？

1. 不能使用 `window` 对象的原因是因为在服务器端渲染时，`window` 对象是不存在的，只有在浏览器环境下才有。因此，在 React 组件中使用 `window` 对象可能会导致代码在服务器端渲染时出错。
2. React Hooks 引入了函数式组件中的状态管理，使得组件状态的管理更加简洁和灵活。同时，它也鼓励开发者将组件拆分为更小的、更易于管理的组件，从而提高代码的可读性和可维护性。此外，React Hooks 还提供了一些其他的钩子函数，如 `useEffect` 和 `useContext` 等，使得开发者能够更方便地处理组件的副作用和上下文信息。

## 状态管理

状态管理工具的本质：管理共享内存中的状态

React Vue Angular 对比
----------------------

 Vue 和 Angular 双向数据绑定，计算属性等，数据是响应式的，控制视图刷新，拥有计算属性等，相比下Vue 和 Angular 使用状态管理的场景减少。
 React 的状态管理工具通常更加灵活和扩展性更强

 React Local State ：组件级别的局部状态

```js
import React, { useState } from 'react';

function HelloWorld() {
  const [message, setMessage] = useState('Hello, World!');

  function handleClick() {
    setMessage('Hello, React!');
  }

  return (
    <div>
      <h1>{message}</h1>
      <button onClick={handleClick}>Change Message</button>
    </div>
  );
}

export default HelloWorld;
```

问题来了，React 的 数据流是自上向下的，大部份情况下Local State 就能满足
