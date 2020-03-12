# Object

## 创建对象   <a id="create"></a>

```javascript
var obj = new Object() // 创建一个包含默认属性和方法的对象
var obj1 = {} // 字面量语法时，如果留空其花括号，则可以定义只包含默认属性和方法的对象
obj.name = "Jaime"
var person = {
    name: "Jaime"
} // 字面量表示法，字面量不会调用Object()构造函数，适合来封装多个可选参数
```

## 默认属性和方法   <a id="properties-methods"></a>

* **constructor**：保存着用于创建当前对象的函数（构造函数）；
* **hasOwnProperty\(propertyName\)**：用于检查给定的属性在当前对象实例中是否存在（不是在实例的原型中），propertyName以字符串形式传入；
* **isPrototypeof\(object\)**：用于检查传入的对象是否是传入对象的原型；
* **propertyIsEnumerable\(propertyName\)**：用于检查给定的属性是否可使用 `for-in` 来枚举，`for-in` 之前先检测对象变量是否是 `null` 或 `undefined`，否则会报错；
* **toLocaleString()**：返回对象的字符串表示，该字符串与执行环境的地区对应；
* **toString()**：返回对象的字符串表示；
* **valueOf()**：返回对象的字符串、数值或布尔值表示，通常与 `toSting` 的返回值相同；


## 属性检测   <a id="detecting-properties"></a>

* `typeof obj['name']` 操作符检测某个属性是否存在，不存在则 `'undefined'`；
* `obj.hasOwnProperty('name')` 返回布尔值；

## 属性类型 <a id="property-type"></a>

* **数据属性**：数据属性包含一个数据值的位置。在这个位置可以读取和写入值。有如下 4 个描述其行为的特性：
  - [[Configurable]]: 表示能否通过 `delete` 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。像那样直接在对象上定义的属性，它们的这个特性默认值为 `true`；
  - [[Enumerable]]: 表示能否通过 `for-in` 循环返回属性。像那样直接在对象上定义的属性，默认值为 `true`；
  - [[Writable]]: 表示能否修改属性的值。像直接在对象上定义的属性，默认值为 `true`；
  - [[Value]]: 包含这个属性的数据值。读取属性值的时候，从这个位置读;写入属性值的时候，把新值保存在这个位置。默认值为 `undefined`。
  
  要修改属性默认的特性，必须使用 `Object.defineProperty()` 方法。接收三个参数: 属性所在的对象、属性的名字和一个描述符对象。其中，描述符(descriptor)对象的属性必须特性中的一个或多个。 
  ```js
  var person = {}; 
  Object.defineProperty(person, "name", {
    writable: false,
    value: "Nicholas" 
  });
  alert(person.name); //"Nicholas" 只读属性
  person.name = "Greg"; 
  alert(person.name); //"Nicholas" 在非严格模式下，赋值操作将被忽略;在严格模式下，赋值操作将会导致抛出错误
  ```
  类似的规则也适用于不可配置的属性。把 `configurable` 设置为 `false`，表示不能从对象中删除属性。如果对这个属性调用 `delete`，则在非严格模式下什么也不会发生，而在严格模式下会导致错误。而且，一旦把属性定义为不可配置的，就不能再把它变回可配置了。此时，再调用 `Object.defineProperty()` 方法修改除 `writable` 之外的特性，都会导致错误。
  
  在调用 `Object.defineProperty()` 方法时，如果不指定，`configurable`、`enumerable` 和 `writable` 特性的默认值都是 `false`。多数情况下，用不到这些高级功能。由于实现不彻底，建议读不要在 IE8 中使用 `Object.defineProperty()` 方法。
  
* **访问器属性**：包含一对儿 `getter` 和 `setter` 函数(两个函数都非必需)。读取访问器属性时，会调用 `getter` 函数，返回有效的值；在写入访问器属性时，会调用 `setter` 函数并传入新值，这个函数负责决定如何处理数据。有如下 4 个描述其行为的特性：
  - [[Configurable]]: 表示能否通过 `delete` 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为数据属性。对于直接在对象上定义的属性，默认值为 `true`；
  - [[Enumerable]]: 表示能否通过 `for-in` 循环返回属性。对于直接在对象上定义的属性，默认值为 `true`；
  - [[Get]]: 在读取属性时调用的函数。默认值为 `undefined`；
  - [[Set]]: 在写入属性时调用的函数。默认值为 `undefined`。

  访问器属性不能直接定义，必须使用 `Object.defineProperty()` 来定义。 
  ```js
  var book = { 
    _year: 2004, // 下划线是一种常用的记号，用于表示只能通过对象方法访问的属性
    edition: 1 
  };
  Object.defineProperty(book, "year", { 
    get: function(){
      return this._year; 
    },
    set: function(newValue){
      if (newValue > 2004) {
        this._year = newValue; 
        this.edition += newValue - 2004;
      } 
    }
  });
  book.year = 2005; 
  alert(book.edition); //2
  ```
  只指定 `getter` 意味着属性是不能写，尝试写入属性会被忽略。 在严格模式下，尝试写入会抛出错误。只指定 `setter` 也不能读，在非严格模式下会返回 `undefined`，在严格模式下会抛出错误。
  
## 定义多个属性 <a id="multiple-properties"></a>

`Object.defineProperties()` 可以通过描述符一次定义多个属性。接收两个对象参数:第一个对象是要添加和修改其属性的对象，第二个对象的属性与第一个对象中要添加或修改的属性一一对应。
```js
var book = {};
Object.defineProperties(book, { 
  _year: { value: 2004 },
  edition: { value: 1 },
  year: {
    get: function(){
      return this._year; 
    },
    set: function(newValue){
      if (newValue > 2004) {
        this._year = newValue;
        this.edition += newValue - 2004; 
      }
    }
  }
}); 
```

## 读取属性的特性 <a id="reading-prop-attr"></a>

`Object.getOwnPropertyDescriptor()` 方法，可以取得给定属性的描述符。接收两个参数: 属性所在的对象和要读取其描述符的属性名称。返回值是一个对象，如果是访问器属性，这个对象的属性有 `configurable`、`enumerable`、`get` 和 `set`；如果是数据属性，这个对象的属性有 `configurable`、`enumerable`、`writable` 和 `value`。
```js
// Object.getOwnPropertyDescriptor()方法只能用于实例属性
var descriptor = Object.getOwnPropertyDescriptor(book, "_year");
// {value: 2004, writable: false, enumerable: false, configurable: false}
alert(typeof descriptor.get); //"undefined"

var descriptor = Object.getOwnPropertyDescriptor(book, "year"); 
// {enumerable: false, configurable: false, get: ƒ, set: ƒ}
alert(descriptor.value); //undefined 
alert(typeof descriptor.get); //"function"
```
在 JavaScript 中，可以针对任何对象——包括 `DOM` 和 `BOM` 对象，使用 `Object.getOwnPropertyDescriptor()` 方法。  
该方法只能用于实例属性，要取得原型属性的描述符，必须直接在[原型对象](../content/chapter06.md#prototype-pattern)上调用该方法。

```js
Object.getOwnPropertyDescriptor(Per.prototype, 'age')
// {value: 11, writable: true, enumerable: true, configurable: true}
```
更多关于对象方法，详见[第六章](../content/chapter06.md)


