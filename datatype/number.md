# Number

* 浮点计算的误差，永远不要测试某个特定的浮点数值
* 监测和监控极大或极小数值的必要性
* NaN的特殊性，isNaN\(\)
* Number\(null\)、Number\(undefined\)、Number\({}\)、Number\(\[\]\)、Number\(""\)，和parseInt\(\)的结果可能会不同，建议使用parseInt；parseInt\(\)应明确指定基数。parseInt\("10", 10\)解析十进制

