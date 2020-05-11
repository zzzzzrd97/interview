# SPA框架
## 为什么选择使用框架而不是原生[参考](https://juejin.im/post/5d5f44dae51d4561df7805b4)
* 组件化
* 天然分层 代码解耦
* 生态链完整
* 开发效率
## 虚拟 DOM 的优缺点
* 虚拟DOM
* 优点
    * 保证性能下限：通过diff，找出最小差异，然后批量进行patch
    * 无需手动操作DOM：虚拟DOM的diff和parch都是在一次更新中自动进行的
    * 跨平台：虚拟DOM本质上是javascript对象，而DOM与平台强相关
* 缺点
    * 无法进行极致性优化：在一些性能要求极高的应用中虚拟DOM无法进行针对性的极致优化,
## 虚拟 DOM 实现原理
## 什么是 MVVM
> 由数据驱动，实现数据的双向绑定
* Model 数据模型
* View UI组件
* ViewModel 同步View 和 Model的对象
## 说说你对 SPA 单页面的理解，它的优缺点分别是什么
> 就是在 Web 页面初始化时加载所有的 HTML、JavaScript 和 CSS，页面的内容的变化，靠动态创建dom
* 优点
    * 用户体验好、快，内容的改变不需要重新加载整个页面，避免了不必要的跳转和重复渲染；
    * 基于上面一点，SPA 对服务器的压力小；
    * 前后端职责分离，架构清晰，前端进行交互逻辑，后端负责数据处理；
* 缺点
    * 初次加载耗时多，为实现单页 Web 应用功能及显示效果，需要在加载页面的时候将 JavaScript、CSS 统一加载，部分页面按需加载；
    * 前进后退路由管理，由于单页应用在一个页面中显示所有的内容，所以不能使用浏览器的前进后退功能，所有的页面切换需要自己建立堆栈管理
    * SEO 难度较大，由于所有的内容都在一个页面中动态替换显示，所以在 SEO 上其有着天然的弱势

