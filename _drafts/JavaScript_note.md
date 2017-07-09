---
---

# 基本流

+ 比较两个值是否相等，用 === 和 !===。更严格，错误更少。
+ JavaScript 有 switch case 语句。
+ 有 ? : 三元操作符。
+ textContent
+ 如果包含进文件中的多个 js 脚本中有相同的函数，则被调用的是后载入的那个。
+ document.createElement 方法只是创建一个节点，要让节点显示，还得用 document.body.appendChild。
+ 推荐使用 addEventListener 和 removeEventListener, 推荐将函数用匿名形式写进 addEventListener 的参数中。
+ 事件参数的 target 属性很有用，特别是在多个元素注册了同一个方法时。这时最好是利用 event delegation，只在（许多个同类子元素的）父元素上注册一个方法。
+ 事件对象的 preventDefault 方法可以阻止一些动作，比如错误信息的提交。
+ event bubbling，从最内部的元素开始，一层层往上检查元素有没有注册处理相应动作的方法，如果有则会逐一执行。调用事件对象的 stopPropagation 方法可以阻止事件继续向上传递。

# Object

+ eval 函数运行给定的 JavaScript 代码字符串。返回结果，或者结果为空就返回 undefined。
+ 用类似 Python 中的字典形式定义的对象称为字面对象（object literal）。定义中，可用同样的方式嵌套对象。
+ 除了可以用点号来访问成员之外，还可用中括号来访问，但其中需要用字符串，也就是单引号将成员名包含起来。object 有时也叫做关联数组（associative array）。
+ 上述方式不但可以获取值，也可以对已有的值更新。此外，还能通过同样的形式加入新的成员。而如果有键和值的对应，可以用中括号的方式，也就是字典形式来加入新成员，键、值分别为成员名称和成员值。这用点号没法做到。因为点号只能接受字面值，而不是变量值。
+ 类，或者模板？原型（prototype）其实也就是一个模板。原型对象也可以有原型，形成一条链子。
+ 当用构造函数创建一个新的对象实例时，域经典面向对象语言不同的是，并非所有的功能都拷贝到了新的对象，而是将功能通过引用链接起来，称为原型链（prototype chain）。所以严格地讲这不是真正的实例化，JavaScript 运用了不同的机制在对象间分享功能。
+ 定义对象的方式之一是写一个普通函数，其中定义一个对象，对其进行初始化之后返回它即可。
+ JavaScript 中的构造函数，也是用函数的方式定义，名称是类名，函数体则是对一系列的 this 成员赋值，同时不需要返回值。调用时要用 new 关键字。
+ 在调用构造函数时，其中的方法成员会在每次调用时定义。
+ 可以用 Object 构造函数来创建一个新对象。其可以有参数，比如将字面值传递过去，也可以没有。
+ 内建函数 create，可以基于一个已存在的对象创建新的。
+ 用构造函数创建的对象，其原型对象（prototype object）就是构造函数定义的类。
+ Object 有很多成员，而被继承的成员仅仅只是定义在 prototype 属性内的那些，可有理解为子命名空间，即以 Object.prototype 开头，而不是以 Object 开头的那些。prototype 属性的值也是一个（object）对象，基本上作为容器使用，存储我们希望顺着原型链继承下去的属性和方法。
+ 因此，定义类的构造函数，如 Object() 或 Person()，都有 prototype 属性，不过后者的 prototype 是空集。
+ 当前对象的原型对象引用，是 `__proto__` 属性, 而 prototype 仅仅只是希望被继承的部分。对于 person，`__proto__` 是一个 Object，包含了其可用的成员，而 Person、Object 的 `__proto__` 属性则为 function。
+ `Object.create()` 函数是以参数为原型创建新的对象，所以如果以 person1 为参数创建 person2，则后者的 `__proto__` 是 person1 的内容。
+ 每个对象实例都有一个 constructor 属性，指向创建该实例的原始构造函数。上例中 person1 和 person2 的 constructor 属性值都为 `function Object()`。而且 constructor 是函数，可用被调用。constructor 还有其他属性，如 name。
+ 对构造函数的 prototype 加入新成员，会让整个继承链动态更新，使得新方法对所有派生自此构造函数的对象实例都能用到。一般是定义方法，以及常量。在其中调用 this 会得到 undefined。
+ 一个非常通用的模式是在构造函数内部定义属性，可以用参数赋值；然后在构造函数的 prototype 属性上定义方法。
+ 继承一个类，是写一个新的构造函数，然后在函数体内调用继承类的 call 方法。this 参数是指新的构造函数。不管需要不需要参数进行初始化都要在构造函数中加入参数，这些将成为派生类的成员，在调用 call 时也要写上需要的参数。而实际上在之后的实例化时，完全可以不用参数。
+ call 方法定义于 Function.prototype 中，其调用一个函数，使用给定的 this 值和其他参数。在调用一个已经存在的函数时可用一个不同的 this 对象。this 指当前对象，调用者。利用 call，可用在其他对象中继承已有的方法，而不需要在新对象中再次编写。可以用来继承，也可以在循环中调用匿名函数，或者直接传递参数，用于给函数中的 this 赋值。
+ 之后用 Object.create() 对派生类的 prototype 属性赋值，其参数是父类的 prototype。但是仍然要让派生类的 prototype.constructor 指向自己，所以要其再次赋值。
+ JSON 要用双引号，这是最安全的。
+ 类的属性没法变成私有的，但是 var 变量（let 呢？）是私有的，而且在构造函数内声明的方法，在实例化时会生成复制体而各自独立。加上闭包的机制，可以组合这两者生成私有成员和相关操作。或者多加几个括号，用一个匿名函数来包装构造函数，同时匿名函数里面有 var 变量可以构成闭包，而构造函数仍然在 prototype 内声明函数。
+ 如果用函数包装加上闭包，需要加上一个序号数组，保存所有实例对应的那个私有变量。
+ Object.__proto__.__proto__.__proto__ === null
+ Object.prototype.__proto__ === null
+ ES2015 加入了 class 关键字，其中可以加入 constructor 方法。constructor 方法不能超过一个，在其中可用 super 关键字调用父类的 constructor。
+ class 中其他方法都是默认 prototype 的，对吗？加了 static 前缀的是静态方法。
+ extends 用于派生父类。如果子类中有 constructor，则其必须先调用 super。
+ 没有 constructor 的类无法作为 extends 的父类。这时可以用 Object.setPrototypeOf。
+ super 还可调用 constructor 以外的其他父类方法。
+ mixin， 多重继承，或者虚拟类继承。
+ 通过构造函数只得到属性，prototype 链需要另外显式地设置，构造函数没有此功能。
+ 使用 new 会得到对象中属性的副本，将其放进子类的 prototype 中，就是子类自己的值了。如果要所有子类都继承的成员，就不能放在构造函数中，而应该在外面声明为此构造函数相应的 prototype 的成员。
+ 每个对象都有 __proto__ 对象属性，每个函数都有 prototype 对象属性。使用 new 加上构造函数的形式会将后者的 prototype 赋值给前者的 __proto__。
+ 构造函数中可以调用另外的多个构造函数，但是实例的 prototype 只能指向一个，所以继承并不是多维的。修改其他的 prototype 也不会影响实例。
+ 直接在构造函数里面写 var 变量也是可以的。但如果这里面没有方法的话，还有意义吗？

