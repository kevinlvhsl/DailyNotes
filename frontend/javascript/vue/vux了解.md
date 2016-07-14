### 网上有的团队针对：用vue在微信上开发的应用 开发了一套风格接近微信的UI

源码地址： [https://github.com/airyland/vux](https://github.com/airyland/vux)
文档源码:  [https://github.com/vuxjs/vux-doc](https://github.com/vuxjs/vux-doc)
文档地址： [https://vuxjs.gitbooks.io/vux/content/](https://vuxjs.gitbooks.io/vux/content/)

还有人写了demo [https://github.com/aha2mao/vux_demo](https://github.com/aha2mao/vux_demo)

```
<template>
    <div id="app"  style="width: 100%">
        <div   style="width: 100%; text-align: center"> 
                <img class="logo" src="./assets/logo.png">
        </div>
            <hello></hello>
            <p>
                Welcome to your Vue.js app!
            </p>
        
        <div  style="width: 100%">
            <div>
                <group>
                    <cell title="vue" value="cool">111</cell>
                </group>
            </div>
        </div>
        <div style="width: 100%">
            <tab>
                <tab-item :selected="demo1 === '1'", @click="demo1='1'">已发货</tab-item>
                <tab-item :selected="demo1 === '2'", @click="demo1='2'">未发货</tab-item>
                <tab-item :selected="demo1 === '3'", @click="demo1='3'">全部订单</tab-item>
        </tab>
        </div>
        <div style="width: 100%">
            <group>
                <radio :options="options" value="中国" fill-mode fill-label="Other" fill-placeholder="填写其他的哦"></radio>
            </group>
        </div>
        <div style="width: 100%">
            <group>
                <group>
                    <switch :title="'双向绑定:值为' + value1", :value.sync="value1"></switch>
                    <switch :title="'双向绑定:值为' + value2", :value.sync="value2"></switch>
                </group>
            </group>
        </div>
        <div>
            <group :title="'no placeholder, the current value is : ' + defaultValue">
                <selector title="省份" :options="list" :value.sync="defaultValue"></selector>
            </group>
            <group title="with placeholder">
                <selector placeholder="请选择省份" title="省份" :options="list" @on-change="onChange"></selector>
            </group>
            <group title="without title">
                <selector placeholder="请选择省份" :options="list"></selector>
            </group>
            <group title="use plain options">
                <selector value="C" title="Selector" :options="list1" @on-change="onChange2"></selector>
            </group>
            <group title='multi selector'>
                <selector placeholder="请选择省份" title="省份" :options="list"></selector>
                <selector :value.sync="values2" title="省份" :options="list"></selector>
            </group>
        </div>
        <div>
            <group>
                <inline-calendar start-date="2016-06-04" end-date="2017-06-18"></inline-calendar>
                <!-- <calendar :value.sync="cvalue"  start-date="2016-06-04" end-date="2017-06-18" title="Date Picker"></calendar> -->
            </group>
        </div>
    <!-- 滚动列表组件。带下拉刷新。。。 -->
        <scroller lock-x :scrollbar-y="false" style="height: 200px" use-pulldown >
            <div class="box1">
                <group>
                    <cell title="vue" value="cool">111</cell>
                </group>
                <group>
                    <cell title="vue" value="cool">222</cell>
                </group>
                <group>
                    <cell title="vue" value="cool">333</cell>
                </group>
                <group>
                    <cell title="vue" value="cool">444</cell>
                </group>
                <group>
                    <cell title="vue" value="cool">555</cell>
                </group>
                <group>
                    <cell title="vue" value="cool">666</cell>
                </group>
                <group>
                    <cell title="vue" value="cool">777</cell>
                </group>
                <group>
                    <cell title="vue" value="cool">888</cell>
                </group>
                <group>
                    <cell title="vue" value="cool">999</cell>
                </group>
                <group>
                    <cell title="vue" value="cool">101010</cell>
                </group>
            </div>
        </scroller>


    </div>
</template>

<script>
import Hello from './components/Hello'
// import {ButtonTab} from 'vux'
// import { Group, Cell } from 'vux'
// 推荐的方式，按需加载需要的组件
import Group from 'vux/dist/components/group'
import Cell from 'vux/dist/components/cell'
import Tab from 'vux/dist/components/tab'
import TabItem from 'vux/dist/components/tab-item'
import Radio from 'vux/dist/components/radio'
import Switch from 'vux/dist/components/switch'
import Selector from 'vux/dist/components/selector'
import Calendar from 'vux/dist/components/calendar'
import InlineCalendar from 'vux/dist/components/inline-calendar'
import Scroller from 'vux/dist/components/scroller'
export default {
    data(){
        return {
            demo1: '1',
            options: ['中国', '美国', '韩国'],
            value1: true,
            value2: false,
            defaultValue: '',
            plainList: ['广东', '广西'],
            list: [{key: 'gd', value: '广东'}, {key: 'gx', value: '广西'}],
            values1: '广西',
            values2: 'gd',
            list1: ['A', 'B', 'C'],
            cvalue: 'TODAY'
        }
    },
    components: {
        Hello,
        Tab,
        TabItem,
        Group,
        Cell,
        Radio,
        Switch,
        Selector,
        InlineCalendar,
        Calendar,
        Scroller
    },
    methods: {
        onChange(){
            
        }
    }
}
</script>

<style>
@import '~vux/dist/vux.css';
html {
    height: 100%;
}

body {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
    height: 100%;
}

#app {
    color: #2c3e50;
    max-width: 600px;
    font-family: Source Sans Pro, Helvetica, sans-serif;
    padding: 10px 0;
}

#app a {
    color: #42b983;
    text-decoration: none;
}

.logo {
    width: 100px;
    height: 100px
}
radio {
    width: 100%;
}
</style>

```

```
popup(:show.sync="popShow" height="150px")
      .btn-wrap
        .cancel(@click="popShow = false") 取消
        .sure(@click="saveClockPeriod") 保存
      .day-wrap
        .week(v-for="w in clock.weekTextList",
          @click="selectWeek($index)",
          :class="{'selected': weekValueList[$index]}")
          | {{w}}
```
