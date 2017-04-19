## JS优化代码技巧

1.Insert item inside an Array（向数组中插入元素）
```
var arr = [1,2,3,4,5];
//old method
arr.push(6);
//new method 快43%
arr[arr.length] = 6;
   
var arr = [1,2,3,4,5];
//old method
arr.unshift(0);
//new method 快98%
[0].concat(arr);
 ```

3.Sorting strings with accented characters（排列含音节字母的字符串）
> Javascript有一个原生方法sort可以排列数组。一次简单的 array.sort() 将每一个数组元素视为字符串并按照字母表排列。
但是当你试图整理一个非ASCII元素的数组时，你可能会得到一个奇怪的结果
**Intl.Collator().compare**
```
 ['único','árbol', 'cosas', 'fútbol'].sort(Intl.Collator().compare);
14      // ["árbol", "cosas", "fútbol", "único"]
15  
16      ['Woche', 'wöchentlich', 'wäre', 'Wann'].sort(Intl.Collator().compare);
17      // ["Wann", "wäre", "Woche", "wöchentlich"]
```



## 从缓存方面去优化

### 为什么要用缓存
一般针对静态资源如CSS,JS,图片等使用缓存，原因如下：

+ 请求更快：通过将内容缓存在本地浏览器或距离最近的缓存服务器（如CDN），在不影响网站交互的前提下可以大大加快网站加载速度。
+ 节省带宽：对于已缓存的文件，可以减少请求带宽甚至无需请求网络。
+ 降低服务器压力：在大量用户并发请求的情况下，服务器的性能受到限制，此时将一些静态资源放置在网络的多个节点，可以起到均衡负载的作用，降低服务器的压力。

### 缓存分类
缓存分为服务端侧（server side，比如 Nginx、Apache）和客户端侧（client side，比如 web browser）。常用的服务端缓存有CDN缓存，客户端缓存就是指浏览器缓存。

#### 浏览器缓存机制详解
> 缓存类型
浏览器缓存分为强缓存和协商缓存：
1 强缓存：浏览器在加载资源时，先根据这个资源的一些http header判断它是否命中强缓存，强缓存如果命中，浏览器直接从自己的缓存中读取资源，不会发请求到服务器。比如某个css文件，如果浏览器在加载它所在的网页时，这个css文件的缓存配置命中了强缓存，浏览器就直接从缓存中加载这个css，连请求都不会发送到网页所在服务器；
2 协商缓存：当强缓存没有命中的时候，浏览器一定会发送一个请求到服务器，通过服务器端依据资源的另外一些http header验证这个资源是否命中协商缓存，如果协商缓存命中，服务器会将这个请求返回（304），但是不会返回这个资源的数据，而是告诉客户端可以直接从缓存中加载这个资源，于是浏览器就又会从自己的缓存中去加载这个资源；若未命中请求，则将资源返回客户端，并更新本地缓存数据（200）。

强缓存与协商缓存区别：强缓存不发请求到服务器，协商缓存会发请求到服务器。

### 如何设置缓存
#### 1 HTML Meta标签控制缓存（非HTTP协议定义）
<META HTTP-EQUIV="Pragma" CONTENT="no-cache">
上述代码的作用是告诉浏览器当前页面不被缓存，每次访问都需要去服务器拉取。这种方法使用上很简单，但只有部分浏览器可以支持，而且所有缓存代理服务器都不支持，因为代理不解析HTML内容本身。

####　2 HTTP头信息控制缓存
HTTP头信息控制缓存是通过Expires（强缓存）、Cache-control（强缓存）、Last-Modified/If-Modified-Since（协商缓存）、Etag/If-None-Match（协商缓存）实现，下面详细介绍。

+ 1）Expires是http1.0提出的一个表示资源过期时间的header，它描述的是一个绝对时间，由服务器返回，用GMT格式的字符串表示，如：Expires:Thu, 31 Dec 2016 23:55:55 GMT，

读取缓存数据条件：缓存过期时间（服务器的）< 当前时间（客户端的
缺点：Expires是较老的强缓存管理header，由于它是服务器返回的一个绝对时间，这样存在一个问题，如果客户端的时间与服务器的时间相差很大（比如时钟不同步，或者跨时区），那么误差就很大，所以在HTTP 1.1版开始，使用Cache-Control: max-age=秒替代。
+ 2）Cache-Control描述的是一个相对时间，在进行缓存命中的时候，都是利用客户端时间进行判断，所以相比较Expires，Cache-Control的缓存管理更有效，安全一些。

读取缓存数据条件：上次缓存时间（客户端的）+max-age < 当前时间（客户端的）

+ Cache-Control值可以是 `public、private、no-cache、no- store、no-transform、must-revalidate、proxy-revalidate、max-age`

