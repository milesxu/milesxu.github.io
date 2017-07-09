---
---

+ visibility 属性指定一个元素是否可见。值 hidden 可让元素不可见。但元素即使不可见，仍然会在页面上占据空间。使用 display 属性可以让元素不占空间。
+ display 属性指定元素使用的 box 类型。inline 类似 `<span>`；block 类似 `<p>`；flex 就是 flexbox；inline-block 表示元素本身是 inline 级别的 box，但是其内部元素是 block 类型的； inline-flex 是 inline 级别的 flex 容器；inline-table 是 inline 级别的表格；list-item 使得元素类似 li 元素；run-in 依据上下文选择 block 或者 inline；table 使得元素类似 table 元素，类似功能有 table-caption, table-column-group, table-header-group, table-row-group, table-cell, table-column, table-row；none 使得元素完全不显示；initial 将其值设置成默认值；inherit 继承自父元素。
+ position 可能的值：static, absolute, fixed, relative, initial, inherit。static 是默认值。元素按照其文档流中出现的次序渲染；absolute 使得元素与其第一个非静态的祖先元素相关联地渲染；fixed 则是相对于浏览器窗口渲染；relative 则依据其本来的位置进行偏移；initial 将其属性设置为默认值；inherit 则使其从其父节点继承。
+ overflow 属性指定当内容溢出元素的 box 时该怎么做。默认值是 visible， 内容会在元素的 box 之外显示；hidden 表示内容会被裁剪且多出的内容不会显示；scroll 表示内容会被裁剪但是会添加滚动条使得多出的内容可见，滚动条一直可见；auto 表示一旦出现裁剪，就会出现滚动条；initial 和 inherit 同上。
+ list-style-type 表示列表指示的形状，可能值：disc(default), armenian, circle, cjk-ideographic, decimal, decimal-leading-zero, georgian, hebrew, hiragana, hiragana-iroha, katakana, katakana-iroha, lower-alpha, lower-greek, lower-latin, lower-roman, square, upper-alpha, upper-latin, upper-roman, initial, inherit, none。none 表示没有标记。

# 选择器

+ descendant combinator, or white space character。如果有多个相同的子元素，则都会起作用。包括所有层数中符合条件的子节点。
+ child combinator, or >。只选择一层内所有符合条件的子节点。
+ adjacent sibling combinator, or +。选择具有相同父节点的相连的元素。
+ general sibling combinator, or ~。有相同的父节点，但不需要相连。
+ 以上 pattern，如果是 A B 为选择器，则都是匹配 B。另外，还是用 class name 匹配更好。出现意外的影响的可能性更低。
+ 属性选择器，匹配拥有特定属性或者属性值的元素。例子：`a[target], a[target="_blank"]`
+ `[attribute~="value"]` 匹配完整的单词，用空格分割的字符串。
+ `[attribute|="value"]` 匹配有连接符，前缀为 value 的值，或者仅有前缀的值。
+ 匹配子串：`[attribute^="value"]` 匹配起始子串，`[attribute$="value"]` 匹配结尾子串，`[attribute*="value"]` 匹配任意子串。
+ 应用：比如匹配一个电话号码，然后用 background 属性，给特殊的背景形状及图标。

