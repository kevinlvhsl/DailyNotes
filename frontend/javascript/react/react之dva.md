## dva

[官方地址](https://github.com/dvajs/dva)

主要封装了redux，使创建react-redux应用更简便快捷。

[介绍](http://slides.com/sorrycc/dva)

[一个快速上手的教程](https://github.com/sorrycc/blog/issues/18)
12步搭建一个简单的应用


### dva 的5个方法

```
  import dva from'dva';

// 1. Initialize 创建 dva 实例
  const app = dva();

// 2. 装载插件 (可选)
  app.use(require('dva‐loading')());

// 3. Register Model 注册 Model
  app.model(require('./models/count'));

// 4.  Set Router 配置路由
  app.router(require('./router'));

// 5. Start 启动应用
  app.start('#root');
```
##### 一段代码

```
import './index.html'
import 'babel-polyfill'
import dva from 'dva'
import createLoading from 'dva-loading'
import { browserHistory } from 'dva/router'

// 1. Initialize
const app = dva({
  initialState: {
    app: {
      login: true,
    },
  },
  ...createLoading(),
  history: browserHistory,
  onError (error) {
    console.error('app onError -- ', error)
  },
})


// 2. Model
app.model(require('./models/app'))
app.model(require('./models/dashboard'));
app.model(require('./models/statistics'));
app.model(require('./models/riskrecord'));
app.model(require('./models/verification'));
app.model(require('./models/DataManage'));
app.model(require('./models/AppManage'));


// 3. Router
app.router(require('./router'))

// 4. Start
app.start('#root')

```
![状态-路由组件-Model之间的关系图](https://s3.amazonaws.com/media-p.slid.es/uploads/564115/images/3216129/dva_concepts.png)