# 语法和类型

+ 声明：var、let、const。
+ 7 个数据类型：6 个基础类型：Boolean、null、undefined、Number、String、Symbol 和 Object。
+ 字面值：数组、Boolean、浮点、整数、Object、RegExp、String。
+ 数组可以有缺失值，就是两个逗号连在一起可以。

# 控制流和错误处理

+ 从 ES2015 开始，JavaScript 支持 Promise 对象，允许控制延迟和异步操作流。
+ Promise 实例处于以下状态之一：pending、fulfilled、rejected、settled。
+ Promise 对象 prototype.then 方法，取得的就是构造对象时，resolve 函数的参数。

# 循环和迭代

+ for...in 和 for...loop。

# 函数

+ arguments.callee 是 arguments 对象的一个属性，可用来指向当前正在执行的函数，即在其函数体内递归调用。在当前函数是匿名函数是很有用。比如 map 的匿名函数参数。不过不推荐使用，绝大多数情况下用非匿名函数替代即可。
+ 可以在函数内嵌套函数。内部函数为其外部函数私有的，且其形成了一个闭包。闭包是一个表达式（一般为函数），其能够拥有自由变量及绑定这些变量的环境（是环境“关闭”了表达式）。
+ 内部函数仅能通过外部函数内的语句访问；内部函数构成了闭包：内部函数能够使用外部函数的参数和变量，反过来则不行。
+ 定义在外部函数内的变量和函数的生命周期会随着闭包函数的生命周期的延长而延长。
+ 函数的参数保存在数组形式的对象中，可用 arguments[i] 的形式访问。
+ ES2015 加入了默认参数，以及剩余参数。剩余参数允许我们将无限数量的参数表示成一个数组。形式是函数的最后一个参数有 `...` 前缀。和 arguments 对象的区别：arguments 不是真正的数组，而剩余参数是数组，意味着诸如 sort、map、forEach 或 pop 等方法可以直接应用。arguments 则有其他附加功能。
+ arrow function，=>
+ 在 arrow function 之前，每个函数都有自己的 this，如果内部函数要调用外部的 this，就必须事先将要调用的 this 赋值给一个 var 变量。
+ arrow function 形式简洁，没有自己的 this 属性，直接调用外部的 this。
+ 内建函数：eval、isFinite、isNaN、parseFloat、parseInt、decodeURI、decodeURIComponent、encodeURI、encodeURIComponent、escape、unescape。
+ 在 JavaScript 中，函数是第一类对象，因为他们能够拥有属性和方法，和任何其他对象一样。不同的是他们是 Function 对象。

