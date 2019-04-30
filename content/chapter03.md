# 3. JavaScript基本概念

### 1. 基本概念

* 几个基本概念：标识符、关键字、操作符、语句、函数
* ECMAScript的一切（变量、函数名和操作符）都区分大小写
* 语句末尾建议加`;`，某些情况增进代码性能
* var未初始化的变量会保存一个特殊的值
* 一条语句定义多个变量，用`,`分隔开

### 2. 数据类型

* [基本+复杂+ES6](../datatype/)
* 相互转换见[附录](../appendix/data-type-conversion.md)

#### 3. `typeof`操作符
* `typeof null`返回值
* 从技术角度讲，函数在 ES 中是对象，不是一种数据类型。然而，函数也确实有一些特殊的属性，因此通过 typeof 操作符来区分函数和其他对象是有必要的

#### 4. 

8. **undefined 和 null 的特殊性，`null == undefined // true`**<br/>
9. **浮点计算的误差，永远不要测试某个特定的浮点数值**<br/>
10. 监测和监控极大或极小数值的必要性
11. NaN的特殊性，isNaN\(\)
12. Number\(null\)、Number\(undefined\)、Number\({}\)、Number\(\[\]\)、Number\(""\)，和parseInt\(\)的结果可能会不同，建议使用parseInt；parseInt\(\)应明确指定基数。parseInt\("10", 10\)解析十进制
13. null和undefined没有`toString()`方法，数值的`toString()`可以传一个参数，进制基数\(应用到进制间转换\)，null和undefined可以使用String\(null\)转型函数，返回字面量"null"，undefined派生自null
14. object的每个实例都具有的属性和方法
15. 操作符：a++和++a的重要区别，联想记忆看顺序变量在前就先用再计算++
16. 逻辑与&&、逻辑或\|\|  是短路操作符；`||`的这一特性可以用来避免变量赋null或undefined
17. 严格模式不允许使用with语句，大量with语句会导致性能下降，不建议使用类型转换
18. 函数体内部可通过arguments对象访问这个参数数组（非真正的Array）。非严格模式下，arguments和命名参数的值保持同步，但内存空间独立，没有传递值的参数自动赋予undefined。严格模式对arguments的限制。EcMAScript中的所有参数传递的都是值，不可能通过引用传递参数
19. 实际上，未指定返回值的函数返回的是一个特殊的undefined值
20. 由于不存在函数签名的特性，ECMAScript函数不能被重载
21. i++    是在for循环结束之前的最后一句执行
22. break 和 continue 语句都可以与 label 语句联合使用，从而返回代码中特定的位置。这种联合使用的情况多发生在循环嵌套的情况下
23. 匿名函数

