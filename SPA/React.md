## React
[面试题](https://juejin.im/post/5d5f44dae51d4561df7805b4)
[面试题](https://juejin.im/post/5c989ea76fb9a070ad504cd8)
### React 项目用过什么脚手架
* create-react-app
### 生命周期
[参考](https://zhuanlan.zhihu.com/p/38030418)
#### React生命周期有哪些
* 组件初始化(initialization)阶段
* 组件的挂载(Mounting)阶段
    * componentWillMount
    * render
    * componentDidMount
* 组件的更新(update)阶段
    * componentWillReceiveProps(nextProps)
    * shouldComponentUpdate(nextProps, nextState)
    * componentWillUpdate(nextProps, nextState)
    * render
    * componentDidUpdate(prevProps, prevState)
* 卸载阶段
    * componentWillUnmount
#### react 性能优化是哪个周期函数
> shouldComponentUpdate
#### React最新的生命周期是怎样的
#### React的请求应该放在哪个生命周期中
> componentDidmount
### 组件
#### React 中有三种构建组件的方式
> React.createClass()、ES6 class 和无状态函数。
#### React 中 keys 的作用是什么
#### React的setState是同步还是异步
#### React 中 refs 的作用
#### 组件传值/通信
#### 虚拟DOM实现原理
#### 为什么虚拟DOM会提高性能
#### 展示组件(Presentational component)和容器组件(Container component)之间有何不同
#### 类组件(Class component)和函数式组件(Functional component)之间有何不同
#### (组件的)状态(state)和属性(props)之间有何不同
#### 何为受控组件(controlled component)
#### 何为高阶组件(higher order component)
#### 为什么建议传递给 setState 的参数是一个 callback 而不是一个对象
#### 除了在构造函数中绑定 this，还有其它方式吗
#### (在构造函数中)调用 super(props) 的目的是什么
#### 应该在 React 组件的何处发起 Ajax 请求
#### 描述事件在 React 中的处理方式。
#### createElement 和 cloneElement 有什么区别？
### React Hooks
#### 了解哪些 React Hooks的作用和基本知识
### Redux
#### 优缺点
#### redux的工作流程
#### react-redux是如何工作的
#### redux与mobx的区别
#### redux中如何进行异步操作
#### redux异步中间件之间的优劣
### Redux 和 mobx
### 性能优化
#### React有哪些优化性能是手段
### 算法
#### react diff 原理
#### mixin、hoc、render props、react-hooks的优劣如何
#### 你是如何理解fiber的
#### 你对 Time Slice的理解