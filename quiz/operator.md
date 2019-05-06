---
操作符相关练习，操作符特殊规则和运算优先级
---

1. 下列代码输出结果?

   ```js
   var a = 0,b=0;
   b =  a++ + (a++ + 2), b, a = b++ ;
   document.writeln(b);
   document.writeln(a);
   ```


2. 理解模与模运算符特点，a和b的结果分别是多少?
   ```js
   var a = 17 % 12; 
   var b = -17 % -12; 
   ```
3. 下列代码的输出结果?

   ```js
   var a = 2+3;
   document.write(a++);
   document.write(++a);
   document.write(a--);
   document.write(--a);
   ```
4. 下列代码的输出结果?

   ```js
   var a = 3;
   var b = 5;
   var res = b - a != a && !b;
   ```
5. 下列代码的输出结果?

   ```js
   var a = 3;
   var b = 5;
   var res = a > b - a && ! b - a || a ? "true" : "false";
   ```