+ *伪类* 让我们能基于区别于文档树的信息来定义对象的样式，或者是对不能用简单选择器来表达的对象定义样式。例如，一个元素仅能在用户与之交互时才有 hover 或 focus 状态。因此就有 :hover 和 :focus 伪类。
+ *伪元素* 能让我对没有直接在文档树中呈现的元素定义样式。如 HTML 中并没有 firstletter 元素，于是有了 ::first-letter。
+ 伪元素：`::before, ::after, ::first-letter, ::first-line, ::selection`。后三个影响源文档中的内容，前两个则注入内容。还有 `::spelling-error, ::grammar-error` 可用于拼写检查。
+ 伪类： `:not(), :lang(), :hover, :focus, :target`。用 :target 可以高亮属于页面 URL 中 # 之后对应的部分。用此属性可以用链接做 Tab 标签。
+ :not() 返回除了成功匹配的元素之外的所有元素。例子： `p:not(.message)`。多个 :not() 可以串起来使用。
+ 依照索引选择的伪类：`:first-child, :last-child, :only-child, :nth-child(), :nth-last-child()`。后两个接受的参数是： odd 或 even 关键字、整数如 2 或 8，或者形如 An+B 的形式，A 是步长，B 是偏移量。负数也可以用。
+ :empty 匹配真正的空，比如 `<p></p>`，加一个空格都不行。`p:not(:empty)`
+ + 以上伪类也能够匹配在文档子树中相应位置的元素。如 `p:nth-last-child(2)` 会匹配所有在其父容器中位列倒数第二且为 p 的元素。
+ 类型化子索引伪类：`:first-of-type, :last-of-type, :only-of-type, :nth-of-type(), :nth-last-of-type()`
+ 例子：`p:nth-of-type(5)` 会匹配所有 p 元素，然后从中查找第五个元素。
+ `p:first-of-type::first-letter` 即可只让第一段第一个字符大写而不是每一段第一个字符。
+ `:enabled, :disabled` 匹配拥有或者缺少 HTML5 中的 disable 属性的元素。
+ `:required, :optional` 匹配出现或缺少 required 属性的元素。
+ `:checked` 仅对 radio 和 checkbox 有效。`[type=radio]:checked + label`
+ `:in-range, :out-of-range` 能和 range, number, date 一起用，需要元素设定最大最小值。
+ `:valid, :invalid` 可用于格式检查。串起来使用：`input:focus:invalid`。

# CSS 架构和组织

## 结构举例：

+ reset.css 复位和正规化的样式，最小化颜色、边框或字体相关的声明
+ typography.css 字体名称、粗细、行距、大小，以及 body 和 heading 的字体样式。
+ layout.css 管理布局和分段、网格的样式。
+ form.css 表单控件和标签的样式
+ lists.css 列表特定的样式
+ tables.css 表格特定样式
+ carousel.css 传送带（carousel）组件需要的样式
+ accordion.css 手风琴（accordion）组件需要的样式

## 编写干净 CSS 的黄金准则

+ 避免全局和元素选择器
+ 不要用过度特定的选择器，不要串着使用 class name，就是两个类紧挨着使用。可以声明两个类。避免使用 id 选择器。class name 选择器是用 . 开头，id 选择器是用 # 开头。如果是全局不变的甚至是跨站不变的样式，可以用 id，避免被覆盖。
+ 使用语义明显的类名（class name）
+ 不要让 CSS 和 标记结构过度耦合。因为如果 HTML 要改名字，那么 CSS 也要跟着改。其实用类名也一样可以用父子关系符号的，所以类名更好。

BEM: Block-Element-Modifier，把页面分成块，每个块有不同的元素。一个项目内块的名称必须唯一，一个块内元素的名称必须唯一，块的变化，要体现在名称上。变化以原来的元素样式为基础，也就是 HTML 的元素类名有两个，空格分开。

# 调试与优化

# 复杂布局

## 盒子模型（box model）

+ 也许理解 CSS 最重要的一点是：所有东西都是一个盒子（box）。任何文档中的元素生成一个 box。盒子可能是 block-level box 或者 inline-level box。盒子的类型决定了元素如何影响页面布局。
+ 默认情况下，p、section 等元素创建 block-level box，而 a、span、em 等创建 inline box。SVG 不使用 box 模型。
+ block-level box 根据它们源位置垂直地进行渲染，并且横向扩展填满包含它的元素的可用宽度（table 除外）。即为 normal flow。block-level box 有一个 display 属性，可能的值为 block、list-item、table 或者任何 table-* 值（如 table-cell）。
+ inline-level box 相反，并不形成内容的新块。这些盒子构成了一个 block box 当中的行。它们水平显示，填满包含它的 box 的宽度，如果必要也会换行。inline-level box 的 display 值可以是 inline、inline-block、inline-table 或 ruby。
+ 盒子的维度是盒子内内容区域、padding 宽度和边框宽度的总和。margin 宽度为元素创建了一个 margin box，且会影响文档中的其他元素；然而 margin 宽度对 box 的维度没有任何影响。
+ 与大多数浏览器认为 width 即为内容区域的宽度不同，IE 5.5 认为三个加起来的和为 width 值。CSS 中引入了 box-sizing 属性来实现这个效果。
+ box-sizing 在 CSS3 中定义，有两个可能的值： content-box 和 border-box。前者是默认值，后者符合 IE 5.5 的设定。后者推荐使用，最好放在复位规则中，即 html 下面。
+ `*, *:before, *:after { box-sizing: inherit; }` 或者直接写 border-box。
+ margin collapse（边界折叠）：当两个 box 彼此相邻时，它们之间的距离是它们相邻的边的 margin 中 *较大* 的那个，而不是它们的和。
+ float 的本意就是让原本垂直排列的多个组件横向排列，所以只用 float 即可达到目的，不需要 inline-block 的帮助。
+ 无法在没有 float 的元素上创建 margin 属性使之与 float 元素分开。解决方案是在中间再加一个隐形的块。

