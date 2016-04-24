### css揭秘相关
## 说明



有很多优秀的网站提供了及时有效的浏览器兼容性信息。 推荐如下：
 Can I Use
...
?（ http://caniuse.com）
 WebPlatform.org（ http://webplatform.org）
 Mozilla Developer Network（ http://developer.mozilla.org）
 维基百科上的“浏览器排版引擎对比（ CSS 兼容性）”词条（ http://
en.wikipedia.org/wiki/Comparison_of_layout_engines_(Cascading_
Style_Sheets)）
有时候你可能会发现某个特性已经得到浏览器支持了， 但不同浏览器的
表现可能还有着细微的差异。 比如说， 它可能需要一个浏览器前缀 2①， 或者
在语法上存在细微的差别。 我们的示例代码中只会包含符合标准的、 无前缀
的语法。 不过在绝大多数情况下， 你都可以同时使用各种不同的语法， 并且
通过层叠机制来确保哪条声明最终生效。 出于这个原因， 你应该把标准语法
排在最后。 举例来说， 要得到一条从黄色到红色的垂直渐变色， 本书只会列
出标准语法：
background: linear-gradient(90deg, yellow, red);


在 CSS 2 之后， CSS 工作组意识到这门语言已经变得非常庞大， 再也无
法把它塞进单个规范中了。 这样不仅阅读和编辑极其困难， 而且限制了 CSS
本身的快速发展。 别忘了， 一项规范如果要推进到最终阶段， 其中的每项特
性都必须具备两个独立的实现和全面的测试。 原先的那种方式已经玩不转
了。 因此， 我们决定跨出一步， 将 CSS 打散到多个不同的规范（ 模块） 中，
每个模块都可以独立更新版本。 这其中， 那些延续 CSS 2.1 已有特性的模块
会升级到 3 这个版本号。 比如以下模块：
 CSS 语法（ http://w3.org/TR/css-syntax-3）
 CSS 层叠与继承（ http://w3.org/TR/css-cascade-3）
 CSS 颜色（ http://w3.org/TR/css3-color）
 选择符（ http://w3.org/TR/selectors）
 CSS 背景与边框（ http://w3.org/TR/css3-background）
 CSS 值与单位（ http://w3.org/TR/css-values-3）
 CSS 文本排版（ http://w3.org/TR/css-text-3）
 CSS 文本装饰效果（ http://w3.org/TR/css-text-decor-3）
 CSS 字体（ http://w3.org/TR/css3-fonts）
 CSS 基本 UI 特性（ http://w3.org/TR/css3-ui）
此外， 如果某个模块是前所未有的新概念， 那它的版本号将从 1 开始。
比如下面这些：
 CSS 变形（ http://w3.org/TR/css-transforms-1）
 图像混合效果（ http://w3.org/TR/compositing-1）
 滤镜效果（ http://w3.org/TR/filter-effects-1）
 CSS 遮罩（ http://w3.org/TR/css-masking-1）
 CSS 伸缩盒布局（ http://w3.org/TR/css-flexbox-1）
 CSS 网格布局（ http://w3.org/TR/css-grid-1）
