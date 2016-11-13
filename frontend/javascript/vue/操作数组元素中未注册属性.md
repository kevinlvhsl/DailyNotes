## 今天再一次深刻体会到vue下的数组跟新其中的某个元素的属性， 一定要把这个属性先注册到元素上。
比如
```
<template>
item(v-for="li in list")
  .had-changed(:class="{hadc : !!li.c}")
  .change-btn(@click="change($index)")
<template>
data: () {
  return {
    list: [
      {a: 1, b: 2},
      {a: 2, b: 4},
    ]
  }
}
methods: {
  change (index) {
     list[index].c = '我是新增的属性'
  }
}
```
在这个时候， 如果你页面上有一个列表循环， 其中有依赖该item的一个c属性, 你如果点击了某个按钮
去改变这个li的c属性，使得!!li.c为真 而添加上hadc类， 这个时候，你应该是会失败。 得不到你想要的效果。
这时候就应该想办法在list还没有注册到data上的时候， 将c属性添加到里面的元素上去。

已经吃过多次这个亏了， 所以今天长点记性来记录一下
