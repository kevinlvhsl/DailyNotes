### react的基本组成部分和基本语法
---------------------

#### 一、HTML 模板
```
<!DOCTYPE html>
<html>
  <head>
    <script src="../build/react.js"></script>
    <script src="../build/react-dom.js"></script>
    <script src="../build/browser.min.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/babel">
      // ** Our code goes here! **
    </script>
  </body>
</html>
```
> 上面代码有两个地方需要注意。首先，最后一个 <script> 标签的 type 属性为 text/babel 。这是因为 React 独有的 JSX 语法，跟 JavaScript 不兼容。凡是使用 JSX 的地方，都要加上 type="text/babel" 
> 也可以用jsxTransform.js解释包
> 其次，上面代码一共用了三个库： react.js 、react-dom.js 和 Browser.js ，它们必须首先加载。其中，react.js 是 React 的核心库，react-dom.js 是提供与 DOM 相关的功能，Browser.js 的作用是将 JSX 语法转为 JavaScript 语法，这一步很消耗时间，实际上线的时候，应该将它放到服务器完成。

#### 二、ReactDOM.render()
```
ReactDOM.render 是 React 的*最基本方法*，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);
```

#### 三、JSX 语法
> HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写
```
var names = ['Alice', 'Emily', 'Kate'];
ReactDOM.render(
  <div>
  {
    names.map(function (name) {
      return <div>Hello, {name}!</div>
    })
  }
  </div>,
  document.getElementById('example')
);
```
> 上面代码体现了 JSX 的基本语法规则：遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析。
  JSX 允许直接在模板插入 JavaScript 变量。如果这个变量是一个数组，则会展开这个数组的所有成员 https://github.com/ruanyf/react-demos/blob/master/demo03/index.html
```var arr = [
  <h1>Hello world!</h1>,
  <h2>React is awesome</h2>,
];
ReactDOM.render(
  <div>{arr}</div>,
  document.getElementById('example')
);```
> 上面代码的arr变量是一个数组，结果 JSX 会把它的所有成员，添加到模板
#### 四、组件
> React 允许将代码封装成组件（component），然后像插入普通 HTML 标签一样，在网页中插入这个组件。React.createClass 方法就用于生成一个组件类
```
var HelloMessage = React.createClass({
  render: function() {
    return <h1>Hello {this.props.name}</h1>;
  }
});

ReactDOM.render(
  <HelloMessage name="John" />,
  document.getElementById('example')
);
```
> 上面代码中，变量 HelloMessage 就是一个组件类。模板插入 <HelloMessage /> 时，会自动生成 HelloMessage 的一个实例（下文的"组件"都指组件类的实例）。所有组件类都必须有自己的 render 方法，用于输出组件。
注意，组件类的第一个字母必须大写，否则会报错，比如HelloMessage不能写成helloMessage。另外，--组件类只能包含一个顶层标签，否则也会报错--。
``` 错误代码示例

var HelloMessage = React.createClass({
  render: function() {
    return <h1>
      Hello {this.props.name}
    </h1><p>
      some text
    </p>;
  }
});```
*** 添加组件属性，有一个地方需要注意，就是 class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。

#### 五、this.props.children
> this.props 对象的属性与组件的属性一一对应，但是有一个例外，就是 this.props.children 属性。它表示组件的所有子节点
```
var NotesList = React.createClass({
  render: function() {
    return (
      <ol>
      {
        React.Children.map(this.props.children, function (child) {
          return <li>{child}</li>;
        })
      }
      </ol>
    );
  }
});

ReactDOM.render(
  <NotesList>
    <span>hello</span>
    <span>world</span>
  </NotesList>,
  document.body
);```

上面代码的 NoteList 组件有两个 span 子节点，它们都可以通过 this.props.children 读取。