> 各个消息中的指令含义如下：
   + Public指示响应可被任何缓存区缓存。
   + Private指示对于单个用户的整个或部分响应消息，不能被共享缓存处理。这允许服务器仅仅描述当前用户的部分响应消息，此响应消息对于其他用户的请求无效。
   + no-cache指示请求或响应消息不能缓存，该选项并不是说可以设置”不缓存“，而是需要和服务器确认
   + no-store在请求消息中发送将使得请求和响应消息都不使用缓存，完全不存下來。
   + max-age指示客户机可以接收生存期不大于指定时间（以秒为单位）的响应。上次缓存时间（客户端的）+max-age（64200s）<客户端当前时间
   + min-fresh指示客户机可以接收响应时间小于当前时间加上指定时间的响应。
   + max-stale指示客户机可以接收超出超时期间的响应消息。如果指定max-stale消息的值，那么客户机可以接收超出超时期指定值之内的响应消息。

> 注意：这两个header可以只启用一个，也可以同时启用，当response header中，Expires和Cache-Control同时存在时，Cache-Control优先级高于Expires：

+ 3）Last-Modified/If-Modified-Since：Last-Modified/If-Modified-Since要配合Cache-Control使用。
Last-Modified：标示这个响应资源的最后修改时间。web服务器在响应请求时，告诉浏览器资源的最后修改时间。
If-Modified-Since：当资源过期时（强缓存失效），发现资源具有Last-Modified声明，则再次向web服务器请求时带上头 If-Modified-Since，表示请求时间。web服务器收到请求后发现有头If-Modified-Since 则与被请求资源的最后修改时间进行比对。若最后修改时间较新，说明资源又被改动过，则响应整片资源内容（写在响应消息包体内），HTTP 200；若最后修改时间较旧，说明资源无新修改，则响应HTTP 304 (无需包体，节省浏览)，告知浏览器继续使用所保存的cache。
缺点：

Last-Modified标注的最后修改只能精确到秒级，如果某些文件在1秒钟以内，被修改多次的话，它将不能准确标注文件的修改时间（无法及时更新文件）
如果某些文件会被定期生成，当有时内容并没有任何变化，但Last-Modified却改变了，导致文件没法使用缓存，有可能存在服务器没有准确获取文件修改时间，或者与代理服务器时间不一致等情形（无法使用缓存）。

+ 4）Etag/If-None-Match：Etag/If-None-Match也要配合Cache-Control使用。
Etag：web服务器响应请求时，告诉浏览器当前资源在服务器的唯一标识（生成规则由服务器决定）。Apache中，ETag的值，默认是对文件的索引节（INode），大小（Size）和最后修改时间（MTime）进行Hash后得到的。
If-None-Match：当资源过期时（使用Cache-Control标识的max-age），发现资源具有Etage声明，则再次向web服务器请求时带上头If-None-Match （Etag的值）。web服务器收到请求后发现有头If-None-Match 则与被请求资源的相应校验串进行比对，决定返回200或304。
Etag是服务器自动生成或者由开发者生成的对应资源在服务器端的唯一标识符，能够更加准确的控制缓存。Last-Modified与ETag一起使用时，服务器会优先验证ETag。
Etag 请求流程图
![请求流程图](https://segmentfault.com/img/bVCrP5)
![https://segmentfault.com/img/bVCrP8](https://segmentfault.com/img/bVCrP8)

#### 3、用户行为与缓存

浏览器缓存行为还有用户的行为有关，引用文章[浏览器 HTTP 协议缓存机制](http://my.oschina.net/leejun2005/blog/369148)详解的结论
![](https://segmentfault.com/img/bVCrQj)


### CDN缓存
> CDN缓存属于Cache服务器的一种。
CDN的全称是Content Delivery Network，即内容分发网络。其目的是通过在现有的Internet中增加一层新的网络架构，将网站的内容发布到最接近用户的网络"边缘"，使用户可 以就近取得所需的内容，解决Internet网络拥塞状况，提高用户访问网站的响应速度。从技术上全面解决由于网络带宽小、用户访问量大、网点分布不均等 原因，解决用户访问网站的响应速度慢的根本原因。
![](https://segmentfault.com/img/bVCrQC)

通过上图，我们可以了解到，使用了CDN缓存后的网站的访问过程为：
　　1)、用户向浏览器提供要访问的域名；
　　2)、浏览器调用域名解析库对域名进行解析，由于CDN对域名解析过程进行了调整，所以解析函数库一般得到的是该域名对应的CNAME记录，为了得到实际IP地址，浏览器需要再次对获得的CNAME域名进行解析以得到实际的IP地址；在此过程中，使用的全局负载均衡DNS解析，如根据地理位置信 息解析对应的IP地址，使得用户能就近访问。
　　3)、此次解析得到CDN缓存服务器的IP地址，浏览器在得到实际的IP地址以后，向缓存服务器发出访问请求；
　　4)、若请求文件并未修改，返回304（充当服务器的角色）。若当前文件已过期，则缓存服务器根据浏览器提供的要访问的域名，通过Cache内部专用DNS解析得到此域名的实际IP地址，再由缓存服务器向此实际IP地址提交访问请求；
　　5)、缓存服务器从实际IP地址得得到内容以后，一方面在本地进行保存，以备以后使用，二方面把获取的数据返回给客户端，完成数据服务过程；
　　6)、客户端得到由缓存服务器返回的数据以后显示出来并完成整个浏览的数据请求过程。
  
  
  ---参考[https://segmentfault.com/a/1190000006741200](https://segmentfault.com/a/1190000006741200)











