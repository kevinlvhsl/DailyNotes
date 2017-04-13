## js笔试常见-算法题
-----
参考了[https://segmentfault.com/a/1190000008593715](https://segmentfault.com/a/1190000008593715)

### 如何将浮点数点左边的数每三位添加一个逗号，如12000000.11转化为『12,000,000.11』?
```
  function commafy(num){
  	return num && num
  		.toString()
  		.replace(/(\d)(?=(\d{3})+\.)/g, function($1, $2){
  			return $2 + ',';
  		});
  }
```

### 浅拷贝 和 深拷贝
**浅拷贝仅适用于基本数据类型拷贝，引用类型拷贝属于引用拷贝，会与源对象共用**
```
// 浅拷贝      
function extendCopy(p) {
　　　　var c = {};
　　　　for (var i in p) { 
　　　　　　c[i] = p[i];
　　　　}
　　　　c.uber = p;
　　　　return c;
　　}
  
  // 深拷贝
function deepCopy(p, c) {
　　　　var c = c || {};
　　　　for (var i in p) {
　　　　　　if (typeof p[i] === 'object') {
　　　　　　　　c[i] = (p[i].constructor === Array) ? [] : {};
　　　　　　　　deepCopy(p[i], c[i]);
　　　　　　} else {
　　　　　　　　　c[i] = p[i];
　　　　　　}
　　　　}
　　　　return c;
　　}
```


### 判断回文字符串

+ 方法一(数组倒序后比较)
```
const isPalindromic = str => str === str.split('').reverse().join('')
```

+ 方法二(用数组遍历，找到中间下标，从中间到两边扩散逐个比较，如果全等则返回true)
> 优点 只需要遍历数组的一半长度即可，找到不同的，立即返回不浪费
```
const isPalindromic = (str) => {
  const len = str.length
  let start = Math.ceil( len / 2 )
  while (start < len) {
    if (str[start] !== str[ len - start - 1 ]) return false
    start ++
  }
  return true
}
```
------------

### 数组去重
+ 方法一 利用对象的无重复属性去重
```
const uniqueES5 = (arr) => {
    var cache = {};
    return arr.filter((item) => {
        return cache[item] ? false : (cache[item] = true);
    });
};
```

+ 方法二 利用ES6中Set无重复的特性
```
const uniqueES6 = (arr) => Array.from(new Set(arr));

let b = uniqueES6([1,2,3,4,5,23,2,3,4,1,2,2,3,34,'1', '3'])   // => [1, 2, 3, 4, 5, 23, 34, "1", "3"]
```

+ 方法三 利用排序
```
Array.prototype.sortUnique = function () {
  var temp = []
  this.sort()
  for(i = 0; i < this.length; i++) {
    if( this[i] === this[i+1]) {
      continue
    }
    temp[temp.length]=this[i]
  }
  return temp
}
```
+ 方法四 利用filter
```
var unique = function (keywords) {
 return keywords.filter((keyword, index) => keywords.lastIndexOf(keyword) === index)
}
// [1, 34, 6, 3, "df", "1", "6", 1, 6] => [34, 3, "df", "1", "6", 1, 6]
```
> 如果还需要排序， 只需要在filter后面再加sort方法 
`.sort((a, b) => a < b ? -1 : 1)`
-------------------------

### 统计一个字符串出现最多的字母
+ 普通的计数方式
```
var findMaxDuplicateCharNormal (str) {
  if (str.length === 1) return str
  var charObj = {}
  for (var i =0; i<str.length; i++) {
    if (charObj[i]) charObj[i] += 1
    else charObj[i] = 1
  }
  var max = 1
  var maxChar = ''
  for (var k in charObj) {
    if (charObj[k] > max) {
      maxChar = k
      max = charObj[k]
    }
  }
  return maxChar
}
```
+ 用正则的黑科技(不太懂)

```
const findMaxDuplicateCharRegex = (chars) => {
    // 先对字符进行排序
    chars = chars.split('').sort().join('');
    // 获取相同字符序列
    let regex = /(.)(\1)+/g;
    let temp = null;
    let max = 0;
    let char = '';
    while (temp = regex.exec(chars)) {
        if (temp[0].length > max) {
            char = temp[1];
            max = temp[0].length;
        }
    }
    return char;
};
```
---------------------
### 阶乘
+ 倒序遍历相乘

```
function factorialize(num) {
  var result = 1
  if(num < 0) return -1
  if(num == 0 || num == 1) return 1
  while(num>1) {
    result *= num--
  }
  return result
}
```
+ 递归实现
```
function jie(num) {
  var result = 1;
  if(num < 0) return -1;
  if(num == 0 || num == 1) return 1;
  if(num > 1) return num*jie(num-1);
}
// 尾递归
function factorial(n, total = 1) {
  if (n === 1) return total;
  return factorial(n - 1, n * total);
}
```
-----

### 生成斐波拉契数列（数组）
> 利用数组特性，
```
function getFibonacci(n) {
  if ( Number.isNaN(n) || n < 0 || !Number.isInteger(n)) throw new Error('请输入正整数')
  var fibarr = [];
  var i = 0;
  while(i < n) {
    if(i <= 1) {
      fibarr.push(i);
    } else {
      fibarr.push(fibarr[i - 1] + fibarr[i - 2])
    }
    i++;
  }
  return fibarr;
}
```

------
### 不借助临时变量，进行两个整数的交换

`let a = 1,let b = 2;`
+ 方法一 简单的加减法(针对数字）
```
// 加减法
a = a - b;
b = b + a;
a = b - a;
```
+ ES6解构赋值

```
[a, b] = [b, a];
```

 + 异或运算
 ```
 // 异或(不太懂)
a = a ^ b;
b = a ^ b;
a = b ^ a;
 ```


### 正数组的最大差值


`let array = [10,5,11,7,8,9];`
```
getMaxGap = (array) => Math.max.apply(Math, array) - Math.min.apply(Math, array)
//或者
getMaxGap = (array) => Math.max(...array) - Math.min(...array)
```
+ 使用reduce方法
```
const getMaxDiff = (array) => {
    if (array.length < 1) return arrary[0];
    array = array.reduce(([max, min], el) => {
       max = el > max ? el : max;
       min = el < min ? el : min;
       return [max, min];
    }, array);
    return array[0] - array[1];
};

```

+ 用普通的遍历求得最大和最小值（最快）
```
function getMaxGap(arr) {
    var min = arr[0];
    var maxGap = 0;// 最大差值
    for (var i = 0; i < arr.length; i++) {
        var current = arr[i];
        min = Math.min(min, current);
        var gap = current - min;  // 当前差值
        maxGap = Math.max(maxGap, gap);
    }
    return maxGap;
}
```

### 排序算法

#### [CANVAS演示排序算法过程](http://math.hws.edu/eck/jsdemo/sortlab.html)

+ 冒泡
> 大数向后面冒 中间比较的时候 [大于号]就是大数向后冒小->大 顺序， [小于号]就是小数向后冒 大-> 小 倒序
```
function bubbleSort(arr) {
    for (var i = 0; i < arr.length - 1; i++) {
        for (var j = i+1; j < arr.length; j++) {
            var temp;
            if (arr[i] > arr[j]) {
                // temp = arr[i];
                // arr[i] = arr[j]
                // arr[j] = temp
                [arr[i], arr[j]] = [arr[j], arr[i]]
            }
        }
        console.log(arr)
    }
    return arr
}
```

+ 快速排序算法
> 随机选一第一个数作为中间比较值， 小的放左边，大的放右边， 然后递归对左右两边的分别排序，最后用数组连接方法concat合并起来
```
function quickSort(arr) {

    if(arr.length<=1) {
        return arr;
    }

    let leftArr = [];
    let rightArr = [];
    let q = arr[0];
    for(let i = 1,l=arr.length; i<l; i++) {
        if(arr[i]>q) {
            rightArr.push(arr[i]);
        }else{
            leftArr.push(arr[i]);
        }
    }

    return [].concat(quickSort(leftArr),[q],quickSort(rightArr));
}

```

### 随机生成指定长度的字符串

+ 利用random生成26个字母和10个数字里的一个下标
```
function randomString(n) {
  let str = 'abcdefghijklmnopqrstuvwxyz9876543210';
  let tmp = '',
      i = 0,
      l = str.length;
  for (i = 0; i < n; i++) {
    tmp += str.charAt(Math.floor(Math.random() * l));
  }
  return tmp;
}

```

### 实现类似getElementsByClassName 的功能
> 自己实现一个函数，查找某个DOM节点下面的包含某个class的所有DOM节点？不允许使用原生提供的 getElementsByClassName querySelectorAll 等原生提供DOM查找函数。
> 遍历所有节点，利用正则匹配包含该class的节点
```
function queryClassName(node, name) {
  var starts = '(^|[ \n\r\t\f])',
       ends = '([ \n\r\t\f]|$)';
  var array = [],
        regex = new RegExp(starts + name + ends),
        elements = node.getElementsByTagName("*"),
        length = elements.length,
        i = 0,
        element;

    while (i < length) {
        element = elements[i];
        if (regex.test(element.className)) {
            array.push(element);
        }

        i += 1;
    }

    return array;
}
```

### 过滤敏感词
> 利用正则匹配
```
/**
 * 过滤敏感词
 * @param String content 要过滤的内容
 * @param  Array dirtyDict 敏感词库数组
 * @param String replaceChar 替换成什么字符，默认为*
 * @return replaced content
 */
 function filter (content, dirtyDict, char='*') {
 if (!dirtyDict instanceof Array || dirtyDict.length === 0) return content
  dirtyDict.forEach((item) => {
    content = content.replace(new RegExp('(' +item+')', 'ig'), char)
  })
  return content
}
```

### 原型继承
```
function Person(p_name,p_age){
    this.name=p_name;
    this.age=p_age;
    this.speak=function(){
        alert(this.name+this.age);
    }
}
function Student(p_no){
    this.no=p_no;
    this.say=function(){
        alert(this.name+this.age+this.no);
    }
}
Student.prototype = new Person('wangwu',21);
Student.prototype.constructor = Student
var stu = new Student(10);
stu.speak();
stu.say();
```









