## 用 position 和 z-index 管理层（layer）

+ 文档中的每个元素参与到一个堆栈上下文（stacking context）之中。堆栈上下文是一个模型，一组规则，用于规定元素如何显示在屏幕上。
+ html 元素创建了 root stacking context。某些 CSS 属性和值也会为它们应用到的元素。触发 local stacking context。
+ 从下到上的顺序是：z-index 为负值的；没有位置设定的元素；堆栈层为 0 的，包括 z-index 为 auto；z-index 值为正值的。如果两个元素有相同的堆栈层，它们将依据它们在源 HTML 中的位置叠层，后出现的较高。
+ 当某个元素的 opacity 属性值小于 1 时，其会创建一个新的 stacking context。这样它的子元素的 z-index 设定就变得和其父元素相关而不是和根上下文相关，设定了也没用。
+ rgba(), hsla(), transition

## 使用 CSS Multicolumn Layout

+ 多列布局允许文字和元素从一列流向另一列，自动调整 viewport 或者 container 的宽度。
+ 使用 columns 属性即可让容器实现多列，它是 column-width 和 column-number 的整合速记。
+ column-gap 用来设置列之间的间距，column-rule 可以在列之间绘制分割线。分割线不会增加间距的宽度，而是在间距的中间显示，如果其比分割还宽，就会延伸到列的内部。
+ 图片的宽度不会超过列的宽度，超出的部分会被裁剪。加入 `width: 100%` 可以让图片正常缩小到适合列宽的大小。
+ column-span 控制某个元素是否横跨多个列。目前只有两个值：none 或者 all。
+ break-inside 属性用于多列容器的子元素。avoid-column 就能使得子元素都完整地存在于一列中。
+ break-before 和 break-after 可以选择元素，在其之前或者之后分割到不同列。可以取的值为 column 或 always。可以结合之前的 nth 选择器来用。
+ columns 可以加入 height 限制，最好同时加上 `column-fill: auto/balance`。
+ 多列对组件来说很好，整体页面不推荐。

## 用 Flexbox 创建灵活的布局

