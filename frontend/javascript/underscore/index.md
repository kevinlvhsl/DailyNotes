##  util lib  underscore _  第一回 
[http://www.w3cfuns.com/notes/17398/441f8b402179ea95dd833bee9842bad2.html](http://www.w3cfuns.com/notes/17398/441f8b402179ea95dd833bee9842bad2.html)
 以上是源码研究解读。
 学习网址如下。
http://www.css88.com/doc/underscore/里面有api的用法，以及源码注释。
> 我们自己写代码时，什么样逻辑最容易懂呢？
第一次未测试版本时，是最容易看懂的。
因为没有后来那些为了修补bug，添加的各种if语句。
也没有后来的重构，代码复用后，导致的各种共有函数的抽离。

所以我从来不相信别人，写点代码时，就直接用单var链那种方式来写。除非代码短。
随便写写就是几百行，每写个变量都要返回到作用域顶部，填到单var链中吗？
单var链是有必要的。那是代码写完后，进行重构时，再移上去的。

###  框架 
```
(function(){
	
	//缓存this，浏览器的window或者服务端的exports
	var root = this;
	
	//下划线库的局部变量_,注意是个函数
	var _ = function(obj){
		if(obj instanceof _) return obj;
		if(!(this instanceof _)) return new _(obj);
		this._wrapped = obj;
	};
	
	//暴露给export或者window
	if(typeof exports !== 'undefined'){
		if(typeof module !== 'undefined' && module.exports){
			exports = module.exports = _;
		}
		exports._=_;
	}else{
		root._ = _;
	}
	
	_.VERSION = '1.8.2';
	
	/*各种内部变量、函数*/
	//...
	
	/*各种公开的静态api,如：*/
	_.each = function(){
		//TODO
	};
	_.first = function(){
		//TODO
	};
	_.bind = function(){
		//TODO
	};
	_.keys = function(){
		//TODO
	};
	_.noConfict = function(){
		//TODO
	};
	_.chain = function(){
		//TODO
	};
	//...
	
	//实例方法
	_.prototype.value = function(){
		//TODO
	};
	//...
	
	//对amd支持
	if (typeof define === 'function' && define.amd) {
		define('underscore', [], function() {
			return _;
		});
	}
}).call(this);
```
> 基本上都能看懂，
下划线构造函数我们得看看
```
var _ = function(obj){
		if(obj instanceof _) return obj;
		if(!(this instanceof _)) return new _(obj);
		this._wrapped = obj;
	};
```
> 第一句不用说，如果参数是自己的实例，那就返回参数。
主要是第二句。还记得我们生成数组时，可以不用写new的吗（虽然不提倡），比如`var a = new Array();  var a = Array();`

第二句代码就是其到是这个作用，如果你调用_，不是用new的，函数内部自动会给你new的，看下Person类
```var Person = function(name){
	if(!(this instanceof Person)){
		return new Person(name);
	}
	this.name = name;
}

var p = new Person('laoyao');
alert(p.name);

var p = Person('xxx');
alert(p.name);```
以上两句的作用是一样
当然了，你也可以反过来用，例如一个函数不让它new， 就在他 new 的 的时候 的时候提示 不能  new
```var MyAlert = function(str){
	if(this instanceof MyAlert){
		throw new Error("MyAlert is not a constructor");
	}
	alert(str);
}
MyAlert(111);//弹出
new MyAlert(222);//报错```



