对2.0的解读学习
http://www.kancloud.cn/zmwtp/vue2/148822
> Vue\                ;根目录
    benchmarks\     ;测试目录
    build\          ;构建目录
    dist\           ;生成目录
    examples\       ;Demo目录
    src\            ;源代码目录
    test\           ;测试目录
    
> 源代码实现目录(vue\src)

Vue\src\
    compiler\       ;模板编译实现
    core\           ;Vue核心实现
    entries\        ;生成入口实现
    platforms\      ;渲染平台实现
    server\         ;服务器渲染实现
    shared\         ;基础工具目录
> 模块组织(\vue\build\alias.js)
```
    var path = require('path')
    
    module.exports = {
      vue: path.resolve(__dirname, '../src/entries/web-runtime-with-compiler'),
      compiler: path.resolve(__dirname, '../src/compiler'),
      core: path.resolve(__dirname, '../src/core'),
      shared: path.resolve(__dirname, '../src/shared'),
      web: path.resolve(__dirname, '../src/platforms/web'),
      server: path.resolve(__dirname, '../src/server')
    }
```