+ 灵活布局基本的使用方式是创建`display: flex` 或 `display: inline-flex` 到包含元素中。这时，其直接子元素都变成 flex items。如果没有其他属性设置，每个flex item 会有相同的高度，其值等于最高的元素高度值；水平得堆叠，每个 box 的边界之间没有空隙。
+ 用此法可以使得元素能够很好地水平排列，也就是 foundation 中的 row？
+ `flex-wrap: wrap` 可以让 flex items 在超出容器范围的时候跳到下一行。对容器内的元素设定 `flex: 0 0 25%` 或者诸如此类就可以控制每行几个元素。`flex: 1 0 25%` 会让元素填充空白区域。还有 wrap-reverse。
+ `justify-content: space-between, justify-content: space-around, justify-content: center || flex-start || flex-end`
+ 利用 flexbox 创建网格比使用其它方法需要的标记和样式都少许多。
+ 使用 flexbox 还可以创建灵活的、垂直对齐的表单组件。
+ flex 实际上是三个属性的速记：flex-grow 指示元素是否有必要增长，值非负，默认为 0；flex-shrink 指示一个元素是否有必要减少大小，必须为整数，默认为 1；flex-basis 指示初始化或最小宽度（当 flex 轴是水平时）或高度（当 flex 轴是竖直时），可以是长度或者百分比或 auto，初始值是 auto。极力推荐只用 flex。
+ order 属性确定了 flex item 在屏幕上显示的顺序，其值必须是整数，初始值是 0。
+ 在有 flex 的前提下，只需一句 `align-items: center` 即可让所有元素垂直居中。进一步地，如果要消除换行后两行间的空隙，可以加上 `align-content: center`。
+ `align-items: flex-start || flex-end || center || stretch || baseline`
+ `aline-self: auto || flex-start || flex-end || center || baseline || stretch`
+ flex-direction 属性定义 flex item 们一个接一个排列的轴，默认值是 row，可以改为 column。还有让排列顺序方向的值：row-reverse, column-reverse。
+ flex-flow 是 flex-direction 和 flex-wrap 的速记。
+ 对于 flex item，可以用 order 重新定义顺序，浏览器会将它们按照 order 定义的顺序显示，而不是标记源的顺序。原理类似 z-index。
+ flex-basis 可以定义每个 item 的默认宽度。

# 过渡和动画

+ 过渡定义起始和终了状态，浏览器会填充中间的状态；动画则定义的是中间的状态并控制动画如何进展。
+ 只有能够插值，接受 interpolatable 值的属性可以做动画或者过渡。
+ transition 接受时间长度值。如 1s。
+ 用 JavaScript 语句 `toggle.('change')` 可以触发元素的过渡效果。
+ transition 是以下属性的速记：`transition-duration, transition-property, transition-timing-function, transition-delay`
+ 所有 timing function 都是 cubic-bezier() 的简写。
+ 在 transition 中可以加入要过渡的元素属性，后面紧跟过渡的方式，多个过渡用逗号隔开。
+ 元素有 transitionend 事件，可以用 JavaScript 追踪。每个 transition 都会触发 transitionend 事件，如果要辨别，就用参数 `eventObject.propertyName` 进行辨别。
+ 动画如果不能演示则会有严重后果，可用 JavaScript 代替。动画可以无限重复，过渡总是有限的。动画使用关键帧，可以创建更复杂的效果。动画可以在播放循环中暂停。
+ 用 @keyframes 定义一个动画，然后在某个样式中，在 animation 属性中引用其名称。定义中可以用 from 和 to，也可以使用百分比定义关键帧。

# CSS 变形

# 根据条件应用 CSS

+ @media 的类型，可以是 `all, screen, print, speech`。在其大括号内，再写各元素的样式。
+ 但是 @media 真正强大的地方，是进行 Media feature 的查询。例子：`@media (width: 30em){}, @media screen and (width: 30em){}`。还有查询：`max-width, min-width`。事实上，可以和 min- 和 max- 搭配的 media feature 有：`aspect-ratio, device-aspect-ratio, color, color-index, height, device-height, monochrome, resolution, width, device-width`。
+ discrete media feature：

| Property | Acceptable Values |
|---|---|
| grid | Boolean (grid) |
| hover | none \| on-demand \| hover |
| any-hover | none \| on-demand \| hover |
| inverted-colors | none \| inverted |
| light-level | dim \| normal \| washed |
| overflow-block | none \| scroll \| optional-paged \| paged |
| overflow-inline | none \| scroll |
| orientation | portrait \| landscape |
| pointer | none \| coarse \| fine |
| any-pointer | none \| coarse \| fine |
| scan | interlace | progressive |
| scripting | none \| initial-only \| enabled |
| update-frequency | none \| slow \| normal |

