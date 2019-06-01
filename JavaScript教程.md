Java Script 教程

## Object.assign

Object.assign方法用于对象的合并，将源对象（ source ）的所有可枚举属性，复制到目标对象（ target ）。

```javascript
var target = { a: 1 };  
var source1 = { b: 2 };  
var source2 = { c: 3 };  
Object.assign(target, source1, source2);  
target // {a:1, b:2, c:3}  
```

Object.assign方法的第一个参数是目标对象，后面的参数都是源对象。

##  

## 数组 reduce()方法

```javascript
arr.reduce(callback,[initialValue])
```

* callback （执行数组中每个值的函数，包含四个参数）
  - previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
  - currentValue （数组中当前被处理的元素）
  - index （当前元素在数组中的索引）
  - array （调用 reduce 的数组）
* initialValue （作为第一次调用 callback 的第一个参数。）

```javascript
var items = [10, 120, 1000];

// our reducer function
var reducer = function add(sumSoFar, item) { return sumSoFar + item; };

// do the job
var total = items.reduce(reducer, 0);

console.log(total); // 1130
```

如何知道一串字符串中每个字母出现的次数？

```javascript
var arrString = 'abcdaabc';

arrString.split('').reduce(function(res, cur) {
    res[cur] ? res[cur] ++ : res[cur] = 1
    return res;
}, {})
```

koa的源码中，有一个only模块

```javascript
var a = {
    env : 'development',
    proxy : false,
    subdomainOffset : 2
}
only(a,['env','proxy'])   // {env:'development',proxy : false}

var only = function(obj, keys){
  obj = obj || {};
  if ('string' == typeof keys) keys = keys.split(/ +/);
  return keys.reduce(function(ret, key){
    if (null == obj[key]) return ret;
    ret[key] = obj[key];
    return ret;
  }, {});
};
```



> 参考网址 [JS进阶篇--JS数组reduce()方法详解及高级技巧](https://segmentfault.com/a/1190000010731933)

## slice

语法

```javascript
array.slice(start,end)
```

示例

```javascript
//数组
var a=[1,2,3,4,5,6];
var b=a.slice(0,3);     //[1,2,3]
var c=a.slice(3);       //[4,5,6]

//字符串
var a="i am a boy";
var b=a.slice(0,6);
```



## splice

语法

```javascript
array.splice(start,deleteCount,item...)
```

示例

```javascript
var a=['a','b','c'];
var b=a.splice(1,1,'e','f');    //a=['a','e','f','c'],b=['b']
```

## split

语法

```javascript
string.split(separator,limit)
```

示例

```javascript
var a="0123456";
var b=a.split("",3);    //b=["0","1","2"]
```

## bind

```javascript
this.x = 9;
var module = {
  x: 81,
  getX: function() { return this.x; }
};

module.getX(); // 81

var retrieveX = module.getX;
retrieveX();  // 9

var boundGetX = retrieveX.bind(module);
boundGetX(); // 81
```

1. `module.getX();` 的结果是 81，因为 getX 里的 this 是 module, 所以 this.x 是 module 里的 `x = 81`。
2. `retrieveX();` 的结果是 9， 因为这时相当于 `var retrieveX = function() { return this.x; };`， `retrieveX();` 相当于在全局跑了遍函数里的内容，this.x 是 全局的 `this.x = 9。
3. `var boundGetX = retrieveX.bind(module);`，**bind(module) 的作用是每当调用 retrieveX() 这个函数时，这个函数里的 this 都是 module，替换掉了全局的 this**，在 boundGetX() 调用时，返回的是 `module.x`，所以是 81。

> 参考： [JavaScript bind() 的用法](https://www.jianshu.com/p/ee175cade48b)

## Number

```javascript
将一个值转换为字符串的3种方法
1.value.toString()
2."" + value		//可读性差
3.String(value)		
```




| 描述              | 函数              |
| --------------- | --------------- |
| 丢弃小数部分,保留整数部分   | parseInt(5/2)   |
| 向上取整,有小数就整数部分加1 | Math.ceil(5/2)  |
| 四舍五入            | Math.round(5/2) |
| 向下取整            | Math.floor(5/2) |

















