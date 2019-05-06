# Undefined

* `Undefined` 类型只有一个值，即特殊的 `undefined`；
* 对未初始化和未声明的变量执行 typeof 操作符都返回了 `"undefined"` 值；
* `null` 和 `undefined` 值没有 `toString()` 方法，`null` 和 `undefined` 可以使用 `String()` 转型函数来返回字面量；
* 实际上，`undefined` 值是派生自 `null` 值的；
* ```javascript
  null == undefined; // true
  String(undefined); // "undefined"
  ```

