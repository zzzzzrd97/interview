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


### elementUI怎么做到组件按需加载
### vue3.0特性了解
* 监测机制的改变
* 模板
* 对象式的组件声明方式
* 其它方面的更改