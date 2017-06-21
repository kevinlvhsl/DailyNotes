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
