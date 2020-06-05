* 截图工具 snipaste

## v-show和v-if
* v-show控制的是display属性
* v-if 是直接将节点删除
> 如果节点需要频繁的显示隐藏，使用v-show更好
## v-for中的key属性
> 虚拟dom的因素
## 可以做到响应式的方法
> 可以改变原数组的方法
* push()
* pop()     删除数组最后一个元素
* shift()   删除数组第一个元素
* unshift() 数组最前边添加元素
* splice()
* sort()
* reverse()
* Vue.set(obj,index,value)
> 通过索引值修改数组中的元素不会引起界面上的刷新？
## v-model
> v-bind 绑定一个属性  
> v-on 绑定事件,通过事件对象的值改变被绑定属性的值
```vue
<template>
    <input type="text" v-model="message">
    <input type="text" v-bind:value="message" v-on:input="message=$event.target.value" >
</template>
```
### v-model修饰符的使用
* lazy
    * v-model.lazy
    > 可以让输入框在失去焦点/敲击回车的时候再进行双向绑定
* number
    * v-model.number  
    > 将字符串转化为数字
* trim
    * v-model.trim
    > 输入首尾空格过滤


## 为什么组件中的data必须是一个function
为了避免多个组件使用了同一组数据
组成一个function,使得每个组件建立了一个自己的空间,每个空间之间的数据互不影响,避免造成了数据污染
# 父子组件
## 组件内部无法访问Vue实例中的数据
## 数据传递
### 父传子
### 通过props向子组件传递数据
> 在子组件中,若接收的数据有默认值且数据类型是数组/对象的话,那么默认值必须是一个函数返回的内容   
> default:function(){return []}
```vue
// 父
<template>
    <div>
        <template-child :sendName="name"></template-child>
    </div>
</template>
<script >
    export default ({
        data(){
            return{
                name:'123'
            }
        }
    })
</script>
// 子
<template>
    
</template>
<script >
    export default ({
        props:{
            sendName:{
                type:String,    // 类型
                default:'',     // 默认值
                require:true,    // 如果为true,那么该值是必传的
                validator:function(value){ // 自定义验证
                    
                } 
            }
        },
        data(){
            return{}
        }
    })
</script>

```
### 子传父
### 通过自定义事件$emit
通过自组建中的方法出发$emit来发射事件,然后在模板中绑定被发射的事件,最后在父组件中接收
## 直接访问
### 父访问子
* $children
    * 返回的是数组类型(不常用),包含该组件中所有的子组件
* $refs
    * 返回的是对象类型(常用),默认是一个空的对象
### 子访问父
* $parent
    * 返回的是对象类型(不常用),只有当前子组件的父组件
### 访问根组件
* $root
    * 返回的是对象类型,只有当前的Vue实例
# solt插槽
> 使组建更具有扩展性
* 以导航栏为例:如何封装？
    * 抽取共性,保留不同
## 作用域插槽
> 父组件替换插槽中的标签,但是内容由子组件提供


    