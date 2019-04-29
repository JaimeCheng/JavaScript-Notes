# 严格模式规则

1. 部分保留字不能作为标识符和属性名；eg.不能定义名为 eval 或 arguments 的变量，否则会导致语法错误；
2. 给未经声明的变量赋值在严格模式下会导致抛出 ReferenceError 错误； 初始化未经声明的变量会导致错误；
3. 对于尚未声明过的变量，只能执行一项操作，即使用 typeof 操作符检测其数据类型（对未经声明的变量调用 delete 不会导致错误，但这样做没什么实际意义，而且在严格模式下确实会导致错误） ;
4. 八进制字面量在严格模式下是无效的，会导致支持的 JavaScript 引擎抛出错误 ;
5. 严格模式下不允许使用 with 语句，否则将视为语法错误 ;
6. 严格模式对函数限制除了参数名和函数名外，不能出现两个命名参数同名的情况 ，否则会语法错误；
7. ```javascript
   function doAdd(num1, num2) {
    arguments[1] = 10;
    alert(arguments[0] + num2);
   }
   ```

   严格模式对如何使用 arguments 对象做出了一些限制。首先，像前面例子中那样的赋值会变得无效。也就是说，即使把 arguments\[1\]设置为 10， num2 的值仍然还是 undefined。其次，重写arguments 的值会导致语法错误（代码将不会执行）；

8. 严格模式下，`argunments.callee`会导致错误，非严格模式下，ES5还定义了`arguments.caller`属性，在严格模式下访问会导致错误，非严格模式下这个属性始终是undefined，定义该属性是为了区分函数的`caller`属性和`arguments.caller`
9. 严格模式下，不能为caller属性赋值，否则会导致错误

