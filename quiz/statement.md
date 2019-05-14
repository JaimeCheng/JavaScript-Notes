---
description: 流程控制语句相关练习
---

# 语句

1. 分别用if和switch语句实现学生考试成绩：低于60分不及格，60-80及格，80-90良好，90以上优秀。[run](https://jsbin.com/pepoye/edit?js,output) <br/>

2. 用循环打印  “九九乘法表”，包含for，while，do-while语句示例。[run](https://jsbin.com/qudeyox/edit?html,output)<br/>

3. 用循环打印三角形*号和倒三角星号（金字塔）。[run](https://jsbin.com/fuvecag/edit?js,output)<br/>

4. 毕达哥拉斯三元组，是一组三个正数，a小于b小于c，并且a平方加b平方等于c平方，现存在一组三元组，满足a加b加c等于1000，请写一个程序找到这组数并且输出。提示：考虑程序运行效率。[run](https://jsbin.com/zagutuw/edit?js,output)<br/>

5. 百鸡百钱问题，一只公鸡1文钱，一只母鸡2文钱，一只小鸡半文钱，需要买100只鸡， 正好花完，可以怎么买？有多少种买法？请用程序实现,用一百文钱买一百只鸡。[run](https://jsbin.com/jacayij/edit?js,output)<br/>

6. for-in语句示例。<br/>

   ```js
   var obj = {name:'czm', age: 18 };
   for (var key in obj) {
     console.log(key);  //以此输出 name，age
   }
   ```

7. with语句示例。<br/>

   ```js
   var qs = location.search.substring(1);
   var hostName = location.hostname;
   var url = location.href;
   
   // with 改写
   with(location){
     var qs = search.substring(1);
     var hostName = hostname;
     var url = href;
   }
   ```

8. 请解释continue与break关键字的作用，并结合label语句用他们写一个demo示例。[run](https://jsbin.com/jitipaz/edit?js,console)<br/>

   ```js
   var num_break = 0;
   outermost_break:
   for (var i=0; i < 10; i++) {
     for (var j=0; j < 10; j++) {
       if (i == 5 && j == 5) {
         break outermost_break;
       }
   		num_break++; 
     }
   }
   console.log(num_break);    
   
   var num_continue = 0;
   outermost_continue:
   for (var i=0; i < 10; i++) {
     for (var j=0; j < 10; j++) { 
       if (i == 5 && j == 5) { 
         continue outermost_continue;
    	  }
   		num_continue++; 
     }
   }
   console.log(num_continue);
   ```

   