## 第一阶段

### 1.1 React SetState的回调函数

**setState()的参数**

1、this.setState(obj)

```jsx
this.setState({count:1});
```

2、this.setState(callbackFunc)

第一个参数是state的前一个状态，第二个参数是属性对象props

```jsx
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
```

3、this.setState(obj , callbackFunc)

 第一个参数是要改变的state对象

 第二个参数是 state 导致的页面变化完成后的回调，等价于componentDidUpdate

> 参考网址：https://blog.csdn.net/juzipchy/article/details/75453860

**异步更新的setState**

```jsx
keyUp = (e) => {
        this.setState({
            name: e.target.value
        }, () => console.log(1, this.state.name));
}
```

> 参考网址：https://blog.csdn.net/juzipchy/article/details/73425070

### 1.2 React创建组件的方式及区别

1. 函数式定义的无状态组件
2. es5原生方式React.createClass定义的组件
3. es6形式的extends React.Component定义的组件

> 参考网址：https://www.cnblogs.com/wonyun/p/5930333.html

### 1.3 受控组件和非受控组件

受控组件就形式上来说，受控组件就是为某个form表单组件添加value属性

```
render: function() {
    return <input type="text" value="Hello!" />;
}
```

非受控组件表现形式上，react中没有添加value属性的表单组件元素就是非受控组件。

```
<input type="text" />
```

> 参考网址：https://www.cnblogs.com/wonyun/p/6023363.html

## 第二阶段

### 2.1 React 生命周期

React 生命周期分为三种状态 1. 初始化 2.更新 3.销毁

![React生命周期](https://github.com/lennywang/Img/raw/master/lifecycle.jpg)

componentDidMount

shouldComponentUpdate

componentDidUpdate

componentWillUnmount

>  参考网址：https://www.cnblogs.com/qiaojie/p/6135180.html

React 中import 的用法 

import React,{Component} from 'react';

导入‘react’文件里export的一个默认的组件，将其命名为React以及Component这个非默认组件

> 参考网址：https://blog.csdn.net/naxieren1992/article/details/79582484

## 第三阶段

### 3.1 纯函数

**纯函数** 一个函数的返回结果只依赖于它的参数，并且在执行过程里面没有副作用，我们就把这个函数叫做纯函数。

**1、函数的返回结果只依赖于它的参数**

```
const a = 1
const foo = (b)=> a + b
foo(2) // => 3
```

foo函数不是一个纯函数，因为它返回的结果依赖于外部变量 a，我们在不知道 a 的值的情况下，并不能保证 foo(2) 的返回值是 3。

**2、函数执行过程里面没有副作用**

一个函数执行过程对产生了外部可观察的变化那么就说这个函数是有副作用的。

```
const a = 1
const foo = (obj, b)=> {
  obj.x = 2
  return obj.x + b
}
const counter = { x:1 }
foo(counter, 2) //=> 4
counter.x // => 2
```

 foo 内部加了一句 obj.x = 2，计算前 counter.x 是 1，但是计算以后 counter.x 是 2。foo 函数的执行对外部的 counter 产生了影响，它产生了副作用，因为它修改了外部传进来的对象，现在它是不纯的。



### 3.2 高阶组件

**概念和作用**

什么是高阶组件

高阶组件就是一个函数，传给它一个组件，它返回一个新的组件。



 高阶组件的作用

 用于代码复用，可以把组件之间可复用的代码、逻辑抽离到高阶组件当中。新的组件和传入的组件通过 props 传递信息。



```jsx
import React, { Component } from 'react'

export default (WrappedComponent) => {
  class NewComponent extends Component {
    // 可以做很多自定义逻辑
    render () {
      return <WrappedComponent />
    }
  }
  return NewComponent
}
```



### 3.3 Redux

**store**：store在这里代表的是数据模型，内部维护了一个state变量，用例描述应用的状态。store有两个核心方法，分别是getState、dispatch。前者用来获取store的状态（state），后者用来修改store的状态。

```jsx
// 创建store, 传入两个参数
// 参数1: reducer 用来修改state
// 参数2(可选): [], 默认的state值,如果不传, 则为undefined
var store = redux.createStore(reducer, []);


// 通过 store.getState() 可以获取当前store的状态(state)
// 默认的值是 createStore 传入的第二个参数
console.log('state is: ' + store.getState());  // state is:
```

// 通过 store.dispatch(action) 来达到修改 state 的目的 
// 注意: 在redux里,唯一能够修改state的方法,就是通过 store.dispatch(action) 
store.dispatch({type: ‘add_todo’, text: ‘读书’});

**action** ：对行为（如用户行为）的抽象，在redux里是一个普通的js对象。redux对action的约定比较弱，除了一点，action必须有一个type字段来标识这个行为的类型。所以，下面的都是合法的action

```jsx
{type:'add_todo', text:'读书'}
{type:'add_todo', text:'写作'}
{type:'add_todo', text:'睡觉', time:'晚上'}
```

**reducer** ：一个普通的函数，用来修改store的状态。传入两个参数 state、action。其中，state为当前的状态（可通过store.getState()获得），而action为当前触发的行为（通过store.dispatch(action)调用触发）。reducer(state, action) 返回的值，就是store最新的state值。

```jsx
// reducer方法, 传入的参数有两个
// state: 当前的state
// action: 当前触发的行为, {type: 'xx'}
// 返回值: 新的state
var reducer = function(state, action){
    switch (action.type) {
        case 'add_todo':
            return state.concat(action.text);
        default:
            return state;
    }
};
```

**调用关系**

```jsx
store.dispatch(action) --> reducer(state, action) --> final state
```

**redux使用套路** 

```jsx
// 定一个 reducer
function reducer (state, action) {
  /* 初始化 state 和 switch case */
}

// 生成 store
const store = createStore(reducer)

// 监听数据变化重新渲染页面
store.subscribe(() => renderApp(store.getState()))

// 首次渲染页面
renderApp(store.getState()) 

// 后面可以随意 dispatch 了，页面自动更新
store.dispatch(...)
```









