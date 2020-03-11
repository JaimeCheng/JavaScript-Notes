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

## 函数声明  <a id="declaration "></a>

* 有声明提升，即使遇见 `return` 也不例外；
* 实际上，解析器在向执行环境中加载数据时，对函数声明和函数表达式并非一视同仁。解析器会率先读取函数声明（声明提升），并使其在执行任何代码之前可用（可以访问）；

  ```javascript
  fnAdd(2,3);
  function fnAdd (a,b){
    F();
    document.write(a+b);
    return;
    function F () {
      document.write(2);
    }
  }
  //
  function F(){
    A = 5;
    function A(){ }
    console.log(A);	//5
  }
  F();
  ```

## 函数表达式  <a id="expression"></a>

* 函数表达式与其他表达式一样，使用前必须先赋值；所以不像函数声明那样有函数提升；

  ```javascript
  var fnAdd = function(a,b){
    document.write(a+b);
  }; // 表达式函数像声明变量一样具有这个分号
  fnAdd(2,3);
  ```

## 匿名函数  <a id="anonymous"></a>

* 基本格式： `function(){}` 即 `function` 关键字后没有标识符，也叫拉姆达函数；
* ```js
  // 不要这样做，不同浏览器修正方法不一致，这种方式很危险
  if (condition) {
    function sayHi() { alert('Hi') }
  } else {
    function sayHi() { alert('Yo') }
  }
  // 应使用函数表达式
  var sayHi;
  if (condition) {
    sayHi = function () { alert('Hi') }
  } else {
    sayHi = function () { alert('Yo') }
  }
  ```

## 立即执行函数  <a id="immediate-function"></a>

* 创建并立即调用一个函数，即可以执行其中代码，又不会在内存中留下对该函数的引用；
* **var res = function a() {} ()** ，（函数表达式）立即执行该函数，必须使用一个变量接收返回值（或直接console等号右边），否则不会执行；
* **(function a() {} )()**，立即执行该函数，可以不用变量接收，函数外的括号可换成 `+` `-` `!`，例如`!function a(){}()`；
* **(function a() {} ())**，等价上条；
* **(function () {})()，(function () {} ())**，（匿名函数，函数表达式）立即执行该匿名函数，可以不用变量接收，同样可使用`+` `-` `!` ；
* 用立即执行函数的好处，通过定义一个匿名函数，创建了一个新的函数作用域，相当于创建了一个“私有”的命名空间，该命名空间的变量和方法，不会破坏污染全局的命名空间；
* 应用：**(function a(){}) **，会返回这个函数（不会执行），但是在括号外面无法调用该函数，需要一个变量接收该函数，`var fun = (function a(){})`,一般这个用在递归上见下文示例[递归函数万能实现方式](#recursion)；
* 在匿名函数中定义的任何变量，都会在执行结束时销毁； 

## 作为值的函数  <a id="asvalues"></a>

* 函数名本身是变量，所以不仅可以把函数像参数一样传递，还可以将其作为另一函数的结果返回；
* 应用示例：
  ```js
  var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];
  data.sort(createComparisonFunction("name"));
  alert(data[0].name); //Nicholas
  data.sort(createComparisonFunction("age"));
  alert(data[0].name); //Zachary
  
  function createCompariFunction (propertyName) {
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

## 函数内部属性  <a id="internals"></a>

* 函数内部(函数体内)有两个特殊对象 `arguments` 和 `this`；
* 函数体内部可通过 `arguments` 对象访问这个参数数组（非真正的Array）。非严格模式下，`arguments` 和命名参数的值保持同步，但内存空间独立，没有传递值的参数自动赋予 `undefined`。严格模式对 `arguments` 赋值会变得无效，重写 `arguments` 值会导致语法错误。ECMAScript中的所有参数传递的都是值，不可能通过引用传递参数。`arguments.length` 可获得参数长度，[arguments详细说明](../content/chapter03.md#function)；
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

## 函数属性和方法  <a id="properties-methods"></a>

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

- **闭包**相关内容详见[第七章](../content/chapter07.md#closures)；

* 闭包是能读取其他函数内部变量的函数。在一个函数内部定义了其他函数就创建了闭包，原理如下：
  - 在后台执行环境中，闭包的作用域链包含着它自己的作用域、包含(外部)函数的作用域和全局作用域；
  - 通常，函数的作用域及其所有变量都会在函数执行结束后被销毁；
  - 但是，当函数返回一个闭包时，这个函数的作用域会一直在内存中保存到闭包不存在为止；
* 使用闭包可以在JavaScript中模仿块级作用域（js本身没有这个概念），要点如下：
  - 创建并立即调用一个函数，既可以执行其中代码，又不会在内存中留下对该函数的引用；
  - 结果就是函数内部的所有变量都会被立即销毁——除非将某些变量赋值给了包含(外部)作用域的变量；
* 闭包还可以在对象中创建私有变量，要点如下：
  - 即使js中没有正式的私有对象属性的概念，但可以使用闭包实现公有方法，而通过公有方法可以访问在包含作用域中定义的变量；
  - 有权访问私有变量的公有方法叫做特权方法；
  - 可以使用构造函数模式、原型模式来实现自定义类型的特权方法，也可以使用模块模式、增强的模块模式来实现单例的特权方法；
* 由于闭包会携带包含它的函数的作用域，因此比其他函数占用更多内存，建议在绝对必要时再考虑使用闭包；
