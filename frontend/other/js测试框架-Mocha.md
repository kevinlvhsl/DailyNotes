## 测试框架 Mocha 实例教程
--本文内容来自[阮一峰](http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html)的博客

Mocha（发音"摩卡"）诞生于2011年，是现在最流行的JavaScript测试框架之一.
所谓测试框架，就是运行测试的工具。通过它，可以为javascript应用添加测试，从而保证代码的质量。

Mocha、Jasmine、Karma、Tape都是比较流行的测试框架。

### 测试脚本的写法
Mocha的作用是运行测试脚本，首先必须学会写测试脚本。所谓的测试脚本，就是用来啊测试源码的脚本。

下面是一个加法模块add.js的代码。
```
function add (a, b) {
  return a + b
}
module.exports = add
```
通常，测试脚本与要测试的源码脚本同名，但是后缀名为`.text.js`(表示测试)或者是`.spec.js`(表示规格) 
add.test.js
```
var add = require('./add.js');
var expect = require('chai').expect;

describe('加法函数的测试', function() {
  it('1 加 1 应该等于 2', function() {
    expect(add(1, 1)).to.be.equal(2);
  });
});
```
这段代码，就是测试脚本，它可以独立执行，测试脚本里面应该包括一个或多个`describe`块，
每个describe 块应该包括一个或多个it
.test.js
  --describe
    --it
    --it
    --...
  --describe
  ...

`describe ` 块称为册是套件test suite，表示一组相关的测试。他是一个函数，
第一个参数是测试套件的名称，
第二个参数是一个实际执行的函数

`it` 块称为测试用例 test case，表示一个单独的测试，是测试的最小单元。它也是一个函数
第一个单数 是测试用例的名称，“1+1应该等于2”
第二个参数是一个实际执行的函数。

### 断言库的用法
上面测试脚本里面有一句断言：`expect(add(1, 1).to.be.equal(2))`

所谓断言，就是判断源代码的实际执行结果与预期结果是否一致，如果不一致就跑出一个错误。

所有的测试用例（it块） 都应该包含一句或多句断言。他是编写测试用例的关键。
断言功能由断言库来实现，Mocha本身不带断言库，所以必须县映入断言库。
```var expect = require('chai').expect;```

断言库有很多种，上面代码引入的是 chai， 并指定使用expect断言风格。

expect 断言的优点是 接近自然语言：
```
//相等或不相等
expect(4+5).to.be.equal(9)
expect(4+5).to.be.not.equal(10)
expect(foo).bo.be.deep.equal({bar:'foo'})

// 布尔值为true
expect('everthing').to.be.ok;
expect(false).to.not.be.ok;

// typeof
expect('test').to.be.a('string');
expect({ foo: 'bar' }).to.be.an('object');
expect(foo).to.be.an.instanceof(Foo);

// include
expect([1,2,3]).to.include(2);
expect('foobar').to.contain('foo');
expect({ foo: 'bar', hello: 'universe' }).to.include.keys('foo');

// empty
expect([]).to.be.empty;
expect('').to.be.empty;
expect({}).to.be.empty;

// match
expect('foobar').to.match(/^foo/);
```

基本上expect断言的写法都是一样的，头不是expect方法，尾部是断言方法，
比如： equal、a/an，ok、match 两者之间用to或者to.be连接。

如果expect断言不成立，就会跑出一个错误，事实上，只要不跑出错误，测试用力就算通过。
`it('1 加 1 应该等于 2', function() {});`
上面的这个测试用例，内部没有任何代码，由于没有抛出了错误，所以还是会通过。

### Mocha的基本用法
最简单的命令：`mocha add.test.js ` 如果通过则会输出

加法函数的测试
    ✓ 1 加 1 应该等于 2

mocha命令后面可以指定多个测试脚本
`mocha file1 file2 file3 ...`

Mocha 默认运行test子目录里的测试脚本。 所以一般都会把测试脚本放在test目录里面，然后执行mocha就不需要参数了

但是mocha默认只执行test目录下的第一层测试用例，要想执行所有的包括更深层目录的用例， 必须加上--recursive参数
`mocha --recursive`

### 通配符
命令指定测试脚本时，可以使用通配符，同时指定多个文件。
```
mocha spec/{my, awesome}.js  // 指定执行spec目录下的my.js和.awesome.js
mocha test/unit/*.js  // 指定执行test/unit目录下的所欲js文件
```
除了使用shell通配符还可以使用node通配符。
```mocha 'test/**/*.@(js|jsx)' ```
上面代码指定运行test木下任何子目录中、文件后缀名为js或jsx的测试脚本。 
注意：node通配符要放在单引号之中，否则* 会先被shell解释





