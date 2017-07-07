### VS Code 使用小技巧
这些天sublime突然抽风，老是死掉 逼我不得不用vs code。
一开始用的时候，真的很不习惯，少了好多好用的快捷键。 ctrl + shift + d    ctrl + shift + up/down   ctrl + k &  ctrl+b  ctrl+k && ctrl+u/l

但是vscode 的插件也很丰富。


所有插件查找地址（https://marketplace.visualstudio.com/）

编码快捷方式（http://docs.emmet.io/cheat-sheet/）

安装插件出现  错误unable to verify the first certificate （无法确认第一证书）　　

　　解决方法如下：　　

　　在vscode 下 进入 文件->首选项-->设置 在上面的搜索框输入 proxy,会出现 有3个相关设置项，设置如下的选项 

　　　　

1
2
3
4
// 是否应根据提供的 CA 列表验证代理服务器证书。
"http.proxyStrictSSL": true,
//设置为false , 这时候会在右侧的自定义设置中增加一条
"http.proxyStrictSSL": false,
　　　　重启 VScode ，然后在安装插件，会发现神奇的可以安装了。

插件

1、HTML Snippets

　　超级使用且初级的H5代码片段以及提示

2、HTML CSS Support 

　　让HTML标签上写class智能提示当前项目所支持的样式

3、jQuery Code Snippets

　　jQuery 提示工具

4、Path Intellisense

　　路径提示补全

5、Document this

　　Js的注释模板

6、ESlint

　　ESlint接管原声js提示，可以自定制体会规则 

7、Auto Close Tag

　　自动补全html标签

8、Auto Rename Tag

　　修改html标签，自动帮你完成尾部闭合标签的同步修改

9、View InBrowser

　　默认浏览器查看HTML文件（快捷键Ctrl+F1可以修改）

10、beautify

　　格式化代码的工具

11、Rainbow Brackets

　　彩虹括号（不推荐用）

12、Guides

　　标签对其线

13、Project Manager

　　在多个项目之前快速切换的工具

14、vscode-icons

