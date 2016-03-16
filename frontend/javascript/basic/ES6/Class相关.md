## Class

### Class基本语法

Class基本语法
Class的继承
原生构造函数的继承
Class的取值函数（getter）和存值函数（setter）
Class的Generator方法
Class的静态方法
Class的静态属性和实例属性
new.target属性
Mixin模式的实现


1、Class基本语法
（1）概述

JavaScript语言的传统方法是通过构造函数，定义并生成新对象。下面是一个例子。

function Point(x,y){
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
}
上面这种写法跟传统的面向对象语言（比如C++和Java）差异很大，很容易让新学习这门语言的程序员感到困惑。
