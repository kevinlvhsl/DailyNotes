### 利用http的get方法，爬取网页源码

```
var http = require('http')
var fs = require('fs')
var baseUrl = 'http://www.imooc.com/learn/'
var cheerio = require('cheerio')
http.get(baseUrl+ 348, function(res){
    var html = ''
    res.on('data', function(data){
        html += data
    })

    res.on('end', function(){
        fs.writeFileSync('scott.html', html, 'utf-8')
        console.log('ok')
        filterChapters(html)
    })
    res.on('error', function(err){
        console.error(err)
    })
})
// 过滤html源码信息 成有用的章节信息
// cheerio 跟jquery一样的解析html
function filterChapters(html){
    var $ = cheerio.load(html)
    var wrap = $('.mod-chapters')
    var chapters = wrap.find('.chapter')
    console.log(chapters)
    
    var courseDate = []
    chapters.each(function(item){
        var chapter = $(this)
        var title = chapter.find('strong').text()
        var videos = chapter.find('.video').children('li')
        console.log(title)
        //courseDate.push({
        //    title:title,
        //    videos: []
        //})
       
    })
}
```

+ 先将网页源码抓取回来
+ 然后利用cheerio模块解析load，则能跟jquery一样解析dom 提取中间有用的信息


