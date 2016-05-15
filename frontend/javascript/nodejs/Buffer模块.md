### Buffer

buffer 是用来处理各种数据的。 
在javascript中是以uft-8编码格式来保存数据的，而在计算机中是以二进制来保存和处理各种数据，
所以 需要Buffer对象来转换处理。
在nodejs 中Buffer对象是内置的。 打开命令行 node环境下： `Buffer`
```
> Buffer
{ [Function: Buffer]
  poolSize: 8192,
  isBuffer: [Function: isBuffer],
  compare: [Function: compare],
  isEncoding: [Function],
  concat: [Function],
  byteLength: [Function: byteLength] }
  ```
  poolSize: 表示缓存默认区大小， 其余为自带的方法  isBuffer：判断一个对象是否为Buffer对象
  
  创建Buffer对象：
  可以给构造函数中传入[内容]  或  [内容],[编码]， 或者 传一个长度数字[length]
  如果指定buf的长度的话，超过长度的内容将不被缓冲
  ```
  var buf =new Buffer(100024)
  var buf = new Buffer('hello 慕课网')
undefined
> buf
<Buffer 68 65 6c 6c 6f 20 e6 85 95 e8 af be e7 bd 91>
--------
 var buf = new Buffer('hello 慕课网', 'base64')
undefined
> buf
<Buffer 85 e9 65 a1 44>
```

  
  
