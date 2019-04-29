# 5. 引用类型

1. 在ES中，引用类型是一种数据结构，Object、Array、Date、RegExp、Function、基本包装类型（3个）、单体内置对象（2个）
2. 对象是某个特定引用类型的实例，新对象是使用new操作符后跟一个构造函数来创建的 `var person = new Object();`等同于`var person = {}`，定义了只包含默认属性和方法的对象
3. 在通过对象字面量定义对象时，实际上不会调用Object构造函数

