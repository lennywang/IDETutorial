### React SetState的回调函数

#### setState()的参数

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

#### 异步更新的setState

```jsx
keyUp = (e) => {
        this.setState({
            name: e.target.value
        }, () => console.log(1, this.state.name));
}
```

> 参考网址：https://blog.csdn.net/juzipchy/article/details/73425070



###  React 生命周期

React 生命周期分为三种状态 1. 初始化 2.更新 3.销毁

![React生命周期](https://github.com/lennywang/Img/raw/master/lifecycle.jpg)

componentDidMount

shouldComponentUpdate

componentDidUpdate

componentWillUnmount

>  参考网址：https://www.cnblogs.com/qiaojie/p/6135180.html



### React创建组件的三种方式及其区别

1. 函数式定义的无状态组件
2. es5原生方式React.createClass定义的组件
3. es6形式的extends React.Component定义的组件

> 参考网址：https://www.cnblogs.com/wonyun/p/5930333.html

React 中import 的用法 

import React,{Component} from 'react';

导入‘react’文件里export的一个默认的组件，将其命名为React以及Component这个非默认组件

> 参考网址：https://blog.csdn.net/naxieren1992/article/details/79582484

### 受控组件和非受控组件

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













