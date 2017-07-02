### javascript 着重基础的笔试题
```
for: for (var i=0; i<4; i++) {
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
输出： 1 0     2 0   2 1    3 0    3 2
考察for循环 continue 功能， 和foo作为for的标签。  continue如果指定了foo 是直接跳出当前循环，到指定标签的循环 没指定的话， 就是跳过当前循环的当前值。
```