　　让 vscode 资源树目录加上图标；点击设置->如图：
![](http://images2015.cnblogs.com/blog/1079080/201703/1079080-20170314091439666-1916642081.png)
　　

15、background

　　可以让vscode的背景修改为自己喜欢的图，最多3张照片

　　https://marketplace.visualstudio.com/items?itemName=shalldie.background

　　图片配置

　```
// Plugin background enabled.background 插件是否启用
    "background.enabled": false,
 
    // Use default images.使用默认图片
    "background.useDefault": false,
 
    // Your custom Images(Max length is 3). 自己定制背景图，最多3个
    "background.customImages": [
        "file:///E:/wushen.png",
        "file:///E:/wushen.png",
        "file:///E:/wushen.png"
    ]
　　
```

vsCode配置

```
// 控制是否显示 minimap(缩略图)
   "editor.minimap.enabled": true,

// 视区宽度自动换行设置。
　"editor.wordWrap": "on",

// 指定用在工作台中的颜色主题。
　"workbench.colorTheme": "Monokai",
```
来自[Lonely existence](http://www.cnblogs.com/sxz2008/p/6646857.html)



### vscode中的常用快捷键
VSCode 快捷键 Mac

#### 全局

Command + Shift + P / F1 显示命令面板
Command + P 快速打开
Command + Shift + N 打开新窗口
Command + W 关闭窗口

#### 基本

Command + X 剪切（未选中文本的情况下，剪切光标所在行）
Command + C 复制（未选中文本的情况下，复制光标所在行）
Option + Up 向上移动行
Option + Down 向下移动行
Option + Shift + Up 向上复制行
Option + Shift + Down 向下复制行
Command + Shift + K 删除行
Command + Enter 下一行插入
Command + Shift + Enter 上一行插入
Command + Shift + \ 跳转到匹配的括号
Command + [ 减少缩进
Command + ] 增加缩进
Home 跳转至行首
End 跳转到行尾
Command + Up 跳转至文件开头
Command + Down 跳转至文件结尾
Ctrl + PgUp 按行向上滚动
Ctrl + PgDown 按行向下滚动
Command + PgUp 按屏向上滚动
Command + PgDown 按屏向下滚动
Command + Shift + [ 折叠代码块
Command + Shift + ] 展开代码块
Command + K Command + [ 折叠全部子代码块
Command + K Command + ] 展开全部子代码块
Command + K Command + 0 折叠全部代码块
Command + K Command + J 展开全部代码块
Command + K Command + C 添加行注释
Command + K Command + U 移除行注释
Command + / 添加、移除行注释
Option + Shift + A 添加、移除块注释
Option + Z 自动换行、取消自动换行

#### 多光标与选择

Option + 点击 插入多个光标
Command + Option + Up 向上插入光标
Command + Option + Down 向下插入光标
Command + U 撤销上一个光标操作
Option + Shift + I 在所选行的行尾插入光标
Command + I 选中当前行
Command + Shift + L 选中所有与当前选中内容相同部分
Command + F2 选中所有与当前选中单词相同的单词
Command + Ctrl + Shift + Left 折叠选中
Command + Ctrl + Shift + Right 展开选中
Alt + Shift + 拖动鼠标 选中代码块
Command + Shift + Option + Up 列选择 向上
Command + Shift + Option + Down 列选择 向下
Command + Shift + Option + Left 列选择 向左
Command + Shift + Option + Right 列选择 向右
Command + Shift + Option + PgUp 列选择 向上翻页
Command + Shift + Option + PgDown 列选择 向下翻页

查找替换

Command + F 查找
Command + Option + F 替换
Command + G 查找下一个
Command + Shift + G 查找上一个
Option + Enter 选中所有匹配项
Command + D 向下选中相同内容
Command + K Command + D 移除前一个向下选中相同内容

进阶

Ctrl + Space 打开建议
Command + Shift + Space 参数提示
Tab Emmet插件缩写补全
Option + Shift + F 格式化
Command + K Command + F 格式化选中内容
F12 跳转到声明位置
Option + F12 查看具体声明内容
Command + K F12 分屏查看具体声明内容
Command + . 快速修复
Shift + F12 显示引用
F2 重命名符号
Command + Shift + . 替换为上一个值
Command + Shift + , 替换为下一个值
Command + K Command + X 删除行尾多余空格
Command + K M 更改文件语言

导航

Command + T 显示所有符号
Ctrl + G 跳转至某行
Command + P 跳转到某个文件
Command + Shift + O 跳转到某个符号
Command + Shift + M 打开问题面板
F8 下一个错误或警告位置
Shift + F8 上一个错误或警告位置
Ctrl + Shift + Tab 编辑器历史记录
Ctrl + - 后退
Ctrl + Shift + - 前进
Ctrl + Shift + M Tab 切换焦点

编辑器管理

Command + W 关闭编辑器
Command + K F 关闭文件夹
Command + \ 编辑器分屏
Command + 1 切换到第一分组
Command + 2 切换到第二分组
Command + 3 切换到第三分组
Command + K Command + Left 切换到上一分组
Command + K Command + Right 切换到下一分组
Command + K Command + Shift + Left 左移编辑器
Command + K Command + Shift + Right 右移编辑器
Command + K Left 激活左侧编辑组
Command + K Right 激活右侧编辑组

#### 文件管理

Command + N 新建文件
Command + O 打开文件
Command + S 保存文件
Command + Shift + S 另存为
Command + Option + S 全部保存
Command + W 关闭
Command + K Command + W 全部关闭
Command + Shift + T 重新打开被关闭的编辑器
Command + K Enter 保持打开
Ctrl + Tab 打开下一个
Ctrl + Shift + Tab 打开上一个
Command + K P 复制当前文件路径
Command + K R 在资源管理器中查看当前文件
Command + K O 新窗口打开当前文件

#### 显示

Command + Ctrl + F 全屏、退出全屏
Command + Option + 1 切换编辑器分屏方式（横、竖）
Command + + 放大
Command + - 缩小
Command + B 显示、隐藏侧边栏
Command + Shift + E 显示资源管理器 或 切换焦点
Command + Shift + F 显示搜索框
Ctrl + Shift + G 显示Git面板
Command + Shift + D 显示调试面板
Command + Shift + X 显示插件面板
Command + Shift + H 全局搜索替换
Command + Shift + J 显示、隐藏高级搜索
Command + Shift + C 打开新终端
Command + Shift + U 显示输出面板
Command + Shift + V Markdown预览窗口
Command + K V 分屏显示 Markdown预览窗口

#### 调试

F9 设置 或 取消断点
F5 开始 或 继续
F11 进入
Shift + F11 跳出
F10 跳过
Command + K Command + I 显示悬停信息

#### 集成终端

Ctrl + ` 显示终端
Ctrl + Shift + ` 新建终端
Command + Up 向上滚动
Command + Down 向下滚动
PgUp 向上翻页
PgDown 向下翻页
Command + Home 滚动到顶部
Command + End 滚动到底部
