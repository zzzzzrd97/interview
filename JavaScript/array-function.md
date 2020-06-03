## 数组的方法
### filter()
array.filter(callbackfn)
> 回掉函数:必须返回一个布尔值
> 返回true时,将该item加入新的数组中
> 返回false时,将该item过滤掉
### map()
array.map(callbackfn)
### reduce()
> 对数组中所有的数组进行汇总
> 参数
```javascript
    array.reduce(function(preValue,n){
        
    },0)
```