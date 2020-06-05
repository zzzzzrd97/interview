# 前端规范化
## 前端模块化开发
* 常见模块化规范
    * CommonJS
    * AMD
    * CMD
    * ES6的Modules
### 模块化的核心
1. 导出
2. 导入
### CommonJS
* 导出
```javascript
    // file name name.js
    flag:true;
    function sum(num1,num2){
       return num1 + num2
    }
    module.exports={
        flag,
        sum   
    }
```
* 导入
```javascript
    let { flag,sum } = require('name.js')
```
### ES6的模块化
* 导出
```javascript
    // file name demo.js
    flag:true;
    function sum(num1,num2){
       return num1 + num2
    }
    // 导出方式1
    export {
        flag,
        sum   
    }
    // 导出方式2
    export var name = '小明';
    export var age = 18
    // 导出方式3 导出函数/类
    export function reduce(num1,num2){
        if(num1>num2){
            return num1-num2
        }   
    }
    export class Person{
        eat(){
            console.log('吃')
        }
    }
    // 导出方式4 使用export default
    export default function(num1,num2){
        return num1*num2
    }
    
```
* 导入
```javascript
// 导入对象中定义的变量
import {flag,sum} from 'demo.js'
// 导入export定义的变量
import {name,age} from 'demo.js'
// 导入export定义的function
import {reduce,Person} from 'demo.js'
// 导入export default的内容
import otherName from 'demo.js'
otherName(); // 执行的便是num*num2 
// 统一全部导入
import * as otherName from 'demo.js'
```
## webpack
> 模块和打包
> 为了可以正常运行,依赖于node环境

* webpack.config.js
```javascript
const path = require('path');       // 依赖的node中的path包
module.exports = {
    entry:'',
    output:{
        path:path.resolve(__dirname,'dist'),            // 必须是一个绝对路径  需要动态获取文件路径  通过node的path包
        filename:''
    }
}
```

### loader
> 转换TS、scss/less、.jsx、.vue等文件转成js/css文件
#### 使用
* npm安装需要使用的loader
    * 不同的文件需要不同的loader
* 在webpack.package.js文件中的modules关键字下进行配置

##### 当webpack使用多个loader的时候,是从右至左的
|文件|所需loader|解释|
|:---:|:---:|:---:|
|.css文件|css-loader|打包css文件,只负责将加载css文件,不负责解析|
|--|style-loader|将样式添加到DOM文档中|




















