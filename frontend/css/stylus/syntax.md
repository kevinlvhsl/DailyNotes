## stylus语法




在stylus中数组用圆括号 () 来表示。 如： (1 2 3 4 5)  表示5个元素的数组  取其中的某一个 用中括号[]    (1 2 3 4 5)[1]  得到 2

### 迭代器

> Interpolation
Interpolation combined with other powerful features allow you to mold properties and selectors all within the language itself.
---

```
table
  for row in 1 2 3 4 5
    tr:nth-child({row})
      height: 10px * row
 
 //等同 for row in (1..5)
------      
table tr:nth-child(1) {
  height: 10px;
}
table tr:nth-child(2) {
  height: 20px;
}
table tr:nth-child(3) {
  height: 30px;
}
table tr:nth-child(4) {
  height: 40px;
}
table tr:nth-child(5) {
  height: 50px;
}
-----

vendors = webkit moz o ms official

border-radius()
  for vendor in vendors
    if vendor == official
      border-radius: arguments
    else
      -{vendor}-border-radius: arguments
#content
  border-radius: 5px
  
  ----------
  #content {
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  -o-border-radius: 5px;
  -ms-border-radius: 5px;
  border-radius: 5px;
}
```




### 操作符

> Operators
Stylus supports all the operators you’ve come to expect from a language, as well as some specific to Stylus.

```
body
  foo: 5px + 10
  foo: 2 ** 8
  foo: 5px * 2
  foo: !!''
  foo: foo and bar and baz
  foo: foo or bar or baz
  foo: 1..5
  foo: 1...5
  foo: 'foo' is a 'string'
  foo: (1 2 3) == (1 2 3)
  foo: (1 2 3) == (1 2)
  foo: ((one 1) (two 2)) == ((one 1) (two 2)) 
  foo: ((one 1) (two 2)) == ((one 1) (two)) 
  foo: ((one 1) (two 2))[0]
  foo: 3 in (1 2 3 4)

body {
  foo: 15px;
  foo: 256;
  foo: 10px;
  foo: false;
  foo: baz;
  foo: foo;
  foo: 1 2 3 4 5;
  foo: 1 2 3 4;
  foo: true;
  foo: true;
  foo: false;
  foo: true;
  foo: false;
  foo: one 1;
  foo: true;
}
```

### 强类型 Type coercion

> Stylus performs type coercion when appropriate, and supports all of the unit types you’ve come to know and love.
 
```
body
  foo: foo + bar
  foo: 'foo ' + bar
  foo: 'foo ' + 'bar'
  foo: 'foo ' + 5px
  foo: 2s - 500ms
  foo: 5000ms == 5s
  foo: 50deg
  --------------
  body {
  foo: foobar;
  foo: 'foo bar';
  foo: 'foo bar';
  foo: 'foo 5px';
  foo: 1.5s;
  foo: true;
  foo: 50deg;
}
```

### 打印 分隔符The sprintf operator

> The powerful “%” operator when used with strings behaves like sprintf, with each argument compiled through the stylus compiler, producing a literal value.

```
body
  foo: '%s / %s' % (5px 10px)
  foo: 'MS:WeirdStuff(opacity=%s)' % 1
  foo: unquote('MS:WeirdStuff(opacity=1)')
  ----------------------
  body {
  foo: 5px / 10px;
  foo: MS:WeirdStuff(opacity=1);
  foo: MS:WeirdStuff(opacity=1);
}
```

### 颜色转换操作Color operations

> Operations against colors are especially useful. When adding or subtracting by a percentage the color lightness may be adjusted, or the hue may be adjusted with deg

```
body
  foo: white - 50%
  foo: black + 50%
  foo: #eee - #f00
  foo: #eee - rgba(black,.5)
  foo: #cc0000 + 30deg
  ----
  body {
  foo: #808080;
  foo: #808080;
  foo: #0ee;
  foo: rgba(238,238,238,0.5);
  foo: #c60;
}
  
```

### 函数Functions

Stylus functions may be defined in the same manner as mixins, however their usage differs as they return values. For example you could define a sum function as shown below:

```
sum(nums...)
  n = 0
  n += num for num in nums

body
  foo: sum(1, 2, 3)
------
body {
  foo: 6;
}
```

### 关键字参数 Keyword arguments

> Keyword arguments are also supported to make function invocation more expressive, also allowing you to disregard argument ordering.
允许传金额以：value形式
```
fade-out(color, amount = 50%)
  color - rgba(0,0,0,amount)

body
  foo: fade-out(#eee)
  foo: fade-out(#eee, 20%)
  foo: fade-out(#eee, amount: 50%)
  foo: fade-out(color: #eee, amount: 50%)
  foo: fade-out(amount: 50%, #eee)
  foo: fade-out(amount: 50%, color: #eee)
  
----
body {
  foo: rgba(238,238,238,0.5);
  foo: rgba(238,238,238,0.8);
  foo: rgba(238,238,238,0.5);
  foo: rgba(238,238,238,0.5);
  foo: rgba(238,238,238,0.5);
  foo: rgba(238,238,238,0.5);
}
```

### 内置函数 Built-in functions

> Stylus is packed with over 60 built-in functions for manipulating colors, checking variable types, math, list operations, and more, many of which are defined in the Stylus language itself

```
body
  foo: red(#fc0)
  foo: green(#fc0)
  foo: blue(#fc0)
  foo: alpha(#fff)
  foo: alpha(rgba(#fff, .5))
---
body {
  foo: 255;
  foo: 204;
  foo: 0;
  foo: 1;
  foo: 0.5;
}
```

### 颜色转换器 Color BIFs

The Color built-in functions allow you adjust lightness, hue, and saturation, check if colors are light or dark and more.
有判断函数，也有处理函数

```
body
  foo: light(#eee)
  foo: dark(#eee)
  foo: dark(#333)
  foo: darken(#eee, 50%)
  foo: lighten(black, 50%)
  foo: #eee - 50%
  foo: black + 50%
---
body {
  foo: true;
  foo: false;
  foo: true;
  foo: #777;
  foo: #808080;
  foo: #777;
  foo: #808080;
}
```






