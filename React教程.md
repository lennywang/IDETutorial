需要做的事儿

1、点赞案例

2、评论案例





## 第一阶段

### 1.1  React 简介
React.js 是一个UI 库。

注: 1、它不是一个框架

​       2、在实际的项目当中，需要结合其它的库，例如 Redux、React-router 等来协助提供完整的解决方案。

 React.js 提供了一种非常高效的方式做到了数据和组件显示形态之间的同步。

### 1.2 JSX

JSX 其实就是 JavaScript 对象。

react-dom 负责把 JSX 变成 DOM 元素，并且渲染到页面上。

JSX 到页面的过程

![jsx到页面过程](https://github.com/lennywang/Img/raw/master/reactdom.png)



### 1.3 render方法

必须要用一个外层的 JSX 元素把所有内容包裹起来。

```jsx
render () {
  return (
    <div>
      <div>第一个</div>
      <div>第二个</div>
    </div>
  )
}
```

表达式插入

表达式用 `{}` 包裹，`{}` 内可以放任何 JavaScript 的代码，包括变量、表达式计算、函数执行等等。

```jsx
const word= ' is good ! '
const className = 'header'
render () {
  return (
    <div className={className}>
      <h1>React 小书 {word}</h1>
    </div>
  )
}
```

特殊属性

| 属性名           | 不合法用法                          | 原因                      | 正确用法                 |
| ------------- | ------------------------------ | ----------------------- | -------------------- |
| class         | <div class=“xxx”>              | class 是 JavaScript 的关键字 | className            |
| for           | <label for='male'>Male</label> | for 是 JavaScript 的关键字   | htmlFor              |
| style 、data-* |                                |                         | 像普通的 HTML 属性那样直接添加上去 |

条件返回

```jsx
render () {
  const isGoodWord = true
  return (
    <div>
      <h1>
        React 小书
        {isGoodWord
          ? <strong> is good</strong>
          : null
        }
      </h1>
    </div>
  )
}
```

表达式插入里面返回 `null` ，那么 React.js 会什么都不显示，相当于忽略了该表达式。

JSX元素变量

JSX 元素其实可以像 JavaScript 对象那样自由地赋值给变量，或者作为函数参数传递、或者作为函数的返回值。

JSX 元素变量

```jsx
//变量
render () {
  const isGoodWord = true
  const goodWord = <strong> is good</strong>
  const badWord = <span> is not good</span>
  return (
    <div>
      <h1>
        React 小书
        {isGoodWord ? goodWord : badWord}
      </h1>
    </div>
  )
}
//函数
renderGoodWord (goodWord, badWord) {
  const isGoodWord = true
  return isGoodWord ? goodWord : badWord
}

render () {
  return (
    <div>
      <h1>
        React 小书
        {this.renderGoodWord(
          <strong> is good</strong>,
          <span> is not good</span>
        )}
      </h1>
    </div>
  )
}
```



###  1.4事件监听 

 on* 的事件监听只能用在普通的 HTML 的标签上，而不能用在组件标签上

```jsx
class Title extends Component {
  handleClickOnTitle () {
    console.log('Click on title.')
  }

  render () {
    return (
      <h1 onClick={this.handleClickOnTitle}>React 小书</h1>
    )
  }
}
```

**event 对象**

事件监听函数会被自动传入一个 `event` 对象，这个对象和普通的浏览器 `event` 对象所包含的方法和属性都基本一致。

常用属性：e.target.innerHTML

常用方法：event.stopPropagation、event.preventDefault

事件中的this

如果你想在事件函数当中使用当前的实例，你需要手动地将实例方法 `bind` 到当前实例上再传入给 React.js

```jsx
class Title extends Component {
  handleClickOnTitle (e) {
    console.log(this)
  }

  render () {
    return (
      <h1 onClick={this.handleClickOnTitle.bind(this)}>React 小书</h1>
    )
  }
}
```



### 1.5 React SetState的回调函数
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

### 1.6 配置组件的props

一个组件的显示形态、行为都可以用 props 来控制

```jsx
class Index extends Component {
  render () {
    return (
      <div>
        <LikeButton wordings={{likedText: '已赞', unlikedText: '赞'}} />
      </div>
    )
  }
}
```



```jsx
class Index extends Component {
  render () {
    return (
      <div>
        <LikeButton
          wordings={{likedText: '已赞', unlikedText: '赞'}}
          onClick={() => console.log('Click on like button!')}/>
      </div>
    )
  }
}
```

**默认配置 defaultProps**

给组件添加类属性 `defaultProps` 来配置默认参数

```jsx
  static defaultProps = {
    likedText: '取消',
    unlikedText: '点赞'
  }
```

**props 不可变**

`props` 一旦传入，你就不可以在组件内部对它进行修改。

props 错误的修改方式

```jsx
handleClickOnLikeButton () {
    this.props.likedText = '取消'
    this.setState({
      isLiked: !this.state.isLiked
    })
  }
```

可以通过父组件主动重新渲染的方式来传入新的 `props`

### 1.7 state 与 props

state 是让组件控制自己的状态，props 是让外部对组件自己进行配置

**尽量写无状态组件**

尽量少地用 `state`，尽量多地用 `props` 

React 在 0.14 版本引入了函数式组件——一种定义不能使用 `state` 组件

```jsx
 const HelloWorld = (props) => {
  const sayHi = (event) => alert('Hello World')
  return (
    <div onClick={sayHi}>Hello World</div>
  )
} 
```



### 1.8 渲染列表数据

```jsx
{users.map((user) => <User user={user} />)}
```

对于用表达式套数组罗列到页面上的元素，都要为每个元素加上 key 属性，这个 key 必须是每个元素唯一的标识。一般来说，`key` 的值是后台数据返回的 `id`，因为后台的 `id` 都是唯一的。



### 1.3 React创建组件的方式及区别

1. 函数式定义的无状态组件
2. es5原生方式React.createClass定义的组件
3. es6形式的extends React.Component定义的组件

> 参考网址：https://www.cnblogs.com/wonyun/p/5930333.html

### 1.4  组件分类

####  1.4.1 受控组件和非受控组件

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

#### 1.4.2 无状态组件与有状态组件

没有 `state` 的组件叫无状态组件（stateless component）

有 state 的组件叫做有状态组件（stateful component）

因为状态会带来管理的复杂性，我们尽量多地写无状态组件，尽量少地写有状态的组件。这样会降低代码维护的难度，也会在一定程度上增强组件的可复用性。



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

### 2.2 ref 和 React.js 中的DOM操作

ref 属性：获取已经挂载的元素的 DOM 节点

```jsx
class AutoFocusInput extends Component {
  componentDidMount () {
    this.input.focus()
  }

  render () {
    return (
      <input ref={(input) => this.input = input} />
    )
  }
}

ReactDOM.render(
  <AutoFocusInput />,
  document.getElementById('root')
)
```

可以给组件标签也加上 ref

```jsx
<Clock ref={(clock) => this.clock = clock} />
```



### 2.3 props.children和容器类组件

使用自定义组件的时候，可以在其中嵌套 JSX 结构。嵌套的结构在组件内部都可以通过 `props.children` 获取到，这种组件编写方式在编写容器类型的组件当中非常有用。



```jsx
ReactDOM.render(
  <Card>
    <h2>React.js 小书</h2>
    <div>开源、免费、专业、简单</div>
    订阅：<input />
  </Card>,
  document.getElementById('root')
)
```

在组件内部通过 `props.children` 获取嵌套在组件中的 JSX 结构

```jsx
class Card extends Component {
  render () {
    return (
      <div className='card'>
        <div className='card-content'>
          {this.props.children}
        </div>
      </div>
    )
  }
}
```

在组件内部把数组中的 JSX 元素安置在不同的地方

```jsx
class Layout extends Component {
  render () {
    return (
      <div className='two-cols-layout'>
        <div className='sidebar'>
          {this.props.children[0]}
        </div>
        <div className='main'>
          {this.props.children[1]}
        </div>
      </div>
    )
  }
}
```



### 2.4 dangerouslySetHTML 和 style 属性 

**dangerouslySetHTML**

出于安全考虑的原因（XSS 攻击），在 React.js 当中所有的表达式插入的内容都会被自动转义。React.js 提供了一个属性 `dangerouslySetInnerHTML` 来设置动态 HTML 结构的效果。

```jsx
render () {
    return (
      <div
        className='editor-wrapper'
        dangerouslySetInnerHTML={{__html: this.state.content}} />
    )
  }
```

`__html` 属性值就相当于元素的 `innerHTML`

**style**

React.js 中你需要把 CSS 属性变成一个对象再传给元素

CSS 属性中带 `-` 的元素都必须要去掉 `-` 换成驼峰命名，如 `font-size` 换成 `fontSize`，`text-align` 换成 `textAlign`。

```jsx
<h1 style={{fontSize: '12px', color: 'red'}}>React.js 小书</h1>
```

可以用 `props` 或者 `state`中的数据生成样式对象再传给元素，然后用 `setState` 就可以修改样式

```jsx
<h1 style={{fontSize: '12px', color: this.state.color}}>React.js 小书</h1>
setState({color: 'blue'})    {/* 修改元素的颜色成蓝色 */}
```

### 2.5 PropTypes 和组件参数验证   

```jsx
npm install --save prop-types

import PropTypes from 'prop-types'

//设置组件参数类型
static propTypes = {
    comment: PropTypes.object
}

//设置组件参数必选
static propTypes = {
    comment: PropTypes.object.isRequired
}

//设置组件参数默认值
static defaultProps = {
    comments: []
}
```

`PropTypes` 数据类型

```jsx
PropTypes.array
PropTypes.bool
PropTypes.func
PropTypes.number
PropTypes.object
PropTypes.string
PropTypes.node
PropTypes.element
```

PropTypes 给组件的参数做类型限制，可以在帮助我们迅速定位错误，这在构建大型应用程序的时候特别有用；另外，给组件加上 propTypes，也让组件的开发、使用更加规范清晰。

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



高阶组件的形式

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



### 3.3 context

context 打破了组件和组件之间通过 props 传递数据的规范，极大地增强了组件之间的耦合性。

context 里面的数据能被随意接触就能被随意修改，每个组件都能够改 context 里面的内容会导致程序的运行不可预料。

在Index的 context 里面放一个 themeColor

```jsx
class Index extends Component {
  static childContextTypes = {
    themeColor: PropTypes.string
  }

  constructor () {
    super()
    this.state = { themeColor: 'red' }
  }

  getChildContext () {
    return { themeColor: this.state.themeColor }
  }

  render () {
    return (
      <div>
        <Header />
        <Main />
      </div>
    )
  }
}
```

子组件怎么获取这个状态

```jsx
class Title extends Component {
  static contextTypes = {
    themeColor: PropTypes.string
  }

  render () {
    return (
      <h1 style={{ color: this.context.themeColor }}>React.js 小书标题</h1>
    )
  }
}
```

组件树

![组件树](https://github.com/lennywang/Img/raw/master/componenttree.png)



### 3.4 Redux

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

> 参考网址：https://blog.csdn.net/juzipchy/article/details/73295078



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





