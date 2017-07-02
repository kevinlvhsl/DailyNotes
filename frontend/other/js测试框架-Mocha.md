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

上面的node通配符改成shell版的：
`mocha test/{,**/}*.{js,jsx}`

### 命令行参数
除了前面介绍的--recursive， mocha 还可以加上其他命令行参数，

+ --help, -h // 查看所有的参数列表  帮助

+ --reporter , -R  // 指定测试报告的格式， 默认是spec格式
    还可以是其他格式  mocha --reporter tap
    
+ --reporters  // 显示所有内置的报告格式dot - dot matrix
    doc - html documentation
    spec - hierarchical spec list
    json - single json object
    progress - progress bar
    list - spec-style listing
    tap - test-anything-protocol
    landing - unicode landing strip
    xunit - xunit reporter
    min - minimal reporter (great with --watch)
    json-stream - newline delimited json events
    markdown - markdown documentation (github flavour)
    nyan - nyan cat!

  + 使用mochawesome模块，可以生成漂亮的HTML格式的报告。
    `npm install --save-dev mochawesome`
    `../node_modules/.bin/mocha --reporter mochawesome`
上面代码中，mocha命令，使用了项目内安装的版本，而不是全局的版本，因为mochawesome模块是安装在项目内的
测试结果报告在mochaawesome-reports子目录生成（当前目录下自动创建）

+ --growl -G
  将测试结果在桌面显示 （经测试貌似无效）

+ --watch -W
 用来监视指定的测试脚本。 mocha --watch 
 上面命令执行以后，并不会退出， 你可以另外打开一个新的窗口，修改test目录下的测试脚本， 比如删除一个测试用例，
 一旦保存， MOcha就会再次自动运行。
 
