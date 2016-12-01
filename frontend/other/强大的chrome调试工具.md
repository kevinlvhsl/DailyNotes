## chrom浏览器的强大功能
转自 [http://www.jianshu.com/p/a894f7f8d27d](http://www.jianshu.com/p/a894f7f8d27d)
> chrome dev-tools功能很强大。相信大多数人使用最多的一个api就是console.log，这很有用，但是这只是chrome 调试api 之一，还有很多其它非常强大的api！推开门，是另一片风景
console.log

其它没啥可讲，主要看看其格式化功能：
> console.log("I am %d years old, my name is %s",18,"Davin")
> I am 18 years old, my name is Davin
输出对象:%O,var t={name:"Davin",age:18}:

使用css样式:％c：


是不是似曾相识? 百度首页按f12看吧。
显示错误和警告：console.error、console.warn

注：除过这些，console还有count、assert、dir等方法，详情移步chrome console api.
$_

$_代表上一个语句的执行结果：

$0 - $4

代表inspect最近选中的5个dom对象，$0代表最近一次选中的dom。这非常有用，我们可以在elements面板中用鼠标单击某个dom,如果要对该dom进行操作，直接在命令行输入$0便是该dom的引用.

$(selector)、$$(selector)

使用css选择器选取dom, 前者只匹配第一个元素，是document.querySelector() 的一个别名，后者会返回所有，是document.querySelectorAll().的别名。

注意：如果"$"符已在js中定义，则会覆盖系统原始的$，当页面中引入jQuery时，$(jQuery)将会覆盖调试命令中的$。区分$有没有被覆盖的一个简单的方法是查看其定义：


未覆盖
下面是引入Neat.js后，neat会定义$：

已覆盖
clear()

清楚控制台的所有输出
copy(object)

将object拷贝到剪贴板
debug(function)

调试某个函数，当指定的函数被执行时将会断在被调试函数的源代码的第一句。

inspect(object/function)

查找某个对象或函数。执行后会定位到该对象／函数处。

自动选中body
命令行输入后，Elements面板中会自动选中body.

定位到函数
monitor(function)

观察某个函数被调用的情况：

Paste_Image.png
monitorEvents(object[, events])

观察某个对象发生的事件.如下，观察当前窗口大小变化的事件。

观察事件
可以同时观察多个事件：
  monitorEvents(window, ["resize", "scroll"])
可以和$0-$4结合使用：
monitorEvents($0, "key");
注：$0为一个input，观察其键盘事件。
当然也存在着相应的解绑事件，如下：
undebug(function)、unmonitor(function)、unmonitorEvents(object[, events])
getEventListeners(object)

获取object的所有事件listeners.

输出document DOMContentLoaded事件listener源码。
keys(object)、values(object)

查看对象的key、value

table(data[, columns])

将对象数据以表格形式显示，columns为可选的列标题。

详细的文档请参考：Command Line API Reference


文／杜文（简书作者）
原文链接：http://www.jianshu.com/p/a894f7f8d27d
著作权归作者所有，转载请联系作者获得授权，并标注“简书作者”。
