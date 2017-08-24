##immutableJS一些API
---


+ 原生js转换为immutableData
```
Immutable.fromJS([1,2]) // immutable的 list

Immutable.fromJS({a: 1}) // immutable的 map

从immutableData 回到 JavaScript 对象

immutableData.toJS()
```

+ 判断两个immutable数据是否一致

`Immutable.is(immutableA, immutableB)`


+ 判断是不是map或List

`Immutable.Map.isMap(x)`

`Immutable.Map.isList(x)`


+ 对象合并(注意是同个类型)

`immutableMaB = immutableMapA.merge(immutableMaC)`


+ Map的增删查改

> 查

```
immutableData.get('a') // {a:1} 得到1。

immutableData.getIn(['a', 'b']) // {a:{b:2}} 得到2。访问深层次的key
```

> 增和改(注意不会改变原来的值，返回新的值)

```
immutableData.set('a', 2) // {a:1} 得到1。

immutableData.setIn(['a', 'b'], 3)

immutableData.update('a',function(x){return x+1})

immutableData.updateIn(['a', 'b'],function(x){return x+1})
```

> 删

```
immutableData.delete('a')

immutableData.deleteIn(['a', 'b'])


+ List的增删查改

如同Map，不过参数变为数字索引。

比如immutableList.set(1, 2)

其它便捷函数

如同underscore的方法，都有噢。

参考
http://facebook.github.io/immutable-js/docs/#/
https://segmentfault.com/a/1190000002909224
