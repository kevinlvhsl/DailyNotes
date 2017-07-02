### javascript 着重基础的笔试题
```
foo: for (var i=0; i<4; i++) {
  for(var j=0; j<4; j++){
    if ( i == j) {
      continue foo;
    }
    if ((i * j) % 2 == 1) {
      continue
    }
    
    console.log(i, j)
  }
}

```
输出： // 1 0    // 2 0   // 2 1    // 3 0    // 3 2
> 考察点：
  for循环 continue 功能， 和foo作为for的标签。  
  continue如果指定了foo 是直接跳出当前循环，到指定标签的下一轮循环 没指定的话， 就是跳过当前循环的当前值，执行当前循环的下一轮值。

```
foo: for (var i=0; i<4; i++) {
  for(var j=0; j<4; j++){
    if ((i * j) >= 3) {
      console.log('stoping', i, j)
      break foo;
    }
    console.log(i, j)
  }
}
```
输出： // 0 0   // 0 1   // 0 2  // 0 3    // 1 1   // 1 2    //  stoping 1 3
break 和标签一期使用，则可以实现从内层循环跳转到外层循环。  如果break后面没有标签， 则只是跳出当前循环继续下一循环。和 continue foo 效果相同
break 不是跳转到标签所在位置继续执行，而是 “跳出标签 foo 所在循环/代码块” 继续执行后面的代码。 
