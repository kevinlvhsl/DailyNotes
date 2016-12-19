## Vue相关note

### vue.js
### vuex
### vue-router
### vue-loader
### webpack + vue + vue-router
### ...

vue2.0 版本中
+ filter  只支持文字处理  不推荐数组 对象。。。 不要用内置的filter
+ broadcast  dispatch 不支持了
+ props 双向绑定不支持了  推荐用自定义组件实现v-model组件（子组件不应该知道有什么状态，父组件知道子组件存在） 
  子组件：入： props   出：$emit   触发如组件event
2.0 源码解读地址
[http://www.kancloud.cn/zmwtp/vue2/148822](http://www.kancloud.cn/zmwtp/vue2/148822)

有人写的一个vue的简版库 [https://github.com/qieguo2016/Vueuv](https://github.com/qieguo2016/Vueuv)
