---
description: 函数表达式是JavaScript中既强大又容易令人困惑的特性
---
# 7. 函数表达式

## 函数表达式  <a id="expression"></a>

* 函数表达式与其他表达式一样，使用前必须先赋值；所以不像函数声明那样有函数提升；

  ```javascript
  var fnAdd = function(a,b){
    document.write(a+b);
  }
  fnAdd(2,3);
  ```
* 上述示例中，赋值给变量的没有名字的函数叫做[匿名函数](../reference/function.md#anonymous)，有时也叫拉姆达函数；

## 递归  <a id="recursion"></a>

* 递归函数是在一个函数通过名字调用自身的情况下构成的，即函数自己调用自己；
  
* 递归必须有退出递归的条件否则成为死循环；
  
  ```js
  // 经典阶乘函数
  function factorial (num) {
   return num <= 1 ? 1 : num * factorial(num - 1);
  }
  
  var another = factorial;
  factorial = null;
  another(4); // 出错 factorial is not a function
  ```
  
* 以上代码先把 `factorial()` 函数保存在变量 `another` 中，然后将 `factorial` 变量设置为 `null`，结果指向原始函数的引用只剩下一个。但在接下来调用`another()` 时，由于必须执行 `factorial()`，而 `factorial` 已经不再是函数，所以就会导致错误。在这种情况下，使用 `arguments.callee` 可以解决这个问题；
  
* 递归函数应始终使用 `arguments.callee` 来递归地调用自身，不是用函数名，因其可能发生变化；
  
  ```js
  function factorial (num) {
   return num <= 1 ? 1 : num * arguments.callee(num - 1);
  }
  ```
  
* `arguments.callee`  是指向正在执行的函数的指针，但严格模式下不可用；

* 严格模式或非严格模式下递归调用并降低耦合的方式如下：
  ```js
  var factroial = (function f (num) {
    return num <= 1 ? 1 : num * f(num - 1);
  }) // 外部不能调用f()
  ```

## 闭包 <a id="closures"></a>

**闭包** 是指 可以访问读取其他函数（包含函数）作用域中的变量的函数，创建闭包的常见方式：在一个函数内部创建另一个函数；

```js
function createCompariFunction (propertyName) {
  return function (obj1, obj2) {
    var value1 = obj1[propertyName]; // 访问了外部函数中的变量propertyName
    var value2 = obj2[propertyName]; // 
    if (value1 < value2) {
      return -1;
    } else if (value1 > value2) {
      turn 1;
    } else {
      return 0;
    }
  }
}

var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];
data.sort(createComparisonFunction("name"));
data.sort(createComparisonFunction("age"));
```

在这个例子中，打注释的两行代码访问了外部函数中的变量propertyName，之所以能访问，是因为内部函数的作用域链包含 `createCompareFunction()`  的作用域；

要理解闭包必须深刻理解执行环境和作用域链，详见[第4章](chapter04.md#execution-context-scope)；