## js笔试常见-算法题
-----

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
    if (str[start] !=== str[ len - start - 1 ]) return false
    start ++
  }
  return true
}
```


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
