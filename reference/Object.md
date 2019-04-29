[TOC]

#### 创建对象
```js
var obj = new Object() // 创建一个包含默认属性和方法的对象
obj.name = "Jaime"
var person = {
	name: "Jaime"
} // 字面量表示法，字面量不会调用Object()构造函数
```

#### 属性和方法

- **constructor**：保存着用于创建当前对象的函数（构造函数）
- **hasOwnProperty(propertyName)**：用于检查给定的属性在当前对象实例中是否存在（不是在实例的原型中），propertyName以字符串形式传入
- **isPrototypeof(object)**：用于检查传入的对象是否是传入对象的原型
- **propertyIsEnumerable(propertyName)**：用于检查给定的属性是否可使用for-in来枚举，for-in之前先检测对象变量是否是null或undefined，否则会报错
- **toLocaleString**：返回对象的字符串表示，该字符串与执行环境的地区对应
- **toString**：返回对象的字符串表示
- **valueOf**：返回对象的字符串、数值或布尔值表示，通常与toSting的返回值相同