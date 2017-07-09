---
---

+ {{}}, v-bind, v-if, v-for, v-on:, v-model, v-once, v-html
+ Vue.component()，component 和 app 是分开的。
+ new Vue 是建立一个新的 View Model。
+ 每个 Vue 实例都代理了其 data 对象的所有属性。
+ Vue 实例有很多 $ 开头的有用方法。
+ Vue 实例有很多生产周期的钩子，可以用函数为其赋值，在特定阶段执行。没有专门的 Controller，控制逻辑就应该分散在生产周期的钩子中。
+ 除了 data，还可以有 computed 属性，是一个个的函数，返回处理的结果。
+ 还有 methods 对象，可以放入方法。方法和计算属性可达到相同结果，不过后者是有缓存的，只在依赖值改变时重新计算。所以应该尽量使用后者，除非不需要缓存就用方法。
+ watch 属性，是更通用的观察数据改变并作出反应的方法。但是 watch 仍然没有 computed 简洁。
+ computed 属性还可以包含 get 和 set 两个方法。get 是从依赖的值来计算结果，而 set 就是反推，去更新依赖的值。
+ 在需要进行异步操作或者资源消耗大的操作应该用 watch。
+ v-bind:class="{}" 来绑定类。里面可以有多个键值对。可以同时声明 class 特性，会自动放到一起。甚至可以把一整个类放到括号里面。也可以用 computed 属性。也可以是数组参数。
+ v-bind:style
+ 在 template 元素中 v-if，可以控制一大块代码。可以加上 v-else、v-else-if。可对元素用 key 属性进行区别。
+ v-show
+ v-for="item in items", v-for="(item, index) in items"。v-for 也同样可以用在 template 元素中以及 Component 中，然后展现一大块的内容。循环的也可以是一个对象。尽可能给每个 v-for 配一个 :key。可以用 computed 属性对 v-for 过滤。

+ Vue.component('name', {//options})
+ 选项中有 template，data。data必须是一个函数。
+ 父组件通过对子组件的属性赋值，向子组件传递信息。可以在子组件上使用 v-bind。要传递数据类型就得用这个。
+ 子组件通过事件向上传递信息。在自己的方法中调用 $emit。
+ 两个非父子关系的组件可以通过建立一个 bus 来传递事件。
+ 任何存在于父模板中的元素都编译到父组件域内；任何子模板则编译到子域。
+ components 属性可以包含多个 组件。然后使用 <component> 元素切换。
+ 可以用 <keep-alive> 包含 <component> 使得来回切换变得迅速。
+ component 可以写成一个异步的函数，最终 resolve 得到内容。

# slot

+ 在子组件内部创建 slot 元素。父组件放在子组件中间的内容，会放到 slot 的位置，如果子组件没有 slot 则这些内容被丢弃。
+ slot 可以有名字 name，而且有名称的 slot 可以和默认的 slot 放在一起使用，名称对应，没有名称的就塞到默认的 slot 中。
+ 在子组件内部可以联合 template 和 scope 使用。作为列表组件很有用。template 定义列表的格式，slot 则定义 v-for 的具体逻辑。
