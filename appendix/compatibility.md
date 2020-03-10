# 兼容性汇总

## 严格模式  <a id="use-strict"></a>

* `"use strict";` 支持 IE10+、FireFox4+、Safari5.1+、Opera12+、Chrome； 

## 数组  <a id="array"></a>

* 支持 `Array.isArray()` 方法的浏览器有 IE9+、 Firefox 4+、 Safari 5+、 Opera 10.5+和 Chrome ；
* IE7 及更早版本对 JavaScript 的实现中存在一个偏差，其 `unshift()` 方法总是返回 `undefined` 而不是数组的新长度。 IE8 在非兼容模式下会返回正确的长度值；
* `indexOf()` 和 `lastIndexOf()` 方法查找特定项在数组中的位置非常简单，支持它们的浏览器包括 IE9+、 Firefox 2+、 Safari 3+、 Opera 9.5+和 Chrome ； 
* 支持ES5迭代方法 `every()、filter()、forEach()、map()、some()` 的浏览器有IE9+、 Firefox 2+、 Safari 3+、 Opera 9.5+和 Chrome ； 
* 支持ES5归并方法 `reduce()、reduceRight()` 的浏览器有 IE9+、 Firefox 3+、 Safari 4+、 Opera 10.5 和 Chrome ；

## 函数  <a id="function"></a>

* IE、 Firefox、 Chrome 和 Safari 的所有版本以及 Opera 9.6 都支持 `caller` 属性 ； 
* 支持 `bind()` 方法的有 IE9+、 Firefox 4+、 Safari 5.1+、 Opera 12+和 Chrome ；

## 日期  <a id="date"></a>
* 支持 `Data.now()` 方法的浏览器包括 IE9+、Firefox 3+、Safari 3+、Opera 10.5 和 Chrome。在不支持它的浏览器中，使用 `+` 操作符把 `Data` 对象转换成字符串，也可以达到同样的目的。

## 字符串  <a id="string"></a>
* 括号表示法访问个别字符的语法得到了 IE8 及 Firefox、Safari、Chrome 和 Opera 所有版本的 支持。如果是在 IE7 及更早版本中使用这种语法，会返回 undefined 值(尽管根本不是特殊的 6 undefined 值)。
  ```js
  var str = 'hello'
  console.log(str[1])
  ```
* 支持 `trim()` 方法的浏览器有 IE9+、Firefox 3.5+、Safari 5+、Opera 10.5+和 Chrome。此外，Firefox 3.5+、Safari 5+ 和 Chrome 8+还支持非标准的 `trimLeft()` 和 `trimRight()` 方法，分别用于删除字符串开头和末尾的空格。