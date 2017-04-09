### js事件


+ dom 0级事件: 直接写在html中的属性绑定。dom节点上直接写 onclick/ onmouseover/等等 或者是 dom.onclick = function(){}
+ dom 2级事件： 通过事件侦听绑定（jquery的on('click', ()=>),或者addEventListener绑定）
> 区别：
dom0级事件 只能有一个，每次重新赋值都会覆盖之前的事件，
dom2级事件， 可以绑定多次，触发时多个都会执行。




通用兼容的事件监听对象

```
// event(事件)工具集，来源：github.com/markyun
 	markyun.Event = {
 		// 页面加载完成后
 		readyEvent : function(fn) {
 			if (fn==null) {
 				fn=document;
 			}
 			var oldonload = window.onload;
 			if (typeof window.onload != 'function') {
 				window.onload = fn;
 			} else {
 				window.onload = function() {
 					oldonload();
 					fn();
 				};
 			}
 		},
 		// 视能力分别使用dom0||dom2||IE方式 来绑定事件
 		// 参数： 操作的元素,事件名称 ,事件处理程序
 		addEvent : function(element, type, handler) {
 			if (element.addEventListener) {
 				//事件类型、需要执行的函数、是否捕捉
 				element.addEventListener(type, handler, false);
 			} else if (element.attachEvent) {
 				element.attachEvent('on' + type, function() {
 					handler.call(element);
 				});
 			} else {
 				element['on' + type] = handler;
 			}
 		},
 		// 移除事件
 		removeEvent : function(element, type, handler) {
 			if (element.removeEventListener) {
 				element.removeEventListener(type, handler, false);
 			} else if (element.datachEvent) {
 				element.detachEvent('on' + type, handler);
 			} else {
 				element['on' + type] = null;
 			}
 		},
 		// 阻止事件 (主要是事件冒泡，因为IE不支持事件捕获)
 		stopPropagation : function(ev) {
 			if (ev.stopPropagation) {
 				ev.stopPropagation();
 			} else {
 				ev.cancelBubble = true;
 			}
 		},
 		// 取消事件的默认行为
 		preventDefault : function(event) {
 			if (event.preventDefault) {
 				event.preventDefault();
 			} else {
 				event.returnValue = false;
 			}
 		},
 		// 获取事件目标
 		getTarget : function(event) {
 			return event.target || event.srcElement;
 		},
 		// 获取event对象的引用，取到事件的所有信息，确保随时能使用event；
 		getEvent : function(e) {
 			var ev = e || window.event;
 			if (!ev) {
 				var c = this.getEvent.caller;
 				while (c) {
 					ev = c.arguments[0];
 					if (ev && Event == ev.constructor) {
 						break;
 					}
 					c = c.caller;
 				}
 			}
 			return ev;
 		}
 	};
```


