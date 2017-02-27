##  一个饿了么的UI库 
---

[http://element.eleme.io/#/](http://element.eleme.io/#/)
> 覆盖了开发后台管理系统所需的各种组件。

好用的几个介绍一下：
### 评分：可以自定义颜色 和icon 还可以定义分数所对应的文字 真心点赞
```
<div class="block">
  <span class="demonstration">区分颜色</span>
  <el-rate
    v-model="value2"
    :colors="['#99A9BF', '#F7BA2A', '#FF9900']">
  </el-rate>
</div>
```
#### Attributes
参数	说明	类型	可选值	默认值
max	最大分值	number	—	5
disabled	是否为只读	boolean	—	false
allow-half	是否允许半选	boolean	—	false
low-threshold	低分和中等分数的界限值，值本身被划分在低分中	number	—	2
high-threshold	高分和中等分数的界限值，值本身被划分在高分中	number	—	4
colors	icon 的颜色数组，共有 3 个元素，为 3 个分段所对应的颜色	array	—	['#F7BA2A', '#F7BA2A', '#F7BA2A']
void-color	未选中 icon 的颜色	string	—	#C6D1DE
disabled-void-color	只读时未选中 icon 的颜色	string	—	#EFF2F7
icon-classes	icon 的类名数组，共有 3 个元素，为 3 个分段所对应的类名	array	—	['el-icon-star-on', 'el-icon-star-on','el-icon-star-on']
void-icon-class	未选中 icon 的类名	string	—	el-icon-star-off
disabled-void-icon-class	只读时未选中 icon 的类名	string	—	el-icon-star-on
show-text	是否显示辅助文字	boolean	—	false
text-color	辅助文字的颜色	string	—	1F2D3D
texts	辅助文字数组	array	—	['极差', '失望', '一般', '满意', '惊喜']
text-template	只读时的辅助文字模板	string	—	{value}


### 走马灯[轮播图](http://element.eleme.io/#/zh-CN/component/carousel)
> 可以定义是否自动，是否显示箭头和园点
```
<template>
  <el-carousel :interval="4000" type="card" height="200px">
    <el-carousel-item v-for="item in 6">
      <h3>{{ item }}</h3>
    </el-carousel-item>
  </el-carousel>
</template>
```
#### Carousel Attributes

|参数	|说明	|类型|	可选值|	默认值|
=========================================================
height	走马灯的高度	number	—	300
initial-index	初始状态激活的幻灯片的索引，从 0 开始	number	—	0
trigger	指示器的触发方式	string	click	—
autoplay	是否自动切换	boolean	—	true
interval	自动切换的时间间隔，单位为毫秒	number	—	3000
indicator-position	指示器的位置	string	outside/none	—
arrow	切换箭头的显示时机	string	always/hover/never	hover
type	走马灯的类型	string	card	—

事件名称	说明	回调参数
change	幻灯片切换时触发	目前激活的幻灯片的索引，原幻灯片的索引


### 文件上传 [详细](http://element.eleme.io/#/zh-CN/component/upload)
> 要自己写一个文件上传有时候真是麻烦
  这里可以自定义预览、文件名、限制大小、
```
<el-upload
  class="upload-demo"
  action="//jsonplaceholder.typicode.com/posts/"
  :on-change="handleChange"
  :file-list="fileList3">
  <el-button size="small" type="primary">点击上传</el-button>
  <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
</el-upload>
<script>
  export default {
    data() {
      return {
        fileList3: [{
          name: 'food.jpeg',
          url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100',
          status: 'finished'
        }, {
          name: 'food2.jpeg',
          url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100',
          status: 'finished'
        }]
      };
    },
    methods: {
      handleChange(file, fileList) {
        this.fileList3 = fileList.slice(-3);
      }
    }
  }
</script>
```

### loading [详细](http://element.eleme.io/#/zh-CN/component/loading)
> 中开发中几乎所有的项目都会用到loading， 给用户以更好的提示，
  这里的loading很灵活，可以局部也可以全局，可以自动消失也可以手动消失
 
 ```
 <template>
  <el-table
    v-loading.body="loading"
    :data="tableData"
    style="width: 100%">
    <el-table-column
      prop="date"
      label="日期"
      width="180">
    </el-table-column>
    <el-table-column
      prop="name"
      label="姓名"
      width="180">
    </el-table-column>
    <el-table-column
      prop="address"
      label="地址">
    </el-table-column>
  </el-table>
</template>

<style>
  body {
    margin: 0;
  }
</style>

<script>
  export default {
    data() {
      return {
        tableData: [{
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }],
        loading: true
      };
    }
  };
</script>
 ```

### 级联选择器[cascader](http://element.eleme.io/#/zh-CN/component/cascader)

> 真是太有用了，完美解决省市县多级选择

#### Attributes
参数	说明	类型	可选值	默认值
options	可选项数据源，键名可通过 props 属性配置	array	—	—
props	配置选项，具体见下表	object	—	—
value	选中项绑定值	array	—	—
popper-class	自定义浮层类名	string	—	—
placeholder	输入框占位文本	string	—	请选择
disabled	是否禁用	boolean	—	false
clearable	是否支持清空选项	boolean	—	false
expand-trigger	次级菜单的展开方式	string	click / hover	click
show-all-levels	输入框中是否显示选中值的完整路径	boolean	—	true
filterable	是否可搜索选项	boolean	—	—
debounce	搜索关键词输入的去抖延迟，毫秒	number	—	300
change-on-select	是否允许选择任意一级的选项	boolean	—	false
size	尺寸	string	large / small / mini	—
¶ props

参数	说明	类型	可选值	默认值
value	指定选项的值为选项对象的某个属性值	string	—	—
label	指定选项标签为选项对象的某个属性值	string	—	—
children	指定选项的子选项为选项对象的某个属性值	string	—	—
disabled	指定选项的禁用为选项对象的某个属性值	string	—	—
¶ Events

事件名称	说明	回调参数
change	当绑定值变化时触发的事件	当前值
active-item-change	当父级选项变化时触发的事件，仅在 change-on-select 为 false 时可用	各父级选项组成的数组

### 日期时间选择器票[DateTimePicker](http://element.eleme.io/#/zh-CN/component/datetime-picker)

> 这个组件真的是管理后台的最爱了，几乎所有的管理后台都会用到日期时间选择。

```
<template>
  <div class="block">
    <span class="demonstration">默认</span>
    <el-date-picker
      v-model="value3"
      type="datetimerange"
      placeholder="选择时间范围">
    </el-date-picker>
  </div>
  <div class="block">
    <span class="demonstration">带快捷选项</span>
    <el-date-picker
      v-model="value4"
      type="datetimerange"
      :picker-options="pickerOptions2"
      placeholder="选择时间范围"
      align="right">
    </el-date-picker>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        pickerOptions2: {
          shortcuts: [{
            text: '最近一周',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit('pick', [start, end]);
            }
          }, {
            text: '最近一个月',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
              picker.$emit('pick', [start, end]);
            }
          }, {
            text: '最近三个月',
            onClick(picker) {
              const end = new Date();
              const start = new Date();
              start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
              picker.$emit('pick', [start, end]);
            }
          }]
        },
        value3: [new Date(2000, 10, 10, 10, 10), new Date(2000, 10, 11, 10, 10)],
        value4: ''
      };
    }
  };
</script>
```

--- 好用的组件太多了， 我就不一一列举了






