---
description: 函数相关练习，递归、闭包、作用域链...，题目持续补充
---

# 函数

1. 下列代码的运行结果？
   ```js
   (function (i) {
     document.write(i++);
     return arguments.callee;
   })(1)(2)(3)
   ```
2. 下列代码的运行结果？
   ```js
   var i=1;
   function A(){
     alert(i);
     var i = 3;
   }	
   A();
   alert(i);
   ```
3. 请使用一条语句对数组求和,要求使用递归。
   ```js
   var arr = [1,2,3,4,5];
   function sum(args){	
     //请在这里填上一条语句，完成对数组求和，要求使用递归。
   }
   sum(arr); 
   ```
4. 用递归函数计算 n! 。<br/>
5. 什么是闭包？闭包的实现方式是,请举一个例子？<br/>

