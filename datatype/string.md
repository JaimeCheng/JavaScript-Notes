# String

* `String` 类型用于表示由零或多个 16 位 Unicode 字符组成的字符序列，即字符串；
* `String` 数据类型包含一些特殊的字符字面量，也叫转义序列；

  | 字面量 | 含义 |
  | :---: | :--- |
  | **\n** | 换行 |
  | **\t** | 制表 |
  | **\b** | 空格 |
  | **\r** | 回车 |
  | **\\** | 斜杠 |
  | **\"** | 双引号，... |

* 任何字符串的长度可以通过其 `length`属性获得；
* **toString\(\)** 方法，返回相应值的字符串表现，`null` 和 `undefined` 没有这个方法，通过传递基数，`toString(基数)` 可以输出以二进制、八进制、十六进制，乃至其他任意有效进制格式表示的字符串值；

  ```javascript
  var num = 10;
  alert(num.toString()); // "10"
  alert(num.toString(2)); // "1010"
  alert(num.toString(8)); // "12"
  alert(num.toString(10)); // "10"
  alert(num.toString(16)); // "a"
  // 拓展：结合parseInt() 进制的相互转换
  ```

* 转型函数 **String\(\)**，这个函数能够将任何类型的值转换为字符串；

  * 如果值有 `toString()` 方法，则调用该方法\(没有参数\)并返回相应的结果；
  * 如果值是 `null`，则返回 `"null"`；
  * 如果值是 `undefined`，则返回 `"undefined"`；

  ```javascript
  var arr = [];
  arr.toString(); // ""
  String(arr); // ""
  arr = [2, 3];
  arr.toString(); // "2,3"
  String(arr); // "2,3"
  ```

