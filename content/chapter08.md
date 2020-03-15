# 8. BOM

## window对象 <a id="window-object"></a>

全局变量会成为 `window` 对象的属性，但是定全局变量与在 `window` 对象上直接定义属性的差别：全局变量不能通过 `delete` 操作符删除，而直接在 window 对象上的定义的属性可以。 
```js
var age = 29; 
window.color = "red";
//在IE < 9 时抛出错误，在其他所有浏览器中都返回false 
delete window.age;
//在IE < 9 时抛出错误，在其他所有浏览器中都返回true 
delete window.color; //returns true
alert(window.age); //29
alert(window.color); //undefined
```
* **窗口位置**
  下列代码可以跨浏览器取得窗口左边和上边的位置：
  ```js
  var leftPos = (typeof window.screenLeft == "number") ? window.screenLeft : window.screenX;
var topPos = (typeof window.screenTop == "number") ? window.screenTop : window.screenY;
  ```
  但不同浏览器的坐标起点不同，无法在跨浏览器的条件下取得窗口左边和上边的精确坐标值。

