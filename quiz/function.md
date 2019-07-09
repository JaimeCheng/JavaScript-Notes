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
   var i = 1;
   function A(){
     alert(i);
     var i = 3;
     alert(i);
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
6. 这段代码输出什么？如果想让这段代码输出0123456789，应该怎么修改？
   ```js
   for (var i = 0; i < 10; ++i) {
     setTimeout(function () {console.log(i)}, 0);
   }
   ```
7. 使用递归输出以下结构。
   ```js
   A
   -A1
   --A11
   ---A111
   ----A1111
   ```
8. 猴子吃桃。第一天悟空吃掉桃子总数一半多一个，第二天又将剩下的桃子吃掉一半多一个，以后每天吃掉前一天剩下的一半多一个，到第n天准备吃的时候只剩下一个桃子。请算一下，桃子一共有多少个？ <br/>
9. 下列代码的运行结果？
   ```js
   var n = 3;
   function A() {
     var n = 1;
     B = function () {
       n = n + 1
     }
     function C() {
       alert(n);
     }
     return C;
   }
   var D = A();
   D(); 		//结果是什么，为什么？
   B();
   D(); 		//结果是什么，为什么？
   ```

10. 下列代码的运行结果？
    ```js
    var a =5;
    function F(){
      a = 10;
      return;
      function a(){}
    }
    F();
    alert(a);
    ```

11. 下列代码的结果是什么？为什么？
    ```js
    var a = 5;
    function a(b) {
      alert(b);
    }
    a(6);
    alert(a); 
    ```
12. 下列代码的输出结果？
    ```js
    function A(){
      var rs = new Array();
      for(var i=0;i<3;i++){
        rs[i] =  function(){ return i;}  ;
      }
      return rs;
    }
    var rst = A()
    document.write(rst[0]());
    document.write(rst[1]());
    document.write(rst[2]());
    document.write(rst[3]());	
    ```

