---
description: 函数相关练习，递归、闭包、作用域链...，题目持续补充，递归题目有点多因为本人递归太差了···
---

# 函数

1. 下列代码的运行结果？
   ```js
   (function (i) {
     document.write(i++);
     return arguments.callee;
   })(1)(2)(3)
   ```
   
2. 下列两段代码的运行结果？
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
   
4. 这段代码输出什么？如果想让这段代码输出0123456789，应该怎么修改？
   ```js
   for (var i = 0; i < 10; ++i) {
     setTimeout(function () {console.log(i)}, 0);
   }
   ```
   
5. 下列代码的运行结果？
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
   
6. 下列代码的运行结果？
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

7. 下列代码的结果是什么？为什么？
   ```js
   var a = 5;
   function a(b) {
     alert(b);
   }
   a(6);
   alert(a); 
   ```

8. 下列代码的输出结果？
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
   
9. 用递归函数计算 n! 。<br/>

10. 用递归函数求幂。<br/>

11. 用递归求1-100的和。<br/>

12. 求 1,3,5,7,9,...第n项的结果和前n项和,序号从0开始。<br/>

13. 求 2,4,6,8,10... 第n项与前n项之和。<br/>

14. Fibonacci数列(斐波那契数列) 1, 1, 2, 3, 5, 8, 13, 21, 34, 55... 第n项。<br/>

15. 数列 1,1,2,4,7,11,16...求第 n 项,求前n项和。<br/>

16. 什么是闭包？闭包的实现方式是,请举一个例子？<br/>

17. 使用递归输出以下结构（目录树）。
    ```js
    Desktop
    ├─.DS_Store
    ├─.localized
    ├─dir1
    |  ├─file3
    |  |  ├─file6
    ├─dir2
    |  ├─file4
    |  ├─file5
    ```
    
18. 猴子吃桃。第一天悟空吃掉桃子总数一半多一个，第二天又将剩下的桃子吃掉一半多一个，以后每天吃掉前一天剩下的一半多一个，到第n天准备吃的时候只剩下一个桃子。请算一下，桃子一共有多少个？ <br/>

19. 用递归函数实现深拷贝。<br/>

20. 使用递归实现 getElementsByClassName。<br/>

21. 经典楼梯问题：一共10级楼梯，每次可以走一步或两步，求一共多少种走法？<br/>

22. 细胞分裂问题：1个细胞，一个小时分裂一次，生命周期是3小时，求n小时后容器内，有多少细胞。<br/>

23. 实现常见的排序算法。<br/>

24. 下列代码的运行结果。
    ```js
    i = 1; 
    alert(i); 
    var A = function() { 
      alert(i); 
      var i = 2; 
      alert(i); 
    } 
    A(); 
    ```
25. 下列代码的运行结果。
    ```js
     var i = 1;
     function A(){
      i = 2;	
      function B(){
         var i = 3;
         console.log(i);
       }
       B();
       console.log(i);
     }
     A();
     console.log(i);
    ```
26. 下列代码的运行结果。
    ```js
    var b = 2008;
    function fnB(){
      alert(this.b);
      +function(){alert(this.b);}();
      function fnB1(){alert(this.b);}
      fnB1();
    }
    var oB = {};
    oB.b = 2011;
    oB.m = fnB;
    oB.m();
    // 函数中的子函数中的this默认指向window,在js中this没有传递性
    ```
27. 下列代码的输出结果。
    ```js
    var i = 2014;
    function fnA(fn){
      fn();
    }
    var o = {
      i:2008,
      fnB:function(){
          alert(this.i);
        },
      fnC:function(){
        this.fnB();		
        fnA(this.fnB);
      }		
    }
    o.fnC();
    // 作用域
    ```
28. 下列代码的输出结果。
    ```js
    var a = "全局的a";
    function obj() { 
      this.fn = function() { 
        alert(this.a); 
        setTimeout(this.fn, 1000);	 
      } 
    } 
    var o = new obj(); 
    o.a = "局部的a"
    o.fn(); 
    ```
29. 下列代码输出结果。
    ```js
    var i=2000;
    var oA = {
      i:2008,
      fnA:function(){	alert(this.i);	}
    }
    var oB = {	i:2010	}
    oA.fnA.call(oB);  	//输出？为什么？
    oA.fnA.call();  	//输出？为什么？
    oA.fnA();  		//输出？为什么？
    ```
30. 下列代码输出结果。
    ```js
    function A(a,b){	
      this.sum = a+b;	
    }
    function B(){	
      A.call(this,[2,3,4]);	
    }
    var b = new B();
    alert(b.sum);
    ```
31. 下列代码输出结果。
    ```js
    function A(){
      this.course = "PHP高级工程师班";
      this.school = "动力学院"	
    }
    function B(){	
      A.apply(this);	
    }
    var c = new B();
    alert(c.school);
    alert(c.course);
    ```
32. 下列代码输出结果。
    ```js
    function A(a,b){ 
      this.sum = a+b; 
    }
    function B(){ 
      A.apply(this,[2,3,4]); 
    }
    var b = new B();
    alert(b.sum);
    ```
33. 下列代码输出结果。
    ```js
    function A(arg){	
      this.sum = arg[0]+arg[1];	
    }
    function B(){	
      A.apply(this,[2,3,4]);	
    }
    var b = new B();
    alert(b.sum);
    ```