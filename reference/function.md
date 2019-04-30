# Function

## Function类型  <a id="basic"></a>

* 函数实际上是一个对象，每个函数都是Function类型的实例，与其他引用类型一样具有属性和方法，函数名实际上也是一个指向函数的指针；
* 函数的名字仅仅是一个包含指针的变量而已；
* 重复声明直接覆盖（没有函数重载）,下例在创建第二个函数时，实际上覆盖了引用第一个函数的变量 `add`；

  ```javascript
  function add (num) {
  return num+100;
  }
  function add (num) {
  return num+200;
  }
  var result = add(100) // 300
  // 以上代码等同于
  var  add = function (num) {
  return num+100;
  }
  add = function (num) {
  return num+200;
  }
  ```

## 函数返回值  <a id="return"></a>

* `return` 关键字；
* 实际上，未指定返回值的函数返回的是一个特殊的 `undefined` 值；

## 声明函数  <a id="defined"></a>

* 有声明提升；
* 实际上，解析器在向执行环境中加载数据时，对函数声明和函数表达式并非一视同仁。解析器会率先读取函数声明（声明提升），并使其在执行任何代码之前可用（可以访问）；

  ```javascript
  function fnAdd (a,b){
    document.write(a+b);
  }
  fnAdd(2,3);
  ```

## 表达式函数

* 没有声明提升；
* 至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行；

  ```javascript
  var fnAdd = function(a,b){
    document.write(a+b);
  }; // 表达式函数像声明变量一样具有这个分号
  fnAdd(2,3);
  ```

## 匿名函数  <a id="anonymity"></a>

* 基本格式： `(function(){})()`；
* 用途：可以立即执行一段代码（执行完毕立即销毁），并可以把返回值赋给变量；

## 函数内部属性  <a id="internal-property"></a>

* 函数内部有两个特殊对象 `arguments` 和 `this`；
* 函数体内部可通过 `arguments` 对象访问这个参数数组（非真正的Array）。非严格模式下，`arguments` 和命名参数的值保持同步，但内存空间独立，没有传递值的参数自动赋予 `undefined`。严格模式对 `arguments` 的限制。ECMAScript中的所有参数传递的都是值，不可能通过引用传递参数。`arguments.length` 可获得参数长度；
* `arguments` 有一个叫 `callee` 的属性其是一个指针，指向拥有这个 `arguments` 对象的函数，案例阶乘函数，常用于消除紧密耦合；
* `this`：引用的是函数据以执行的环境对象，也可以说是 `this` 值，当在网页的全局作用域中调用函数时，`this` 对象引用的就是 `window`；
* ES5规范化了另一个函数对象的属性：`caller` 属性，该属性保存着调用当前函数的函数的引用，如果是在全局作用域中调用当前函数，它的值时 `null`；

## 函数属性和方法 【未开始】  <a id="property-method"></a>

