## weex Syntax
--语法

### data-banding
> weex的数据绑定与vue类似，用双花括号引用数据。
```
<template>
  <container>
    <text style="font-size: {{size}}">{{title}}</text>
  </container>
</template>
<script>
  module.exports = {
    data: {
      size: 48,
      title: 'Alibaba Weex Team'
    }
  }
</script>
```
#### Computed Properties
> According to simple operations, in-template expressions are very convenient. But if you want to put more logic into the template, you should use a computed property.
```<template>
  <container style="flex-direction: row;">
    <text>{{fullName}}</text>
    <text onclick="changeName"></text>
  </container>
</template>
<script>
  module.exports = {
    data: {
      firstName: 'John',
      lastName: 'Smith'
    },
    computed: {
      fullName: {
        get: function() {
          return this.firstName + ' ' + this.lastName
        },

        set: function(v) {
          var s = v.split(' ')
          this.firstName = s[0]
          this.lastName = s[1]
        }
      }
    },
    methods: {
      changeName: function() {
        this.fullName = 'Terry King'
      }
    }
  }
</script>
```
> weex在computed中增加了set方法，允许计算属性被写入设置

+ 样式中也是可以直接写入变量值的
```<template>
  <text style="font-size: {{size}}; color: {{color}}; ...">...</text>
</template>
```
+ 事件
```
<template>
  <text onclick="toggle">Toggle</text>
</template>
```
+ if
`<image src="..." if="{{shown}}"></image>`


### Style & Class
> 语法就是普通的css 或者绑定数据的类或属性

### Events
--事件绑定

以on开头，后面+事件名称
```
<template>
  <image onclick="handler('arg1', $event)" ...></image>
</template>
<script>
  module.exports = {
    methods: {
      handler: function (arg1, e) {
        // TODO
      }
    }
  }
</script>
```
> Event Object
  When an event handler called, it will receive an event object as the first argument. Every event object will contains following properties.
  type: event name, eg: click
  target: target Element of the event
  timestamp: time stamp that event triggered

























