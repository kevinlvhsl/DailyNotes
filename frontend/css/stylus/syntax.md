### 迭代器
> Interpolation
Interpolation combined with other powerful features allow you to mold properties and selectors all within the language itself.

```
table
  for row in 1 2 3 4 5
    tr:nth-child({row})
      height: 10px * row
 
 等同 for row in (1..5)
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

========================

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