#### 六、PropTypes
> 组件的属性可以接受任意值，字符串、对象、函数等等都可以。有时，我们需要一种机制，验证别人使用组件时，提供的参数是否符合要求。
组件类的PropTypes属性，就是用来验证组件实例的属性是否符合要求 
> 与vue的props是一样的
```var MyTitle = React.createClass({
  propTypes: {
    title: React.PropTypes.string.isRequired,
  },

  render: function() {
     return <h1> {this.props.title} </h1>;
   }
});```
> 上面的Mytitle组件有一个title属性。PropTypes 告诉 React，这个 title 属性是必须的，而且它的值必须是字符串。现在，我们设置 title 属性的值是一个数值。 [更多的PropTypes设置](http://facebook.github.io/react/docs/reusable-components.html)
```
React.createClass({
  propTypes: {
    // You can declare that a prop is a specific JS primitive. By default, these
    // are all optional.
    optionalArray: React.PropTypes.array,
    optionalBool: React.PropTypes.bool,
    optionalFunc: React.PropTypes.func,
    optionalNumber: React.PropTypes.number,
    optionalObject: React.PropTypes.object,
    optionalString: React.PropTypes.string,

    // Anything that can be rendered: numbers, strings, elements or an array
    // (or fragment) containing these types.
    optionalNode: React.PropTypes.node,

    // A React element.
    optionalElement: React.PropTypes.element,

    // You can also declare that a prop is an instance of a class. This uses
    // JS's instanceof operator.
    optionalMessage: React.PropTypes.instanceOf(Message),

    // You can ensure that your prop is limited to specific values by treating
    // it as an enum.
    optionalEnum: React.PropTypes.oneOf(['News', 'Photos']),

    // An object that could be one of many types
    optionalUnion: React.PropTypes.oneOfType([
      React.PropTypes.string,
      React.PropTypes.number,
      React.PropTypes.instanceOf(Message)
    ]),

    // An array of a certain type
    optionalArrayOf: React.PropTypes.arrayOf(React.PropTypes.number),

    // An object with property values of a certain type
    optionalObjectOf: React.PropTypes.objectOf(React.PropTypes.number),

    // An object taking on a particular shape
    optionalObjectWithShape: React.PropTypes.shape({
      color: React.PropTypes.string,
      fontSize: React.PropTypes.number
    }),

    // You can chain any of the above with `isRequired` to make sure a warning
    // is shown if the prop isn't provided.
    requiredFunc: React.PropTypes.func.isRequired,

    // A value of any data type
    requiredAny: React.PropTypes.any.isRequired,

    // You can also specify a custom validator. It should return an Error
    // object if the validation fails. Don't `console.warn` or throw, as this
    // won't work inside `oneOfType`.
    customProp: function(props, propName, componentName) {
      if (!/matchme/.test(props[propName])) {
        return new Error(
          'Invalid prop `' + propName + '` supplied to' +
          ' `' + componentName + '`. Validation failed.'
        );
      }
    },

    // You can also supply a custom validator to `arrayOf` and `objectOf`.
    // It should return an Error object if the validation fails. The validator
    // will be called for each key in the array or object. The first two
    // arguments of the validator are the array or object itself, and the
    // current item's key.
    customArrayProp: React.PropTypes.arrayOf(function(propValue, key, componentName, location, propFullName) {
      if (!/matchme/.test(propValue[key])) {
        return new Error(
          'Invalid prop `' + propFullName + '` supplied to' +
          ' `' + componentName + '`. Validation failed.'
        );
      }
    })
  },
  /* ... */
});
```
** 此外，getDefaultProps 方法可以用来设置组件属性的默认值
```
var MyTitle = React.createClass({
  getDefaultProps : function () {
    return {
      title : 'Hello World'
    };
  },
  render: function() {
     return <h1> {this.props.title} </h1>;
   }
});
ReactDOM.render(
  <MyTitle />,
  document.body
);
```上面代码会输出 “Hello World”

#### 七、获取真实的DOM节点

> 组件并不是真实的DOM节点，而是存在于内存之中的一种数据结构，叫做虚拟DOM virtual DOM. 只有当它插入文档以后们才会变成真实的DOM。 根据React的设计，所有的DOM变动，都先在虚拟dom上发生，然后再讲实际发生变动的部分反映在真实dom上，这种算法叫做DOM diff， 它极大提高网页的性能表现、 但是有时候需要从组建获取真实dom的节点，这时候就要用到ref属性。
```
var MyComponent = React.createClass({
  handleClick: function() {
    this.refs.myTextInput.focus();
  },
  render: function() {
    return (
      <div>
        <input type="text" ref="myTextInput" />
        <input type="button" value="Focus the text input" onClick={this.handleClick} />
      </div>
    );
  }
});
ReactDOM.render(
  <MyComponent />,
  document.getElementById('example')
);
```
// TODO
  

















