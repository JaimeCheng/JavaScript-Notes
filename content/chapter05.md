# 5. 引用类型

* [**Array**](../reference/array.md) —— 一组值的有序列表，同时提供了操作和转换这些值的功能；
* [**Object**](../reference/object.md) —— 基础类型，其他所有类型都从它继承了基本的行为；
* [**Function**](../reference/function.md) —— 函数时该类型的实例，故函数也是对象，故而函数可以拥有方法来增强其行为；
* [**Date**](../reference/date.md) —— 提供了有关日期和时间的信息，包括当前日期时间以及相关计算的功能；
* [**RegExp**](../reference/regexp.md) —— ES支持正则表达式的一个接口，提供了最基本和一些高级正则表达式功能；
* [**基本包装类型**](../reference/primitive-wrapper.md) —— 使得基本类型值可以被当作对象来访问；都映射到同名的基本类型；每读取一个基本类型值时，后台就会创建一个对应的基本包装类型对象，但只存在于代码的执行瞬间，执行完毕就立即销毁；
  * **Boolean类型**
  * **Number类型**
  * **String类型**
* [**单体内置对象** ](../reference/singleton-built-in-object.md)—— 所有代码执行前，作用域中就已存在这两个内置对象；
  * **Global对象** —— 大多ES实现中不能直接访问该对象，但web浏览器实现了承担该角色的[window对象](chapter08.md#window-object)；
  * **Math对象** —— 用于辅助完成复杂的数学计算任务；
* 详解见[引用类型](../reference/)

