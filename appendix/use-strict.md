# 严格模式规则

## 变量声明  <a id="variable-declaration"></a>

* 部分保留字不能作为标识符和属性名；eg.不能定义名为 `eval` 或 `arguments` 的变量，否则会导致语法错误； 
* 给未经声明的变量赋值在严格模式下会导致抛出 `ReferenceError` 错误； 初始化未经声明的变量会导致错误；
* 对于尚未声明过的变量，只能执行一项操作，即使用 `typeof` 操作符检测其数据类型（对未经声明的变量调用 delete 不会导致错误，但这样做没什么实际意义，而且在严格模式下确实会导致错误）； 

## Number类型  <a id="number"></a>

* 八进制字面量在严格模式下是无效的，会导致支持的 JavaScript 引擎抛出错误 ； 

## 语句  <a id="statements"></a>

* 严格模式下不允许使用 `with` 语句，否则将视为语法错误 ； 

## 函数  <a id="function"></a>

* 严格模式对函数限制除了参数名和函数名外，不能出现两个命名参数同名的情况 ，否则会语法错误； 
* 严格模式对如何使用 `arguments` 对象做出了一些限制。首先，像前面例子中那样的赋值会变得无效。也就是说，即使把 `arguments[1]` 设置为 10， `num2` 的值仍然还是 `undefined`。其次，重写 `arguments` 的值会导致语法错误（代码将不会执行）；
* ```javascript
   function doAdd(num1, num2) {
    arguments[1] = 10;
    alert(arguments[0] + num2);
   }
  ```
* 严格模式下，`argunments.callee` 会导致错误，非严格模式下，ES5还定义了 `arguments.caller` 属性，在严格模式下访问会导致错误，非严格模式下这个属性始终是 `undefined`，定义该属性是为了区分函数的 `caller` 属性和 `arguments.caller`；
* 严格模式下，不能为 `caller` 属性赋值，否则会导致错误； 
* `setTimeout` 都是在全局作用域中执行的，因此函数中 `this` 的值在非严格模式下指向 `window` 对象，在严格模式下是 `undefined` ；(虽然有不少的书上这么写，经测试，在严格模式下，`setTimeout()` 的回调函数里面的 `this` 仍然默认指向 `window对象`，并不是`undefined`)
  ```js
  function foo() {
    setTimeout(function(){
      console.log('id',this.id)
    },100)
  }
  var id = 21;
  foo.call({'id': 42})
  ```


## 对象  <a id="object"></a>
* 对象的只读属性(`writable: false`)是不可修改的，如果尝试为它指定新值，则在非严格模式下，赋值操作将被忽略；在严格模式下，赋值操作将会导致抛出错误；
* 把对象属性的 `configurable` 特性设置为 `false`，表示不能从对象中删除属性。如果对这个属性调用 `delete`，则在非严格模式下什么也不会发生，而在严格模式下会导致错误；
* 访问器属性只指定 `getter`函数 意味着属性是不能写，尝试写入属性会被忽略。 在严格模式下，尝试写入会抛出错误。只指定 `setter` 也不能读，在非严格模式下会返回 `undefined`，在严格模式下会抛出错误；

## Global对象 <a id="global"></a>
* 严格模式下，在外部访问不到 `eval()` 中创建的任何变量或函数，为 `eval` 赋值也会导致错误；
