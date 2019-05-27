# Function

## 创建函数  <a id="create"></a>

* 函数实际上是一个对象，每个函数都是Function类型的实例，与其他引用类型一样具有属性和方法，函数名实际上也是一个指向函数的指针；

* 函数的名字仅仅是一个包含指针的变量而已；

* 重复声明直接覆盖（没有函数重载）,下例在创建第二个函数时，实际上覆盖了引用第一个函数的变量 `add`；

* 定义函数还可以使用 `var sum = new Function(num1, num2);` 不推荐因为会导致解析两次代码，但便于理解“函数是对象，函数名是指针”，也就是说一个函数可能有多个名字；

  ```javascript
  function add (num) {
    return num+100;
  }
  function add (num) {
    return num+200;
  }
  var result = add(100) // 300
  // 以上代码等同于
  var add = function (num) {
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
  fnAdd(2,3);
  function fnAdd (a,b){
    document.write(a+b);
  }
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


## 作为值的函数  <a id="asvalue"></a>

* 函数名本身是变量，所以不仅可以把函数像参数一样传递，还可以将其作为另一函数的结果返回；
* 应用示例：
  ```js
  var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];
  data.sort(createComparisonFunction("name"));
  alert(data[0].name); //Nicholas
  data.sort(createComparisonFunction("age"));
  alert(data[0].name); //Zachary
  
  function createCompareFunction (propertyName) {
    return function (obj1, obj2) {
      var value1 = obj1[propertyName];
      var value2 = obj2[propertyName];
      if (value1 < value2) {
        return -1;
      } else if (value1 > value2) {
        turn 1;
      } else {
        return 0;
      }
    }
  }
  ```

## 函数内部属性  <a id="internal-property"></a>

* 函数内部(函数体内)有两个特殊对象 `arguments` 和 `this`；
* 函数体内部可通过 `arguments` 对象访问这个参数数组（非真正的Array）。非严格模式下，`arguments` 和命名参数的值保持同步，但内存空间独立，没有传递值的参数自动赋予 `undefined`。严格模式对 `arguments` 的限制。ECMAScript中的所有参数传递的都是值，不可能通过引用传递参数。`arguments.length` 可获得参数长度；
* `arguments` 有一个叫 `callee` 的属性其是一个指针，指向拥有这个 `arguments` 对象的函数，案例阶乘函数，常用于消除紧密耦合，严格模式下运行会导致错误；
  ```js
  function factorial (num) {
    return num <= 1 ? 1 : num * arguments.callee(num - 1);
  }
  ```
* `this`：引用的是函数据以执行的环境对象，也可以说是 `this` 值，当在网页的全局作用域中调用函数时，`this` 对象引用的就是 `window`；
* ES5规范化了另一个函数对象的属性：`caller` 属性，该属性保存着调用当前函数的函数的引用，如果是在全局作用域中调用当前函数，它的值时 `null`；严格模式下，不能为该属性赋值，否则会导致错误；
  ```js
  function outer () {
    inner();
  }
  function inner () {
    console.log(inner.caller); // outer函数的代码
  }
  outer();
  ```
* ES5还定义了 `arguments.caller` 属性，在严格模式下访问会导致错误，非严格模式下始终是 `undefined` ，定义该属性是为了区分函数的 `caller` 属性；

## 函数属性和方法  <a id="property-method"></a>

* **length**：表示函数希望接收命名参数的个数；
* **prototype**：是保存他们所有示例方法的真正所在，在ES5中， `prototype`  是不可枚举的，使用 `for-in` 无法发现；
* **apply()**：非继承而来的方法，设置函数体内 `this` 的值以扩充函数赖以运行的作用域，第一个参数是在其中运行的作用域，另一个是参数数组（Array实例 / arguments对象）；
* **call()**：同上，区别仅在于接收参数的方式不同，第一个参数都是 `this` 值，变化的是其余参数都直接传递给函数，即必须明确的传入每一个参数；结果与 `apply` 没有不同；
* **bind()**：ES5定义的一个方法，该方法会创建一个函数的实例，其 `this` 值会被绑定到传给 `bind()` 函数的值；
  ```js
  window.color = 'red';
  var o = { color: 'blue' };
  
  function sum (a, b) {
    console.log(this.color);
    return a + b;
  }
  
  function applySum (a, b) {
    return sum.apply(this, arguments); // this->window,因为在全局作用域调用
    // return sum.apply(o, [a, b]);
  }
  
  function callSum (a, b) {
    return sum.call(this, a, b);
  }
  
  function sayColor () { alert(this.color); }
  sayColor.call(this); // red
  sayColor.call(window);  // red
  sayColor.call(o);  // blue
  
  sayColor.bind(o)(); // blue 注意bind和以上两个区别
  var objSayColor = sayColor.bind(o); // blue
  ```

