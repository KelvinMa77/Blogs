##  数组

### 创建数组

### Array.from 

语法

>Array.from(arrayLike[, mapFn[, thisArg]])
>Array.from方法从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例
>Array.from() 方法有一个可选参数 mapFn，让你可以在最后生成的数组上再执行一次 map 方法后再返回

```

```

```javascript
// Array.from(document.querySelectorAll(".some-class"))
// Array.from(arguments)
// 创建一个0到100的数组
Array.from({length: 100}, function(v, i) {return i})
```

### Array.fill

语法

> arr.fill(value[, start[, end]])

 fill()方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素,不包括终止索引。这个方法会改变原数组
如果 start 是个负数, 则开始索引会被自动计算成为 length+start, 其中 length 是 this 对象的 length 属性值。如果 end 是个负数, 则结束索引会被自动计算成为 length+end

```javascript
Array(4).fill(1) // [1, 1, 1 ,1]
[1, 2, 3].fill(4, 1);            // [1, 4, 4]
[1, 2, 3].fill(4, -3, -2);       // [4, 2, 3]
[].fill.call({length: 3}, 2) // {0: 2, 1: 2, 2: 2, length: 3}

// 如果fill的参数为引用类型，会导致都执行都一个引用类型，
var arr = Array(3).fill({}) // [{}, {}, {}];
arr[0].hi = "hi"; // [{ hi: "hi" }, { hi: "hi" }, { hi: "hi" }]
```

### Array.of

> Array.of() 方法创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型

```
Array.of(7);       // [7] 
Array.of(1, 2, 3); // [1, 2, 3]
Array.of(undefined); // [undefined]
Array(7);          // [ , , , , , , ]
Array(1, 2, 3);    // [1, 2, 3]
```

### 查找数组元素

### ES5

### Array.prototype.filter 

查找所有符合条件的元素，返回元素集合

```javascript
let arr = [1, 2, 3, 4, 7]
arr.filter(v => v % 2 == 0) // [2, 4]
```

### ES6

#### Array.prorotype.find && Array.prorotype.findIndex

find找到第一个满足条件的元素就返回
findIndex找到第一个满足条件的元素的索引

```javascript
let arr = [1, 2, 3, 4, 7]
arr.find(v => v % 2 == 0) // 2
arr.find(v => v % 2 == 0) // 1
```

### 遍历数组

#### ES5中数组的遍历方法

以下面的arr來说明

```javascript
var arr = [0, 1 , 2 , 3]
arr.key = 'some'
Array.prototype.protoKey = "hahah"
```

1. for循环

```javascript
var arr = [0, 1 , 2 , 3]
arr.key = 'some'
for(var i = 0; i < arr.length; i++>) {
    console.log(arr[i]) // 0 1 2 3
}
```

2. forEach

```javascript
arr.forEach(function(v, i) {
    console.log(v)
})
// 0 1 2 3
```

```javascript
arr.forEach(function(v, i) {
    console.log(v)
    if(v == 2) {
       break; // Syntax Error
    }
})

```

3. every
   every方法测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值。

```javascript
arr.every(function(v, i) {
    console.log(v)
})
// 0 
```

注意只会输出第一个值，every一旦遇到一个回调函数的返回值是falsy, 那么every函数就退出

模拟实现continue的效果

```javascript
arr.every(function(v, i) {
    if(v == 2) {
       
    } else {
        console.log(v)
    }
    return true;
})
// 输出 0 1 3 
```

模拟实现break

```javascript
arr.every(function(v, i) {
    if(v === 2) {
        return false
    }
    console.log(v)
    return true;
})
//  输出 0 1
```

4. for in

```javascript
for(var i in arr) {
    console.log(i) // 0 1 2 3 key protoKey
    console.log(typeof i == 'number') // false i是字符串，不是数值
}
```

### 各种遍历方法对比

for循环支持支持continue, break语法，只遍历数组的索引属性

forEach不支持continue, break语法（使用continue, break直接报语法错误）,遍历无法提前终止, return语句也无效，只遍历数组的索引属性

every不支持continue, break语法，但是可以达到continue和break的效果, 通过return，只遍历数组的索引属性

for in 支持continue, break语法, 但是会**遍历数组和原型上的的所有可枚举的属性**

### ES6中数组遍历的方法

for of遍历
ES6为遍历提供了一个统一的接口, 凡是部署了Iterable接口的对象，都可以通for of遍历，所以不论是数组，对象，Map还是Set都可以通过for of遍历

### iterable