# 表达式和运算符

+ 逗号运算符，计算所有其操作数的值，然后返回最后那个操作数的值。for 循环中多维数组处理比较常见。
+ typeof
+ void 计算操作数的值，但并不返回值。可用于控制链接行为。
+ in 和 Python 中的类似。
+ instanceof
+ 表达式是任何可以确定一个值的有效单位。
+ 用 () 将 {} 括起来，是为了让对象正确解析，而不是被当作代码块。这是唯一目的吗？
+ super

# 数组

+ Array.prototype 包含的方法，如 forEach 等，可用于类似数组的对象上。
+ 类型数组是用于处理二进制数据的，实现有 buffer 和 view。

# 有键集合

+ ES2015 加入了 Map 对象。使用 for...of 循环。
+ 过去的确将 Object 当做映射使用。
+ WeakMap
+ Set
+ Array.from
+ WeakSet 仅能存储对象的集合

# 迭代器和生成器

+ 只要有 next 方法的对象就是迭代器。
+ 生成器是一个特殊的函数，作为迭代器的工厂使用。其形式是 function* 声明加上函数体内部有 yield 返回值。
+ 可迭代（iterable）对象可以用 for...of 进行循环。为达此目的，需要实现 @@iterator 方法，即其需要一个属性，有 Symbol.iterator 键。属性的值可以是一个生成器。


+ 正则表达式 /the/gi，g 的意义是 global，返回所有匹配而不是第一个。 i 表示忽略大小写。
+ 单个数字 \d，多个 \d+
+ 空格 \s，包括 " ", " \r", "\n", "\t", "\f"。
+ 非空格 \S。


+ string 的 split 和 array 的 join 如果不要分隔符，必须显式地以 '' 为参数。
+ arguments 是个特殊的对象，直接调用即可，此时就不必管参数的名称了。
+ Array 的 sort，如果不给参数，就是按照字符串排序。
+ 浏览器自带的库就有得到当前位置的功能，navigator.geolocation
+ for...of 用于 iterable 对象。[Symbol.iterator] === for...of
+ function* yield
+ 用 Function.prototype.bind() 来改变函数的上下文。
+ 一般在别的函数内部，就是别人的 this，此时如果要在别人的函数体内调用某个函数的 this 成员，就必须要另外的绑定了。
+ 返回 null 可以阻止组件在父组件中的渲染。
+ 可以用数组的 map 函数生成 JSX 列表。
+ 创建列表时，需要加上 key 属性。key 仅用在数组里面生成元素的时候，也就是在 map 的里面。
+ key 只需要在其兄弟节点间是唯一的即可，不需要全局唯一。
+ 比较简单的事件处理可以合并成一个函数，只要用事件的目标进行区别即可。
+ react 的组件间的交互，是把统筹的任务交给组件共同的父元素完成。把 state 上提到父组件中，然后父组件向子组件传递的，除了参数外，还有事件处理方法，这样就能够在子组件中触发事件时，在父组件中实现状态的改变。也许和 Angular 的思想类似？
+ immediately-invoked function expression 利用 JavaScript 的函数域生成一个语法域。可防止 variable hoisting 和污染全局环境。也即 self-executing anonymous function。
+ 主要形式是将函数用小括号包围：`(function () {...}) (); (function () {...} ());`
+ 可加符号前缀强化：!, ~, -, +
+ 在期望放表达式的场合，比如逻辑运算，逗号队列中。
+ 可以包含有参数的函数。参数在末尾的调用参数中给出。
+ JavaScript 中， ~ 的作用是将其右边表达式的值 N，进行 -(N + 1) 的运算。使用场景：可以将字符串转换成整数。如果要保持其值不变，就应该使用 ~~；可以将 -1 转换成 0，这在数组查找返回 -1 时特别有用；但是要记住只能对整数使用。
