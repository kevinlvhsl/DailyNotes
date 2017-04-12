## 20个JS优化代码技巧

1.Insert item inside an Array（向数组中插入元素）
```
var arr = [1,2,3,4,5];
//old method
arr.push(6);
//new method 快43%
arr[arr.length] = 6;
   
var arr = [1,2,3,4,5];
//old method
arr.unshift(0);
//new method 快98%
[0].concat(arr);
 ```

3.Sorting strings with accented characters（排列含音节字母的字符串）
> Javascript有一个原生方法sort可以排列数组。一次简单的 array.sort() 将每一个数组元素视为字符串并按照字母表排列。
但是当你试图整理一个非ASCII元素的数组时，你可能会得到一个奇怪的结果
**Intl.Collator().compare**
```
 ['único','árbol', 'cosas', 'fútbol'].sort(Intl.Collator().compare);
14      // ["árbol", "cosas", "fútbol", "único"]
15  
16      ['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(Intl.Collator().compare);
17      // ["Wann", "wäre", "Woche", "wöchentlich"]
```











































