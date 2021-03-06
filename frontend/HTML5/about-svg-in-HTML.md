## HTML中使用svg

在html中可以直接引入svg标签
也可以用 iframe来引入
还可以用object标签引入
```
object.svg-obj(type="image/svg+xml", data="static/images/expedition.svg")
```

在我们的js脚本中，可以直接获取到svg元素，通过id方式最快
javascript
```
 self.svgBox = $('.svg-obj')[0]   //通过选择器获取到svg的容器 object
  self.svgBox.onload = function() {
      self.svgNode = this.contentDocument.querySelector("#expedition") // 加载完后，获取其中的path标签
      self.init()
  }
  init(){ // 我们可以通过setAttribute 和 getAttribute 来操作各个节点的属性
        this.svgNode.setAttribute('stroke-dasharray', (this.percent * this.svgNode.getTotalLength()) + ' ' + this.svgNode.getTotalLength())
        this.svgNode.setAttribute('stroke-dashoffset', 0)
        this.setCurrentCoordPercent()
    },
setPercent(percent) {
    let already = this.svgNode.getTotalLength() * percent
    this.svgNode.setAttribute('stroke-dasharray',  already + ' ' + this.svgNode.getTotalLength())
},
setCurrentCoordPercent() {
    this.coordNode = $('.svg-obj')[0].contentDocument.querySelector("#currentcoordanimate")
    this.coordNode.setAttribute('begin', '0s')
    this.coordNode.setAttribute('end', (this.percent * 5) + 's')
}
```

最好玩的一点就是可以给svg加一些类似css的动画  SMIL动画 
参见 [svg animation][http://www.zhangxinxu.com/wordpress/2014/08/so-powerful-svg-smil-animation/]
```
<svg width="320" height="200" xmlns="http://www.w3.org/2000/svg">
    <text font-family="microsoft yahei" font-size="120" y="150" x="160">
        马
        <animate attributeName="x" values="160;40;160" dur="3s" repeatCount="indefinite" />
    </text>
</svg>
```

还有stroke-dasharray 和stroke-offset 两个属性来让path动起来
详情参见 [张鑫旭的博客][http://www.zhangxinxu.com/wordpress/2014/08/so-powerful-svg-smil-animation/]









