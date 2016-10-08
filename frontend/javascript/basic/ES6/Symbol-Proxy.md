### Symbol 和 Proxy也是一个新的属性
var f1 = Symbol('foo');
var f2 = Symbol('foo');
f1 === f2   // false
这样定义的两个变量是不相同的。  因为Symbol会产生一个不重复的symbol对象。  
在浏览器的控制台里面查看， 只会显示'Symbol(foo)'的字符串，但是两个确实是不同的。

var s1 = Symbol.for('foo');
var s2 = Symbol.for('foo');
s1 === s2  // true
这种方法 两个变量是相同的， 这样定义的变量可以在整个全局范围内共一份， 但是不能刷新浏览器。

```
var arr = [1,2,3,4]
var obj = new Proxy(arr, {
  get: function (target, key, receiver) {
    console.log(`getting ${key}!`);
    return Reflect.get(target, key, receiver);
  },
  set: function (target, key, value, receiver) {
    console.log(`setting ${key}!`);
    return Reflect.set(target, key, value, receiver);
  }
});
接下来访问obj的属性，就会进入代理的handler方法中了。
```