+ @media 是可以嵌套的，这样可以一个情况中加入多于一个的情况。
+ 可以使用 not 关键字来否定一个媒体查询。它在所有查询的前面且否定整个查询。不过可以用逗号隔开不同查询，则每个查询可以有一个 not。
+ 可以在 import 中用媒体查询：`@import url(typography.css) screen, print;`更详细的查询也能加入。
+ import 的问题：对于使用 HTTP/1.1 的浏览器或服务器，使用 import 意味着多一个 HTTP 请求。
+ HTML 元素 style, link, video, source 都有了 media 属性，可以加入媒体查询。source的用途就是针对不同窗口载入不同图片。
+ 媒体查询的 JavaScript API 是 `[window.]matchMedia()`。
+ @support
+ @font-face 有 font-family, src 元素，后者可添加 url。还有 unicode-range 属性。

# 将 CSS 应用于 SVG

# 预处理器

+ Less 中 @ 定义变量，Sass 中是 $。
+ 变量替换，Sass 中是 #{}，Less 中是 @{}。
+ LESS 中 mixin 就是一小段代码，如果没有括号，就自己本身也是一个 CSS 样式，如果有括号，则有类似函数的功能。
+ Sass 中 mixin 用 @mixin 前缀定义，不会生成单独的 CSS 块。

# HTML + CSS

+ `<fieldset>` 是 HTML5 新属性，用于将 form 中相关联的元素分成一个组，并在这些元素周围绘制一个边框。`<legend>` 标签可以为 `<fieldset>` 定义标题。
+ `data-*` 属性用来存储私有与页面或应用的自定义数据，使我们能够在所有 HTML 元素中嵌入自定义的数据属性。
+ 目前的浏览器都会将 `<q></q>` 元素渲染成对应语言的引号。
+ 与 radio 类型联系的 label 有一个 .label-radio 类。
+ label 的 for 属性应该和关联元素的 `id` 属性一致。
+ `header` 元素，一组用于介绍或者对导航有帮助的部分。可以用在很多地方，包括页面开头。
+ `<section>` 元素表示文档或应用程序中的一个通用部分。有鉴于此，一个 section 应该是有主题的内容的划分，经常有一个标题。
+ `article` 元素表示文档、页面、应用程序或网站中一个完整的或者自包含的成分。原则上是可独立分发的或者重用的。
+ `nav` 就是一组导航链接。主要还是用于导航。nav 可以放到 `header` 里面。
+ `aside` 是页面中和内容无关的部分，可以被认为是和内容分离的部分。
+ `footer` 表示脚注或者版权之类的信息。
+ `main` 元素，表示页面中心主题的部分。整个页面只能有一个。
+ `figure, figcaption` 元素，figure 元素可用于标注示意图、图表、照片、代码段，等等。figurecaption 元素是给 figure 内的内容加标题的简单方法。
+ `mark` 元素表示文档中的一段标注或高亮用以表示引用的文字，因其与其他上下文相关。
+ `progress` 用于描述一个还未完成的、正在变化的进程的当前状态，不管完成状态是否被定义。
+ `meter` 元素表示一个元素，其范围已知。例子如果磁盘用量。6 个相关的属性：`max, value, min, high, low, optimum`。
+ `time` 元素
+ 标记出版物名称不要用 i 或者 em 元素，应该用 cite。
+ `dl, dt, dd` 表示 description list，用来表示名称和定义。
+ blockquote 有 cite 属性，给出引用的网址。内联引用则用 q 元素，同样有 cite 属性。但是基于目前浏览器支持情况，最好是用 a 元素包含一个 cite 标签。
+ `details, summary` 元素，表示类似 accordion 的结构，summary 只能是 details 的子元素且是第一个子元素。最开始只显示 summary 中的内容。
+ `ol` 元素，有序列表，有 start 和 reversed 属性。
+ style 的属性 scoped，表示当前嵌入的 style 只对父元素的子元素有效。
+ script 元素有 defer 和 async 属性。
+ picture 元素可以定义多个图片源。其子元素是 source，同时也是 video 和 audio 的子元素。还有属性 srcset, sizes 等等。后两者可用于 picture, img, source 等等。
+ `dialog` 元素表示对话框等
+ `download` 是 a 元素的新属性，表示文件应该被下载而不是浏览。可用在 PDF 文件链接上。
+ `iframe` 元素有新属性 `sandbox, seamless`。sandbox 让外部页面有各种限制，而 seamless 让 iframe 内容和父文档更紧密地联系，更无缝地改写其样式。
+ `menu` 元素和其 `menuitem` 子元素，可用于创建可交互命令的列表。
+ `address` 元素，可以标记联系信息。
+ video 元素，controls 属性控制是否出现控制条，这是自定义控制条的方法吗？
+ a 有 download 属性，可以给下载链接提供一个默认的文件名。a 的 mailto 中，不仅可以给出邮件地址，还可以给出主题 subject 以及内容 body。还有 cc ？
+ abbr 用来显示缩写的全称。
+ code 用来表示代码；pre 中的空格全部保留；var 用于标记变量名；kbd 用于标记键盘输入等；samp 用于标记计算机程序输出。
+ time 标签可以用来显示时间，其 datetime 属性给出显示的格式。

