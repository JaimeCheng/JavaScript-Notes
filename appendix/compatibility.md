# 兼容性汇总

1. `"use strict";` 支持 IE10+、FireFox4+、Safari5.1+、Opera12+、Chrome
2. IE、 Firefox、 Chrome 和 Safari 的所有版本以及 Opera 9.6 都支持 caller 属性 
3. 支持 Array.isArray\(\)方法的浏览器有 IE9+、 Firefox 4+、 Safari 5+、 Opera 10.5+和 Chrome 
4. IE7 及更早版本对 JavaScript 的实现中存在一个偏差，其 unshift\(\)方法总是返回 undefined 而不是数组的新长度。 IE8 在非兼容模式下会返回正确的长度值
5. indexOf\(\)和 lastIndexOf\(\)方法查找特定项在数组中的位置非常简单，支持它们的浏览器包括 IE9+、 Firefox 2+、 Safari 3+、 Opera 9.5+和 Chrome 
6. 支持ES5迭代方法`every()、filter()、forEach()、map()、some()`的浏览器有IE9+、 Firefox 2+、 Safari 3+、 Opera 9.5+和 Chrome 
7. 支持这ES5归并方法`reduce()、reduceRight()`的浏览器有 IE9+、 Firefox 3+、 Safari 4+、 Opera 10.5 和 Chrome 

