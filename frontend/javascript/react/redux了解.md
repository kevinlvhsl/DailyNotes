## redux是一个状态管理机，通过改变状态来改变视图 状态与视图一一对应
> Redux 的设计思想很简单，就两句话。
  + （1）Web 应用是一个状态机，视图与状态是一一对应的。
  + （2）所有的状态，保存在一个对象里面。
  
[内容来自--阮一峰写的redux入门](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_one_basic_usages.html)

### 基本概念和 API
####  Store
Store 就是保存数据的地方，你可以把它看成一个容器。整个应用只能有一个 Store。
Redux 提供createStore这个函数，用来生成 Store。

import { createStore } from 'redux';
const store = createStore(fn);
上面代码中，createStore函数接受另一个函数作为参数，返回新生成的 Store 对象。
这个函数 是一个纯函数(reducer)，只用来同步的改变状态，不包含异步操作或者与其他地理时间相关的因素。
```
import { createStore } from 'redux'
import { Provider } from 'react-redux'
import todoApp from './reducers'
<Provider store={store}>
    <App />
 </Provider>
```

#### State

Store对象包含所有数据。如果想得到某个时点的数据，就要对 Store 生成快照。这种时点的数据集合，就叫做 State。
当前时刻的 State，可以通过store.getState()拿到。
Redux 规定， 一个 State 对应一个 View。只要 State 相同，View 就相同。你知道 State，就知道 View 是什么样，反之亦然。

#### Action
用户通过操作view界面 触发action去修改state
Action 是一个对象。其中的type属性是必须的，表示 Action 的名称。其他属性可以自由设置
`const action = {
  type: 'ADD_TODO',
  payload: 'Learn Redux'
};`


#### Action Creator

View 要发送多少种消息，就会有多少种 Action。如果都手写，会很麻烦。可以定义一个函数来生成 Action，这个函数就叫 Action Creator。
```
const ADD_TODO = '添加 TODO';

function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  }
}

const action = addTodo('Learn Redux');
```
addTodo函数就是一个 Action Creator

#### store.dispatch
store.dispatch()是 View 发出 Action 的唯一方法。
store.dispatch接受一个 Action 对象作为参数，将它发送出去。
store.dispatch(addTodo('Learn Redux'));


#### Reducer
Store 收到 Action 以后，必须给出一个新的 State，这样 View 才会发生变化。这种 State 的计算过程就叫做 Reducer。
`const reducer = function (state, action) { return new_state;};`
```
const defaultState = 0;
const reducer = (state = defaultState, action) => {
  switch (action.type) {
    case 'ADD':
      return state + action.payload;
    default: 
      return state;
  }
};

const state = reducer(1, {
  type: 'ADD',
  payload: 2
});
```
import { createStore } from 'redux';
const store = createStore(reducer);
createStore接受 Reducer 作为参数，生成一个新的 Store。以后每当store.dispatch发送过来一个新的 Action，就会自动调用 Reducer，得到新的 State。
为什么这个函数叫做 Reducer 呢？因为它可以作为数组的reduce方法的参数。请看下面的例子，一系列 Action 对象按照顺序作为一个数组。
```
const actions = [
  { type: 'ADD', payload: 0 },
  { type: 'ADD', payload: 1 },
  { type: 'ADD', payload: 2 }
];
const total = actions.reduce(reducer, 0); // 3
```
上面代码中，数组actions表示依次有三个 Action，分别是加0、加1和加2。数组的reduce方法接受 Reducer 函数作为参数，就可以直接得到最终的状态3。

#### 纯函数
Reducer 函数最重要的特征是，它是一个纯函数。也就是说，只要是同样的输入，必定得到同样的输出。
**纯函数**是函数式编程的概念，必须遵守以下一些约束。
> + 不得改写参数
  + 不能调用系统 I/O 的API
  + 不能调用Date.now()或者Math.random()等不纯的方法，因为每次会得到不一样的结果
由于 Reducer 是纯函数，就可以保证同样的State，必定得到同样的 View。但也正因为这一点，Reducer 函数里面不能改变 State，必须返回一个全新的对象
```
// State 是一个对象
function reducer(state, action) {
  return Object.assign({}, state, { thingToChange });
  // 或者
  return { ...state, ...newState };
}

// State 是一个数组
function reducer(state, action) {
  return [...state, newItem];
}
```

#### store.subscribe()
Store 允许使用store.subscribe方法设置监听函数，一旦 State 发生变化，就自动执行这个函数。
> 只要把 View 的更新函数（对于 React 项目，就是组件的render方法或setState方法）放入listen，就会实现 View 的自动渲染。

store.subscribe方法返回一个函数，调用这个函数就可以解除监听。
let unsubscribe = store.subscribe(() =>
  console.log(store.getState())
);

unsubscribe();

### Store 的实现
 Store 提供了三个方法。
+ store.getState()
+ store.dispatch()
+ store.subscribe()
createStore方法还可以接受第二个参数，表示 State 的最初状态。这通常是服务器给出的
`let store = createStore(todoApp, window.STATE_FROM_SERVER)`
window.STATE_FROM_SERVER就是整个应用的状态初始值。注意，如果提供了这个参数，它会覆盖 Reducer 函数的默认初始值。
```
const createStore = (reducer) => {
  let state;
  let listeners = [];

  const getState = () => state;

  const dispatch = (action) => {
    state = reducer(state, action);
    listeners.forEach(listener => listener());
  };

  const subscribe = (listener) => {
    listeners.push(listener);
    return () => {
      listeners = listeners.filter(l => l !== listener);
    }
  };

  dispatch({});

  return { getState, dispatch, subscribe };
};
```


### Reducer 的拆分

Redux 提供了一个combineReducers方法，用于 Reducer 的拆分。你只要定义各个子 Reducer 函数，然后用这个方法，将它们合成一个大的 Reducer。
```
import { combineReducers } from 'redux';

const chatReducer = combineReducers({
  chatLog,
  statusMessage,
  userName
})

export default todoApp;
```
combineReducers()做的就是产生一个整体的 Reducer 函数。该函数根据 State 的 key 去执行相应的子 Reducer，并将返回结果合并成一个大的 State 对象。

#### 工作流
![](http://www.ruanyifeng.com/blogimg/asset/2016/bg2016091802.jpg)