+ --bail -b

  指定只要 有一个测试用例么有通过，就停止执行后面的测试用例， 这对[持续集成](http://www.ruanyifeng.com/blog/2015/09/continuous-integration.html)很有用.

+ --grep -g
  用于搜索测试用例的名称， 即it块的第一个参数， 然后只执行匹配的测试用例。
  mocha --grep "1 加 1"  只执行测试名称中包含"1 加 1"的测试用例

+ --invert -i
  表示只运行不符合条件的测试脚本 必须与 --grep参数配合使用
  mocha --grep "1 加 1" --invert
  
  ### 配置文件 mocha.opts
  Mocha 允许在test目录下面放置配置文件mocha.opts， 把命令行参数写在里面，
`mocha --recursive --reporter tap --growl`
 写在配置文件
mocha.opts文件。
 ``` --reporter tap
  --recursive
  --growl
  ```
两者效果一致

### ES6测试
如果测试脚本使用ES6写的， name运行测试之前，需要先用babel转码。
```
import add from '../src/add.js';
import chai from 'chai';

let expect = chai.expect;

describe('加法函数的测试', function() {
  it('1 加 1 应该等于 2', function() {
    expect(add(1, 1)).to.be.equal(2);
  });
});
```
ES6转码，需要安装Babel。
`npm install babel-core babel-preset-es2015 --save-dev`
然后在项目下新建一个`.babelrc`配置文件
`{
   "presets": ['es2015'] 
}`
最后使用 --compilers 参数指定测试脚本的转码器
```
../node_modules/mocha/bin/mocha --compilers js:babel-core/register 
```
注意，Babel默认不会对Iterator、Generator、Promise、Map、Set等全局对象，以及一些全局对象的方法（比如Object.assign）转码。如果你想要对这些对象转码，就要安装babel-polyfill。
`npm install babel-polyfill --save`
然后，在你的脚本头部加上一行。
import 'babel-polyfill'

### 异步测试
Mocha默认每个测试用例最多执行2000毫秒，如果到时没有得到结果，就报错。
对于涉及异步操作的测试用例，这个时间往往是不够的，需要用-t或--timeout参数指定超时门槛。

进入demo05子目录，打开测试脚本timeout.test.js。
```
it('测试应该5000毫秒后结束', function(done) {
  var x = true;
  var f = function() {
    x = false;
    expect(x).to.be.not.ok;
    done(); // 通知Mocha测试结束
  };
  setTimeout(f, 4000);
});
```
上面的测试用例，需要4000毫秒之后，才有运行结果。所以，需要用-t或--timeout参数，改变默认的超时设置。
mocha -t 5000 timeout.test.js  // 将测试的超时时限指定为5000毫秒。

面的测试用例里面，有一个done函数。it块执行的时候，传入一个done参数，当测试结束的时候，必须显式调用这个函数，告诉Mocha测试结束了。否则，Mocha就无法知道，测试是否结束，会一直等到超时报错。你可以把这行删除试试看。
Mocha默认会高亮显示超过75毫秒的测试用例，可以用-s或--slow调整这个参数。
mocha -t 5000 -s 1000 timeout.test.js
上面命令指定高亮显示耗时超过1000毫秒的测试用例。
下面是另外一个异步测试的例子async.test.js。
```
it('异步请求应该返回一个对象', function(done){
  request
    .get('https://api.github.com')
    .end(function(err, res){
      expect(res).to.be.an('object');
      done();
    });
});```
Mocha内置对Promise的支持，允许直接返回Promise，等到它的状态改变，再执行断言，
而不用显式调用done方法。请看promise.test.js。
```
it('异步请求应该返回一个对象', function() {
  return fetch('https://api.github.com')
    .then(function(res) {
      return res.json();
    }).then(function(json) {
      expect(json).to.be.an('object');
    });
});
```

### 测试用例的钩子
Mocha在describe块之中，提供测试用例的四个钩子：before()、after()、beforeEach()和afterEach()。它们会在指定时间执行。
```
describe('hooks', function() {

  before(function() {
    // 在本区块的所有测试用例之前执行
  });

  after(function() {
    // 在本区块的所有测试用例之后执行
  });

  beforeEach(function() {
    // 在本区块的每个测试用例之前执行
  });

  afterEach(function() {
    // 在本区块的每个测试用例之后执行
  });

  // test cases
});
```

beforeEach会在it之前执行，所以会修改全局变量。
```
// beforeEach.test.js
describe('beforeEach示例', function() {
  var foo = false;

  beforeEach(function() {
    foo = true;
  });

  it('修改全局变量应该成功', function() {
    expect(foo).to.be.equal(true);
  });
});
```

另一个例子beforeEach-async.test.js则是演示，如何在beforeEach之中使用异步操作。
```
// beforeEach-async.test.js
describe('异步 beforeEach 示例', function() {
  var foo = false;

  beforeEach(function(done) {
    setTimeout(function() {
      foo = true;
      done();
    }, 50);
  });

  it('全局变量异步修改应该成功', function() {
    expect(foo).to.be.equal(true);
  });
});
```

### 测试用例管理
大型项目有很多测试用例。有时，我们希望只运行其中的几个，这时可以用only方法。describe块和it块都允许调用only方法，表示只运行某个测试套件或测试用例。
```

it.only('1 加 1 应该等于 2', function() {
  expect(add(1, 1)).to.be.equal(2);
});

it('任何数加0应该等于自身', function() {
  expect(add(1, 0)).to.be.equal(1);
});
```
只有带有only方法的测试用例会运行。

还有skip方法，表示跳过指定的测试套件或测试用例。
it.skip('任何数加0应该等于自身', function() {
  expect(add(1, 0)).to.be.equal(1);
});

### 浏览器测试

除了在命令行运行，Mocha还可以在浏览器运行。
+ 首先，使用mocha init命令在指定目录生成初始化文件。
`mocha init demo08`

运行上面命令，就会在demo08目录下生成index.html文件，以及配套的脚本和样式表。
```
<!DOCTYPE html>
<html>
  <body>
    <h1>Unit.js tests in the browser with Mocha</h1>
    <div id="mocha"></div>
    <script src="mocha.js"></script>
    <script>
      mocha.setup('bdd');
    </script>
    <script src="tests.js"></script>
    <script>
      mocha.run();
    </script>
  </body>
</html>
```
// add.js
function add(x, y) {
  return x + y;
}
+ 然后，把这个文件，以及断言库chai.js，加入index.html。

<script>
  mocha.setup('bdd');
</script>
<script src="add.js"></script>
<script src="http://chaijs.com/chai.js"></script>
<script src="tests.js"></script>
<script>
  mocha.run();
</script>
+ 最后，在tests.js里面写入测试脚本。

### 生成规格文件
Mocha支持从测试用例生成规格文件。
进入demo09子目录，运行下面的命令。
`mocha --recursive -R markdown > spec.md`

上面命令根据test目录的所有测试脚本，生成一个规格文件spec.md。-R markdown参数指定规格报告是markdown格式。
如果想生成HTML格式的报告spec.html，使用下面的命令。

`mocha --recursive -R doc > spec.html`






