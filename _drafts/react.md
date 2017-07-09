---
---

+ class Name extends React.Component{ constructor, render} ReactDOM.render()
+ componentDidMount, componentWillUnmount
+ 元素都是不可更改地，一旦渲染就是一个固定的画面。如果要动，就得用一个函数包裹元素和渲染元素的函数，然后周期性地调用此函数。
+ 组件类似 JavaScript 的函数。他们接受任何输入，输入通过 props 调用。
+ 也可以用 ES2015 的 class extends，然后写自己的 render 函数。
+ 元素中也可以用组件标记，此时标记中的属性全部传递给组件。组件名首字母必须大写，以和普通 DOM 元素区别。
+ 组件必须返回单个根元素。所以如果有多个组件，最终要被一个 div 包裹。
+ 所有 React 组件必须像纯函数那样对待它们的 props 对象。
+ 将一个类似函数的组件转换成 class：建立一个扩展了 React.Component 的 ES6 class；添加一个 render 方法；将函数体内容移入 render 方法；在 render 方法体内，将 props 改成 this.props；删除函数声明。
+ 在类中加入状态：将 this.props 改成 this.state；加入一个 constructor，其中会初始化 this.state；之前的 props 作为 constructor 的参数；有了自己的 state，外面的函数即可删除组件标记内传递的属性；然后用组件的生命周期方法来控制改变。比如第二条中的方法。
+ 将 setInterval 赋值给一个 this 成员，是为了以后能够对其调用 clearInterval。
+ 直接对 this.state 成员赋值不会引起再次渲染。要达到目的，用 this.setState；多个 setState 调用可能会批量成为一个单个的更新。
+ 因为更新很可能是异步的，所以不能依赖其值产生下一个 state 的值。解决方案是传入一个函数，以之前的 state 为参数，加上更新逻辑。
+ state 能且仅能被拥有它的组件访问和修改。如果要将 state 值传递给子组件，将其值放在调用子组件的 props 对象中。
+ React 中事件名用 camelCase 形式，用 {} 的形式传递方法名。
+ 事件处理，在 class 的 constructor 内加上 this.handleClick = this.handleClick.bind(this)，绑定的过程主要给事件处理函数内的 this 赋值。
+ 只要不在调用时使用 ()，则必须绑定。
+ 分两步构建，首先写静态逻辑，这是需要大量代码而少许思考的过程。此时不需要用到 state，只用 props 就足够了。state 是仅仅用于交互的。
+ 从父组件传递来的 props 不是 state；不随着时间变化的数据不是 state；能够经由其他 state 或者 props 计算得到的不是 state。
+ 找到应该使用 state 的类的步骤：确定每个基于此 state 进行渲染的组件；找到它们的公共祖先；此组件或组件的更高级父组件可拥有 state；如果找不到一个有意义的组件来存放 state，可以创建一个新的满足前述条件的组件。
+ shouldComponentUpdate 方法，只对需要重新渲染的状态变化返回 true。
+ 高阶组件是一个函数，其以一个组件为参数，并返回一个新的组件。好处是可以减少完成同类任务的代码量，比如访问数据库的动作类似，只不过数据源不同。
+ 除了类组件，也可以有函数组件，其以一个 props 类为参数。在定义后，之后的声明式的调用中给出相应的类的成员值即可。
+ 在同时包含有开始标记和结束标记的 JSX 表达式中，被这些标记包围的内容会用一个特殊的 prop 传递：props.children。而且，除了寻常的 HTML 元素和 react 组件，还可以是一个可以调用的函数。

+ 应该是，在 state 中放入足够完成重渲染的选项即可。其他的即可以到时计算，也可以另外存于实例变量中。因为只要调用 render 函数，一切都会读取。但是对实例变量的更改，又不一定需要重新渲染。
+ 对于表单、动画、流媒体播放等任务，可以用 ref 让父组件直接调用子组件的方法。*但是，只在必须的时候使用。*
+ 如果要连续更新而且不能放在一个 setState 中的，串在一起很可能没用。最好用 componentDidUpdate。
+ react 写的 JavaScript 程序，所以除了其提供的类库，其他一切类库也可以在适当的地方使用。比如在 componentDidMount 方法中加入 addEventListener 方法，这样有很多任务不需要和父组件交互即可完成。
+ 那么再进行推广，其他函数，比如 querySelector 等等，也都可以使用了，所以可以操作很多元素。*不过子元素的事件，给父元素注册后，不要忘了在事件处理中写 stopPropagation 方法*。
