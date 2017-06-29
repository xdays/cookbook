# [W3school JavaScript](https://www.w3schools.com/js/)

* null 的类型为 object 可以认为是JS的bug
* null 和 undefined 是值相同但是类型不相同
* 避免使用 String, Number, 和 Boolean 对象, 对性能有影响
* 除非有意为之，否则不要创建全局变量
* javascript的数组不能用数字之外的对象作为key, 否则数组就会变成标准的对象，一些数组的对象就有问题了
* 因为数组用typeof识别出来是Object，所以可以通过如下三种方式识别:
```
# 1
Array.isArray(x);

#2
function isArray() {
    return x.constructor.toString().indexOf('Array') > -1;
}

#3
x instanceof Array
```
