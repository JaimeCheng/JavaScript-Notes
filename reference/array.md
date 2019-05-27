# Array

## 创建数组  <a id="create"></a>

```javascript
  var colors = new Array(3) // 创建一个length=3的数组
  var names = new Array("a", "b", "c") // 创建包含这三项的数组
  var arr = ["a", "b", "c"] // 字面量表示法，与Object一样，字面量不会调用Array()构造函数
```

## length属性  <a id="length"></a>

* 不是只读的，设置length可以从数组的末尾移除项或添加新项，新项的值未赋予时是`ubdefined`；

  ```javascript
  var colors = ["red", "blue", "pink"]
  colors[colors.length] = "black"  // 在末尾添加新项
  ```

## 检测数组  <a id="detecting-arrays"></a>

* 只有一个全局执行环境时 `if(arr instanceof Array){}`；
* ES5新增可以不考虑多个全局执行环境，`if(Array.isArray(arr)){}`；

## 转换方法  <a id="conversions"></a>

```javascript
var arr = ['a', 'b', 'c']
var arr1 = ['a', undefined, null]
console.log(arr.toLocaleString()) // a,b,c
console.log(arr.toString())       // a,b,c
console.log(arr.valueOf())        // ["a", "b", "c"]
console.log(arr1.toString())     // a,,
console.log(arr.join('->'))      // a->b->cf
```

* `join` 方法可重现 `toString` 的返回值，如果不给 `join` 传任何值，或传入 `undefined`，默认使用逗号作为分隔符；
* 如果数组的某一项是 `undefined` 或 `null`，`toString` 、`join` 和 `toLocaleString` 返回的结果中以空字符串表示；

## 栈方法LIFO  <a id="lifo"></a>

栈，后进先出（Last-In-First-Out）

* **push\(\)**：往数组末尾推入任意个项，返回修改后的数组 `length`；
* **pop\(\)**：移除数组末尾一项，数组 `length`减1，返回移除的项；

## 队列方法FIFO  <a id="fifo"></a>

队列，先进先出（First-In-First-Out），队列在列表末端添加项（已有 `push` 方法），从列队前端移除项

* **shift\(\)**：移除数组第一项，数组 `length` 减1，返回移除的项；
* **unshift\(\)**：在数组前端添加任意个项，返回新数组的 `length`；

`arr.unshift('red','pink')`，参数应视为整体添加到前端；

## 重排序方法  <a id="reorder"></a>

* **reverse\(\)**：翻转数组顺序，倒序 1,2,3,4,5 =&gt; 5,4,3,2,1；
* **sort\(\)**：无参数时，每项调用 `toString()`，按升序排列，非常不好用，因此可以接受一个比较函数作为参数，比较函数接收2个参数，如果参数一应该位于参数2之前返回一个负数，相等返回0，应位于参数2之后返回正数；

```javascript
var arr = [2, 1, 23, 19]
function compare(v1, v2) {
if (v1 < v2) {
  return -1
} else if (v1 > v2) {
  return 1
} else {
  return 0
}
}
// 比较数值类型的可简化
function compare(v1, v2) {
return v1-v2 //升序 v2-v1降序
}
arr.sort(compare)
console.log(arr) // [1,2,19,23]
```

* **reverse\(\)**和**sort\(\)**返回值都是排序后的数组（修改原数组）；

## 操作方法  <a id="manipulation"></a>

* **concat\(\)**：基于当前数组的所有项创建一个**新数组**（不修改原数组），先创建当前数组的一个副本，然后将接收的参数添加到副本的末尾，如果参数是一或多个数组，则将这些数组的每一项添加副本末尾，即合并数组；
* **slice\(\)**：基于当前数组的一或多个项创建一个**新数组**（不修改原数组），可接受1-2个参数，即要返回项的起始和结束位置，只有一个参数返回从指定位置到末尾所有项，2个参数返回起始位置到结束位置之间的项（但不包括结束位置），任何不合法的参数都返回空数组，如果结束位置大于最大索引，则等同于只有一个参数；
* **splice\(\)**：向数组中部插入、删除、替换项，并返回一个包含从原数组中删除的项数组（如没有删除则返回空数组），该方法会修改原数组，简单理解为3个参数 （起始位置，要删除的项数，要插入的项）；
  * 删除：删除任意数量的项，2个参数 （起始位置索引，删除项数）；
  * 插入：向指定位置插入任意数量的项，3个参数（起始位置，0\(即要删除的项数\)，要插入的项）；
  * 替换：向指定位置 插入数量的项并同时删除任意数量的项，3个参数（起始位置，要删除的项数，要插入的任意数量的项）；

