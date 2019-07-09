---
description: 操作符相关练习，操作符特殊规则和运算优先级
---

# 操作符

1. 下列代码输出结果?
   ```js
   var a = 0,b=0;
   b =  a++ + (a++ + 2), b, a = b++ ;
   console.log(a);
   console.log(b);
   ```

2. 理解模与模运算符特点，a和b的结果分别是多少?
   ```js
   var a = 17 % 12; 
   var b = -17 % -12; 
   console.log(a);
   console.log(b);
   ```
3. 下列代码的输出结果?

   ```js
   var a = 2+3;
   console.log(a++);
   console.log(++a);
   console.log(a--);
   console.log(--a);
   ```
4. 下列代码的输出结果?

   ```js
   var a = 3;
   var b = 5;
   var res = b - a != a && !b;
   console.log(res);
   ```
5. 下列代码的输出结果?

   ```js
   var a = 3;
   var b = 5;
   var res = a > b - a && ! b - a || a ? "true" : "false";
   console.log(res);
   ```

[TIY·试一试](https://jsbin.com/?js,console)

