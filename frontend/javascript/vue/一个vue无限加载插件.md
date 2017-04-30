## vue-infinite-loading
见源码： [https://github.com/PeachScript/vue-infinite-loading](https://github.com/PeachScript/vue-infinite-loading)

> 滑到底部就触发on-finite事件
> 加载图标可以选（spinner） 波浪点：waveDots、螺旋：spiral、圆圈：circles、泡泡:bubbles、默认

### props属性
+ distance 目标条数
+ onInfinite 加载方法
+ spinner 加载小图标动画
+ direction 加载方向  上拉还是下拉  默认下拉加载更多(bottom)
```
   props: {
      distance: {
        type: Number,
        default: 100,
      },
      onInfinite: Function,
      spinner: String,
      direction: {
        type: String,
        default: 'bottom',
      },
    },
  ```
  
### 事件
+ 加载回来了： $InfiniteLoading:loaded
+ 全部加载完成： $InfiniteLoading:complete
+ 重置（清空列表重来）： $InfiniteLoading:reset
+ 没有跟多了显示最后的提示文字`<span slot="no-more">这里是自定义的提示文字</span>`