## 内容分类

+ 元信息内容：不在页面上呈现的数据，但是会对页面产生影响。包括：title, link, meta, style。
+ 流内容：基本上包括了 HTML 文档中的每个元素，包括 header, footer, p。
+ 分节内容：一个内容块，包括 article, aside, nav, section。
+ 标题内容：h1, h2, 等等。
+ 短句内容：即 inline 内容，包括 em, strong, cite。
+ 嵌入式内容：img, object, embed, video, canvas。
+ 交互式内容：表单。
+ 比较好的页面分布，包括对有残疾的用户的帮助：页面的编排应该是：header、nav、main，其中包含 article、section 或者 div、aside，经常包含于 main 中；footer。
+ 有意义的内容图片应该使用 HTML 的 img 标签；没有语义上意义，纯属装饰的图片应该使用 css 的 background-image。
+ 关于表格，col 和 colgroup 分别能够选取一个列和多个列，可以利用他们对单个的列进行统一的样式修饰。

## 表单

+ required 属性对除了 `button, submit, image, range, color, hidden` 之外的任何 input 类型都有用。
+ placeholder 属性允许一个简短的提示，显示于表单元素之内。
+ pattern 属性允许提供一个正则表达式来匹配用户的输入，以此判定是否合法。
+ title 属性提供 tooltip。
+ disabled 属性可用于除了 output 元素之外的任何表单控件之上。
+ readonly 属性类似 disabled，但是可获得焦点以及会提交其值。
+ multiple 属性表示一个表单控件中能输入多个值。可用于 select, file, email, range 输入类型。
+ form 属性可以将表单元素和它们嵌入的表单之外的表单联系起来。
+ autocomplete 属性指定了表单或者一个表单控件是否具有自动完成功能。默认值是开的。对身份验证的地方最好关掉，如 CAPTCHA。
+ datalist 元素和 select 非常相似，有很多选项，每个都放在一个 option 元素内。可将 datalist 同一个 input 联系起来，即其 list 属性，要和 datalist 的 id 一致。
+ 如果想要自定义的文件选择对话框，不用它就行了吧？
+ autofocus 属性指定一个表单控件应该在页面载入后尽快获得焦点。不推荐使用。
+ 输入类型：`text(default), checkbox, password, submit, button, file, hidden, image, password, radio, reset, submit, search, email, url, tel, date, time, number, range, color, datetime-local, month, week`
+ number, range 输入类型有 min, max, step 属性。
+ keygen 元素是用来生成公有-私有密钥对及提交公钥的控件。有 challenge 和 keytype 属性。

# 想法和心得