## VUE
[面试题](https://juejin.im/post/5d59f2a451882549be53b170)
### 导航守卫
[官方文档](https://router.vuejs.org/zh/guide/advanced/navigation-guards.html)
* 全局钩子
* 路由独享钩子
* 组件内钩子
### 生命周期
#### Vue 的父组件和子组件生命周期钩子函数执行顺序
* 加载渲染过程
    * 父 beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created -> 子 beforeMount -> 子 mounted -> 父 mounted
* 子组件更新过程
    * 父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 update
* 父组件更新过程
    * 父 beforeUpdate -> 父 updated
* 销毁过程
    * 父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed
#### 在哪个生命周期内调用异步请求
> 一般来说，created、mounted中都可以请求，但大部分会在created中发送请求.
* 在created中调用异步请求有两个优点
    * 能更快获取到服务端的数据，减少页面的loading时间
    * 放在create中有助于一致性，因为ssr不支持 beforeMount 和 mounted 函数
#### 在什么阶段才能访问操作DOM？
> 在mounted中可以访问dom  
> mounted函数被调用前，Vue已经将编译好的模板挂载到页面上

#### 父组件可以监听到子组件的生命周期吗
* 手动$emit触发父组件的事件
```vue
<template>
<div>
    <!--parent-->
    <Child @mounted="doSomething"></Child>
</div>
</template>

<script >
// Child.vue
export default({
    mounted(){
        this.$emit("mounted")
    }
})
   
</script>
```
* 通过@hook
> 不仅可以监听mounted，其他的生命周期都可以监听
```text
//  Parent.vue
<Child @hook:mounted="doSomething" ></Child>

doSomething() {
   console.log('父组件监听到 mounted 钩子函数 ...');
},

//  Child.vue
mounted(){
   console.log('子组件触发 mounted 钩子函数 ...');
},    
// 以上输出顺序为：
// 子组件触发 mounted 钩子函数
// 父组件监听到 mounted 钩子函数
```

### 路由
#### vue-router实现
> 其实是基于HTML5的history API、window.onpopstate、window.onhashchange上做的封装，通过一定的规则映射到对应的方法上，同时监听变化，从而实现单页面路由
#### vue-router 路由模式有几种
> 实际上存在三种
* Hash      使用url的hash值作为路由，支持所有的浏览器
* History   
* Abstract  支持所有js运行模式，如果发现没有浏览器的API，路由会自动强进入这个模式
##### Vue中默认的是hash模式，URL中带有#
可以用代码修改成history模式
```javascript
import Vue from 'vue'
import Router from 'vue-router'
import Main from "@/components/Main"
Vue.use(Router);
export default new Router({
    mode:"history",
    routes:[
        {
            path:"/",
            component:Main
        }
    ]
})
```
#### vue-router 中常用的 hash 和 history 路由模式实现原理

### 组件
#### 谈谈你对 keep-alive 的了解
#### 组件中 data 为什么是一个函数
#### computed 和 watch 的区别和运用的场景
#### v-if和v-show的共同点和区别
#### VUE组件怎么传值/组件之间如何通信
#### Vue 中的 key 有什么作用

### Vuex
> 状态管理工具，所定义的内容，可以在整个Vue的组件内使用，可以理解为一个小型的数据库
#### Vuex成员列表
* state 		存放状态
* getters 		加工state成员给外界
* mutations		state成员操作
* actions 		异步操作
* modules		模块化状态管理

#### 详解成员
* state
	* 以对象的形式存储的数据
	* 使用方式：this.$store.store.name
	* 辅助函数：mapState
* getters
	* 相当于vue组件中的computed；可以借助state的值做一些操作以返回一些新的数据，但无法更改state中的数据
	* 使用方式：this.$store.getters.name
	* 辅助函数：mapGetters
```javascript
import { mapGetters } from 'vuex'
export default {
	computed: {
		// 使用对象展开运算符将 getter 混入 computed 对象中
		...mapGetters([
			'doneTodosCount',
			'anotherGetter',
		])M
		// 重命名
		...mapGetters({
			// 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
			doneCount: 'doneTodosCount'
		})
	}
}
```
* mutations
	* 相当于vue组件中的methods；可以对state中的数据做操作以达到更改state中的数据
	* 通常情况下使用常量代替utation的事件类型



### 原理性
#### v-model 的原理
#### 怎样理解 Vue 的单向数据流
#### VUE响应式的原理
#### 双向绑定的原理
* [参考1](https://juejin.im/post/5acd0c8a6fb9a028da7cdfaf)
* [参考2](https://juejin.im/post/5acc17cb51882555745a03f8)
#### 怎么实现对象和数组的监听

### 具体操作
#### 直接给一个数组项赋值，Vue 能检测到变化吗
#### VUE中数组如何实现响应式
#### 怎么用 vm.$set() 解决对象新增属性不能响应的问题 

### 优化
#### 对 Vue 项目进行哪些优化

### SSR
#### 说说 Vue SSR
> 服务端渲染，可以优化SEO抓取，提升首页的加载速度

### elementUI怎么做到组件按需加载
### vue3.0特性了解
* 监测机制的改变
* 模板
* 对象式的组件声明方式
* 其它方面的更改

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
# Vue和React的对比/共通点
### Vue和React的区别
#### 相似之处
* 支持组件化
* 数据驱动试图
#### 不同之处  
##### 监听数据变化的实现原理
* Vue : 通过getter/setter和其他函数时间数据劫持
* React 通过比较引用的方式(diff)
##### 数据流不同
* Vue : 双向绑定
* React : 单向数据流
##### 组合不同功能的方式
* Vue mixins
* ReactHoC(高阶组件)
##### 组件通信
> React 本身并不支持自定义事件，而Vue中子组件向父组件传递消息有两种方式：事件和回调函数，但Vue更倾向于使用事件。在React中我们都是使用回调函数的，这可能是他们二者最大的区别
* Vue
    * 父组件通过props向子组件传递数据或者回掉(一般只传数据)
    * 子组件通过事件向父组件发送消息
    * 新增的provide/inject来实现父组件向子组件注入数据，可以跨越多个层级
* React
    * 父组件通过props可以向子组件传递数据或者回调
    * 可以通过 context 进行跨层级的通信
##### 模板渲染方式的不同
* Vue
    * 通过一种拓展的HTML语法进行渲染
    * 在和组件JS代码分离的单独的模板中，通过指令来实现的
* React 
    * React是通过JSX渲染模板
    * React是在组件JS代码中，通过原生JS实现模板中的常见语法，比如插值，条件，循环等，都是通过JS语法实现的
##### 渲染过程不同
* Vue
    * Vue可以更快地计算出Virtual DOM的差异，这是由于它在渲染过程中，会跟踪每一个组件的依赖关系，不需要重新渲染整个组件树
* React
    * 在应用的状态被改变时，全部子组件都会重新渲染。通过shouldComponentUpdate这个生命周期方法可以进行控制，但Vue将此视为默认的优化。
##### 框架本质不同
* Vue
    * Vue本质是MVVM框架，由MVC发展而来
* React 
    * React是前端组件化框架，由后端组件化发展而来
## vue/react框架里如果有错误怎么上报
### Vue
> vue 中 errorCaptured 只能捕获自己子组件的错误，如果子组件出错了，父组件没有处
  理，就会一级一级往上， 如果 app组件还没有处理，根组件也没有处理，就会报错。
  但是不可能在每一个组件里面都使用 errorCaptured 捕获， 而且一个 app 里面可能有
  很多需要错误捕获的地方， 所以建议在 app.vue 中 或者 根组件里面处理
#### 处理方式
* 显示错误页面(配置一个错误路由)
* 收集错误(错误信息，账号信息，手机设备信息等)，提交给后台
``` vue.js
    errorCaptured(error) {
        console.log('root 出错了');
        console.log(error.message);
        // 我们最多只能拿到这个, 如果是在控制台就可以用这样
        // 手机上可以用 android，ios会更清晰
        console.log(window.navigator.userAgent); 
        return false; // 这样就不会在控制台打印了
    }
```
### React
> 只会在最外层处理 react 中的错误
  react 中 index.js 中 render 是处理不了错误的，需要在 App.js 中处理
#### 处理方式
1. getDerivedStateFromError（静态方法）
```react.js
static getDerivedStateFromError(error) { 
    // 1.显示错误提示界面
    // 2.收集错误信息，提交给后台
    return {
        isError: true;
    }
	// 这个 return 的值也会跟 state 进行合并
}
```
2. componentDidCatch（实例方法）
```react.js
componentDidCatch(error) {
    // 1.显示错误提示界面
    // 2.收集错误信息，提交给后台
    this.setState({
        isError: true
    })
}
```