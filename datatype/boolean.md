# Boolean

* `Boolean` 类型是 ECMAScript 中使用得最多的一种类型，该类型只有两个字面值: `true` 和 `false`；
* 将一个值转换为其对应的 `Boolean` 值，可以调用转型函数 `Boolean()`；
* 其他数据类型转 `Boolean` 规则，这些转换规则对理解流控制语句\(如if语句\)自动执行相应的 `Boolean` 转换非常重要；

  | 数据类型 | 为true的值 | 为false的值 |
  | :---: | :---: | :---: |
  | **Boolean** | true | false |
  | **String** | 任何非空字符串 | ""空字符串 |
  | **Number** | 任何非零数字值\(包括无穷大\) | 0和NaN |
  | **Object** | 任何对象 | null |
  | **Undefined** | 不适用 | undefined |