+ 可以用 radio 来实现标签。把标签和内容放在同一个父类容器里，可以用 css 的 + 和 ~ 进行访问并设定相关属性。然而觉得，其实也可以用 JavaScript 做到，不知是否能够更加简洁。
+ 内容总体容器的 position 为 relative，而每个 Tab 的内容容器的 position 为 absolute。
+ 也可以用 ul 及 li，然后 radio input 和其对应的内容都放在一个 li 之内。Tab 标签是 radio 的 label，应设置 float 属性，display 为 block，position 为 relative。
+ 隐藏 radio 最好的方式是 `visibility: hidden`
+ Tab 内容容器也可以用 display 属性来调整，反正每次只显示一个，其他的是不载入还是隐藏关系不大。
+ 如果要页面变窄时字体消失，可以让字号变成 0。
+ 用 `overflow: hidden` 加上平常宽度减少，hover 后宽度增加，可以做出类似 accordion 的效果。是不是可以用来做菜单？
+ overflow 应该可以用来做图片显示器，需要用到裁剪的地方非常多。
+ radio 可以用来做 Tab，因为只有一个显示；而如果可以让多个列都能够显示，也就是比较简单的 accordion， 就可以用 CheckBox 来做了。而如果每次只显示一个的 accordion，也可以用 input radio 来做。
+ 用 ul 和 链接也可以做 accordion，但是会添加很多的后退页面。
+ 如果不用这些，仅用 div 和 JavaScript，就是写好所有 CSS 样式，然后 addclass 或者 removeclass。
+ padding-top 如果用百分比和 width 是相关的，可以做成固定宽高比例的 box。
+ 隐藏和取消隐藏：`max-height: 0; max-height: auto`
+ 做时间线，用 before 和 after，因为只是一条线而已，不是文字。文字框也不难，就是左右浮动，使用 float。after 和 before 还用来呈现箭头，以后肯定会用到。除了浮动，要定义好其他所有样式，再用一个 invert 类，继承已经定义的，而只改一个浮动属性即可。划线要用 `display:table`。 *要反向可以用 `nth-child(even)`，要活用！*
+ 时间线还需要用到的样式是 clear，其不允许浮动的元素出现在指定的边上。这里需要的是 both。
+ 一排导航用竖线分隔的方式很简单，一个无序列表，然后每个元素的 before 伪类加上 “|” 的 content 即可。
+ 典型的一个主页面内容，即在 `body` 内的内容，可以分为三个部分：header、main、footer。
+ line-width 和 div 的高度不一致（或者不能整除？），就不能让文字和图标垂直居中。
+ 把一些需要 label 的 input 组件包含在 label中。
+ margin 也是一样可以影响组件的宽度的，应该是设置了 box 的原因。margin 可以取负值，这就是所谓的出血？
+ 样式表中，后定义的会覆盖先定义的样式。id 的样式会覆盖 class 的样式，而内置 style 又会覆盖 id 的样式。而带有 !important 后缀的样式又会覆盖前者。其优先级最高。
+ MDB 中的背景遮罩是用两个元素实现的，一个元素（父？）实现背景图片，另外一个元素（子？）实现背景色的改变，主要必须要设置不透明度，比如 rgba 中的 alpha。
+ float 属性指定当前 box 是否需要浮动。position 是 absolute 的元素会忽略 float 属性。在一个浮动元素之后的元素都会浮动。为避免这样，使用 clear 属性或者 clearfix hack。
+ `.clearfix::after { content: ""; clear: both; display: table; }`
+ top 属性对 absolute 和 relative positioned 元素有不同的作用，而对 static positioned 元素无效。top 的意义对于 absolute positioned 元素而言，是其对于其最近非 static positioned 父元素的最高点的距离。所以对于下拉菜单而言，top: 100% 就是紧跟着父元素排列的意思。
+ align-items 的确是用来将 flexbox 内的子元素进行垂直对齐的，但是要出效果，必须确保其高度有足够的余地。通常需要显式地设置具体数值，100% 不一定总是有用。
+ 如果要让 body 的高度变成 100%，一定要将 html、body 一起附上高度 100% 的样式。
+ flow-direction、align-items、justify-content 可以结合起来，将多个元素垂直居中排列。另外的可能是用 top，或者 ul 组合多个元素。
+ em 是根据元素最近的设置了 font-size 的父元素，可以是自己设置的字体值来进行计算；而 rem 总是根据根设置，也就是 html 元素的字体大小来进行计算。两者要活用，都有各自的优势和缺点。另外，Firefox 或者说 SVG 标准并没有设置 rem 单位，却有 em 单位。
+ 不过 SVG 元素也接受 CSS 样式的大小设定。也许可以把大小这些东西放到 CSS 文件中去。
+ span 元素默认是 inline 的 display 属性，是不可以接受大小的设定的。如果需要设置，应该将其 display 属性设置为 block 或者 inline-block。
