# Null

* `Null` 类型是第二个只有一个值的数据类型，这个特殊的值是 `null`；
* `null` 值表示一个空对象指针，所以 `typeof null` 会返回 `"object"`；
* 只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存 `null` 值；
* ```javascript
  null == undefined; // true
  String(null); // "null"
  ```