```javascript
// concat
var arr = ['a', 'b', 'c']
var concat_arr = arr.concat('red', ['x', 'y'])
console.log(arr)         // ["a", "b", "c"]
console.log(concat_arr)  // ["a", "b", "c", "red", "x", "y"]

// slice
var brr = ['aa', 'bb', 'cc', 'dd', 'ee']
var slice_arr1 = brr.slice(3)     // ["dd", "ee"]
var slice_arr2 = brr.slice(1,3)   // ["bb", "cc"]
var slice_arr3 = brr.slice(-3,-2) // slice(arr.length+(-3), arr.length+(-2))  ["cc"]
var slice_arr4 = brr.slice(3,6)   // ["dd", "ee"]
var slice_arr5 = brr.slice(5,4)   // []

// splice
var crr = ['xx', 'yy', 'zz', 'jj', 'kk']
var removed = crr.splice(1, 1)
console.log(crr)    // ["xx", "zz", "jj", "kk"]
console.log(removed) // ["yy"]

removed = crr.splice(0, 0, 'a', 'b')
console.log(crr)     // ["a", "b", "xx", "zz", "jj", "kk"]
console.log(removed) // []

removed = crr.splice(0, 2, 'm', 'n')
console.log(crr)     // ["m", "n", "xx", "zz", "jj", "kk"]
console.log(removed) // ["a", "b"]
```

## 位置方法  <a id="location"></a>

* **indexOf\(\)**：2个参数，要查找的项和查找起点索引\(可选\)，从数组开头开始向后；
* **lastIndexOf\(\)**：同上，从数组末尾开始向前查找；

两个方法都返回查找项的索引，如果没找到返回 `-1`，查找的项必须严格相等（`===`）严格相等时注意对象就算字面量一样如果引用不一样也不行。

## 迭代方法  <a id="iteration"></a>

ES5定义了5个迭代方法，每个方法接收2个参数， 要在每项上运行的函数 `function(item, index, array){}` 和运行该函数的作用域对象\(可选\)——影响 `this` 的值。

* **every\(\)**：对每一项运行给定函数，如果该函数对每一项都返回 `true`，则返回 `true`；
* **filter\(\)**：对每一项运行给定函数，最后返回该函数会返回 `true` 的项组成的数组；
* **forEach\(\)**：对每一项运行给定函数，该方法没有返回值；
* **map\(\)**：对每一项运行给定函数，返回每次函数调用的 `return` 的结果组成的数组；
* **some\(\)**：对每一项运行给定函数，如果该函数对任一项返回 `true`，则返回 `true`；

以上方法都不会修改数组中包含的值,，如果项是**对象可以修改属性**。

```javascript
var numbers = [1,2,3,4,5,4,3,2,1];

var everyResult = numbers.every((item, index, array) => {
    return (item > 2);
}); // false

var someResult = numbers.some((item, index, array) => {
    return (item > 2);
}); // true

var filterResult = numbers.filter((item, index, array) => {
    return (item > 2);
}); // [3, 4, 5, 4, 3]

var mapResult = numbers.map((item, index, array) => {
    return (item * 2);
}); // [2, 4, 6, 8, 10, 8, 6, 4, 2]

numbers.forEach((item, index, array) => {
  // 执行某些操作，但不会修改数组
})
```

## 归并方法  <a id="reduction"></a>

ES5新增了两个归并数组的方法，这两个方法都会迭代所有项，然后构建一个最终返回值，都接收两个参数，要在每一项上调用的函数 `function(prev,cur,index,array){}`，作为归并基础的初始值\(可选\)，给定函数返回的任何值都会作为第一个参数 `prev` 自动传给下一项，第一次迭代发生在数组第二项，如果设置了初始值则从第一项开始迭代。

* **reduce\(\)**：从第一项开始逐个遍历到最后；
* **reduceRIght\(\)**：从最后一项开始，向前遍历到第一项；

```javascript
var arr = [1,2,3,4,5]
var res = arr.reduce((prev, curr)=>{
  return prev+curr
},10)
console.log(res) // 25 如果不加初始值10则结果15
```

## 常见算法  <a id="algorithm"></a>

* **二分排序**
* **冒泡排序**
* **插入排序**
* **选择排序**
* **归并排序**
* **希尔排序**
* **快速排序**
* **堆排序**
* **基数排序**
* **桶排序**

