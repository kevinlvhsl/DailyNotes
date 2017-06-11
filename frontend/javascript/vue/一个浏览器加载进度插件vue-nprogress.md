### vue-progress
[vue-progressbar](https://github.com/hilongjw/vue-progressbar)
使用很简单，只需要use加载这个插件。
#### 安装

`npm install vue-progress`

#### 使用
```
import VueProgressBar from 'vue-progressbar'

Vue.use(VueProgressBar, {
  color: 'rgb(143, 255, 199)',
  failedColor: 'red',
  height: '2px'
})
```
> html

```
<template>
    <div id="app">
        <!-- for example router view -->
        <router-view></router-view>
        <!-- set progressbar -->
        <vue-progress-bar></vue-progress-bar>
    </div>
</template>
```

> script 
```
export default {
  methods:{
    start () {
        this.$Progress.start()
    },
    set (num) {
        this.$Progress.set(num)
    },
    increase (num) {
        this.$Progress.increase(num)
    },
    decrease (num) {
        this.$Progress.decrease(num)
    },
    finish () {
        this.$Progress.finish()
    },
    fail () {
        this.$Progress.fail()
    },
    test(){
      this.$Progress.start()

      this.$http.jsonp('http://api.rottentomatoes.com/api/public/v1.0/lists/movies/in_theaters.json?apikey=7waqfqbprs7pajbz28mqf6vz')
      .then((response) => {
          this.$Progress.finish()
      }, (response) => {
          this.$Progress.fail()
      })
    }
  }
}
```



#### [demo](http://hilongjw.github.io/vue-progressbar/index.html)

