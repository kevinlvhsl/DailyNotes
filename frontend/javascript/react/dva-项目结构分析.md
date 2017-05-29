### dva做的antd-admin管理后台项目

> antd 适合做管理后台，能够简单的做到轻度响应式布局。  栅格布局
一个经典的管理后台目录结构分析
antd-admin
  | assets    // 资源文件 截图示例图片、mp3等等
  | dist      // 打包后的js文件
  | node_modules  
  | public    // 字体文件图片文件、iconfont
  | src
    | components      // 组件目录， 具体页面组件还应该这里面细分
      | 各个组件的目录
      | ...
    | mock            // 假数据文件
    | models          // 页面模型，根据业务数据来分模型，而不是每个页面一个模型对象
    | routes          // 路由文件, 这里面只放页面布局相关的东西， 具体的组件部分应该放到components文件夹下
      app.js          // 整个后台入口容器。将页面分成左右部分，上下部分。 分块根据Layout组件来分
      app.less
      | user
      | chart
      | login
      | ...
    | services        // 调用数据库交互的代码
    | utils           // 工具方法、配置  config.js等通用函数和配置
    index.html        // 整个项目的入口，引入所需要的资源。
    index.js          // dva的入口，这里负责初始化dva实例。启动app
    router.js         // 路由配置，将所有可能的路由指定某个页面列出，及注册对应的模型对象。
    theme.js          // 主题配置文件，主体颜色等配置
  .eslintrcconfig
  .eslintrc
  .roadhogrc.js       // 打包配置文件
  .roadhogrc.mock.js  // 打包测试数据
  package.json      
  Reacme.md
  theme.config.js     // 配置主题引用的具体文件 css文件
  
    
    
    
