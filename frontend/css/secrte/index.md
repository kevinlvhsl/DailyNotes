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
