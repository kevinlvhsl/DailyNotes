## Mobx 

### 概念 & 原则

+ 概念

MobX 将会区分以下概念，你可以在之前的例子中已经见过，不过让我们钻得更深一些以了解更多的细节。
+ 1. 状态（State）

状态（State） 是驱动你应用的数据。 通常每个应用都会有自己独有的状态结构，就像todo元素列表中，有一个视图状态来表示被选中的元素。 记住，状态就像Excel的单元格一样持有一份数据。
+ 2. 衍生物（Derivation）

可以从状态中衍生出衍生物。 衍生物通常存在以下几种形式：
  + UI视图
  + 衍生数据，例如没完成的todo列表
  + 后台交互，例如发送变动给服务器
MobX区分两种衍生物
  + 计算值（Computed values） 这是一种可以根据当前被观察的状态，通过纯函数衍生出的新值。
  + 响应行为（Reactions） 响应行为是当状态发生变化时会自动执行的副作用（side effects），它们是响应式和命令式两种编程方式的桥梁。通常用于获取I/O
  当开始使用MobX时，人们喜欢大量使用响应行为。 黄金准则是：当你想要基于当前的状态创建一个新值时，使用计算值 computed
  类似Excel，公式计算是一种衍生物，用于计算某个值，而将这个公式显示到显示器上，则是一种GUI的响应行为。
+ 3. 行为（action）

> 任何导致状态改变的代码称为行为。例如用户事件、后端数据推送等等 行为可以帮助你的代码结构变得更清晰。 如果使用严格模式，则MobX会强制只有在行为中才能改变状态。
原则

MobX支持一个单向数据流：使用行为改变状态，以触发更新所有被影响到的视图。
Action -->  State -->  View

> 所有的衍生物，在状态改变时都会自动地、最小粒度地更新。作为结果不会依赖任何中间形式的值。
所有的衍生物，默认更新都是同步的。这意味着当状态改变后，行为可以直接检查（inspect）一个计算值。
计算值是懒（lazily）更新的。直到计算值真正被使用时，才会激活更新。当一个视图不再使用它时，它会被自动回收。
所有的计算值都应该是一个纯函数，不要用于改变状态。

举例

下面这个例子体现了上面的概念和原则：
```
import {observable, autorun} from 'mobx';

var todoStore = observable({
    /* 可观察状态 */
    todos: [],

    /* 一个衍生值 */
    get completedCount() {
        return this.todos.filter(todo => todo.completed).length;
    }
});

/* 一个对状态进行观察的函数 */
autorun(function() {
    console.log("Completed %d of %d items",
        todoStore.completedCount,
        todoStore.todos.length
    );
});

/* 一些改变状态的行为 */
todoStore.todos[0] = {
    title: "Take a walk",
    completed: false
};
// -> 同步打印 'Completed 0 of 1 items'

todoStore.todos[0].completed = true;
// -> 同步打印 'Completed 1 of 1 items'
```



### 核心 API
[文档](https://suprise.gitbooks.io/mobx-cn/content/best/autorun.html)

这是最重要的 MobX API。仅仅理解 observable, computed, reactions 和 actions 就足够让你掌握 MobX 并且在应用中使用它!
+ 创建可观察变量（observables）
```
observable(value)
@observable classProperty = value
```
observable 函数的参数可以是JS原始类型、引用、纯对象、类实例、数组和maps。 observable(value) 是一个方便而又强大的方法，他会尽可能地用最合适的类型来创建可观察变量。
