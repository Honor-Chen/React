# 初探 React

## ReactJS简介
+ React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设 Instagram 的网站。做出来以后，发现这套东西很好用，**就在2013年5月开源了**。
+ 由于 React 的设计思想极其独特，属于革命性创新，性能出众，代码逻辑却非常简单。所以，越来越多的人开始关注和使用，认为它可能是将来 Web 开发的主流工具。
+ library
+ Framework


## 前端三大主流框架
+ Angular.js：出来最早的前端框架，学习曲线比较陡，NG1学起来比较麻烦，NG2开始，进行了一系列的改革，也开始启用组件化了；在NG中，也支持使用TS（TypeScript）进行编程；
+ Vue.js：最火的一门前端框架，它是中国人开发的，对我我们来说，文档要友好一些；
+ React.js：最流行的一门框架，因为它的设计很优秀；
+ windowsPhone 7    7.5   8   10


## React与vue.js的对比
### 组件化方面
1. 什么是模块化：从 **代码** 的角度，去分析问题，把我们编程时候的业务逻辑，分割到不同的模块中来进行开发，这样能够**方便代码的重用**；
2. 什么是组件化：从 **UI** 的角度，去分析问题，把一个页面，拆分为一些互不相干的小组件，随着我们项目的开发，我们手里的组件会越来越多，最后，我们如果要实现一个页面，可能直接把现有的组件拿过来进行拼接，就能快速得到一个完整的页面， 这样方**便了UI元素的重用**；**组件是元素的集合体**；
3. 组件化的好处：
4. Vue是如何实现组件化的：.vue 组件模板文件，浏览器不识别这样的.vue文件，所以，在运行前，会把 .vue 预先编译成真正的组件；
 + template： UI结构
 + script： 业务逻辑和数据
 + style： UI的样式
5. React如何实现组件化：在React中实现组件化的时候，根本没有 像 .vue 这样的模板文件，而是，直接使用JS代码的形式，去创建任何你想要的组件；
 + React中的组件，都是直接在 js 文件中定义的；
 + React的组件，并没有把一个组件 拆分为 三部分（结构、样式、业务逻辑），而是全部使用JS来实现一个组件的；（也就是说：结构、样式、业务逻辑是混合在JS里面一起编写出来的）

### 开发团队方面
+ React是由FaceBook前端官方团队进行维护和更新的；因此，React的维护开发团队，技术实力比较雄厚；
+ Vue：第一版，主要是有作者 尤雨溪 专门进行维护的，当 Vue更新到 2.x 版本后，也有了一个小团队进行相关的维护和开发；

### 社区方面
+ 在社区方面，React由于诞生的较早，所以社区比较强大，一些常见的问题、坑、最优解决方案，文档、博客在社区中都是可以很方便就能找到的；
+ Vue是近两年才诞生开源出来的，所以，它的社区相对于React来说，要小巧一些，所以，可能有的一些坑，没人踩过；

### 移动APP开发体验方面
+ Vue，结合 Weex 这门技术，提供了 迁移到 移动端App开发的体验（Weex，目前只是一个 小的玩具， 并没有很成功的 大案例；）
+ React，结合 ReactNative，也提供了无缝迁移到 移动App的开发体验（RN用的最多，也是最火最流行的）；



## 为什么要学习React
1. 设计很优秀，是基于组件化的，方便我们UI代码的重用；
2. 开发团队实力强悍，不必担心短更的情况；
3. 社区强大，很多问题都能找到对应的解决方案；
4. 提供了无缝转到 ReactNative 上的开发体验，让我们技术能力得到了拓展；增强了我们的核心竞争力



## React中几个核心的概念
### 虚拟DOM（Virtual Document Object Model）
 + DOM的本质是什么：就是用JS表示的UI元素
 + DOM和虚拟DOM的区别：
   - DOM是由浏览器中的JS提供功能，所以我们只能人为的使用 浏览器提供的固定的API来操作DOM对象；
   - 虚拟DOM：并不是由浏览器提供的，而是我们程序员手动模拟实现的，类似于浏览器中的DOM，但是有着本质的区别；
 - 为什么要实现虚拟DOM：
 - 什么是React中的虚拟DOM：
 - 虚拟DOM的目的：
![虚拟DOM - 表格排序案例](images/虚拟DOM引入图片.png)
 - 表格排序案例解析：
![虚拟DOM - 表格排序案例解析](images/React中虚拟DOM的概念.png)

### Diff算法
 - tree diff:新旧DOM树，逐层对比的方式，就叫做 tree diff,每当我们从前到后，把所有层的节点对比完后，必然能够找到那些 需要被更新的元素；
 - component diff：在对比每一层的时候，组件之间的对比，叫做 component diff;当对比组件的时候，如果两个组件的类型相同，则暂时认为这个组件不需要被更新，如果组件的类型不同，则立即将旧组件移除，新建一个组件，替换到被移除的位置；
 - element diff:在组件中，每个元素之间也要进行对比，那么，元素级别的对比，叫做 element diff；
 - key：key这个属性，可以把 页面上的 DOM节点 和 虚拟DOM中的对象，做一层关联关系；
![Diff算法图](images/Diff.png)

## React项目的创建
1. 运行 `cnpm i react react-dom -S` 安装包
2. 在项目中导入两个相关的包：
```js
// 1. 在 React 学习中，需要安装 两个包 react  react-dom
// 1.1 react 这个包，是专门用来创建React组件、组件生命周期等这些东西的；
// 1.2 react-dom 里面主要封装了和 DOM 操作相关的包，比如，要把 组件渲染到页面上
import React from 'react'
import ReactDOM from 'react-dom'
```
3. 使用JS的创建虚拟DOM节点：
```js
    // 2. 在 react 中，如要要创建 DOM 元素了，只能使用 React 提供的 JS API 来创建，不能【直接】像 Vue 中那样，手写 HTML 元素
    // React.createElement() 方法，用于创建 虚拟DOM 对象，它接收 3个及以上的参数
    // 参数1： 是个字符串类型的参数，表示要创建的元素类型
    // 参数2： 是一个属性对象，表示 创建的这个元素上，有哪些属性
    // 参数3： 从第三个参数的位置开始，后面可以放好多的虚拟DOM对象，这写参数，表示当前元素的子节点
    // <div title="this is a div" id="mydiv">这是一个div</div>

    var myH1 = React.createElement('h1', null, '这是一个大大的H1')

    var myDiv = React.createElement('div', { title: 'this is a div', id: 'mydiv' }, '这是一个div', myH1)
```
4. 使用 ReactDOM 把元素渲染到页面指定的容器中：
```js
    // ReactDOM.render('要渲染的虚拟DOM元素', '要渲染到页面上的哪个位置中')
    // 注意： ReactDOM.render() 方法的第二个参数，和vue不一样，不接受 "#app" 这样的字符串，而是需要传递一个 原生的 DOM 对象
    ReactDOM.render(myDiv, document.getElementById('app'))
```
5. JSX（符合 XML 规范的 JS 语法）的原理是什么？
```js
// 注意： 千万要记住，哪怕你在 JS 中可以写 JSX 语法了，但是，JSX内部在运行的时候，也是先把 类似于HTML 这样的标签代码，转换为了 React.createElement 的形式；
// 也就是说：哪怕我们写了 JSX 这样的标签，也并不是直接把 我们的 HTML 标签渲染到页面上，而是先转换成 React.createElement 这样的JS代码，再渲染到页面中；（JSX是一个对程序员友好的语法糖）
```


## JSX语法
1. 如要要使用 JSX 语法，必须先运行 `cnpm i babel-preset-react -D`，然后再 `.babelrc` 中添加 语法配置；
2. JSX语法的本质：还是以 React.createElement 的形式来实现的，并没有直接把 用户写的 HTML代码，渲染到页面上；
3. 如果要在 JSX 语法内部，书写 JS 代码了，那么，所有的JS代码，必须写到 {} 内部；
4. 当 编译引擎，在编译JSX代码的时候，如果遇到了`<`那么就把它当作 HTML代码去编译，如果遇到了 `{}` 就把 花括号内部的代码当作 普通JS代码去编译；
5. 在{}内部，可以写任何符合JS规范的代码；
6. 在JSX中，如果要为元素添加`class`属性了，那么，必须写成`className`，因为 `class`在ES6中是一个关键字；和`class`类似，label标签的 `for` 属性需要替换为 `htmlFor`.
7. 在JSX创建DOM的时候，所有的节点，必须有唯一的根元素进行包裹；
8. 如果要写注释了，注释必须放到 {} 内部;
9. 注意：babel-core 和 babel-loader 必须是相邻的版本，否则编译报错；
```js
Cannot find module '@babel/core'
babel-loader@8 requires Babel 7.x (the package '@babel/core'). If you'd like to use Babel 6.x ('babel-core'), you should install 'babel-loader@7'.ou should install 'babel-loader@7'.
// 原因是：
// babel-loader和babel-core版本不对应所产生的，
// babel-loader 8.x对应babel-core 7.x
// babel-loader 7.x对应babel-core 6.x
// 解决方法：
npm i --save-dev babel-loader@7.1.5
```



## React中组件的创建
> 在React中，"构造函数" 就是一个最基本的组件;

> 如果想要把组件放到页面中，可以把 构造函数的名称，当作 组件的名称，以 HTML标签形式引入页面中即可；

>  注意：React在解析所有的标签的时候，是以标签的首字母来区分的，如果标签的首字母是小写，那么就按照 普通的 HTML 标签来解析，如果 首字母是大写，则按照 组件的形式去解析渲染；

> 结论：组件的首字母必须是大写；
```js
function Hello(props) {
	// 在组件中，如果想要使用外部传递过来的数据，必须，显示的在 构造函数参数列表中，定义 props 属性来接收；
	// 通过 props 得到的任何数据都是只读的，不能从新赋值
	// props.name = '000'
	return <div>
		<h1>这是在Hello组件中定义的元素 --- {props.name}</h1>
	</div>
}
```
题外话：
```js
function Person (name, age) {
	this.name = name
	this.age = age
}
Person.prototype.say = function () {
	console.info('这是 say 方法')
}
let p1 = new Person('zs', 16)
console.info(p1.say())
```

## 第一种基本组件的创建方式
- ### 父组件向子组件传递数据
- ### 属性扩散（ES6 中 ...）
```js
import Hello from './components/Hello.jsx'
let person = {
	name: 'ls',
	age: 22,
	gender: '男',
	address: '北京'
}
ReactDOM.render(<div>
	<Hello {...person}></Hello>
</div>, document.getElementById('app'))
```

- ### 将组件封装到单独的文件中
```js
import React from 'react'

// 在构造函数中定义的组件，若要使用 props ，必须先定义，然后再使用；而使用 class 创建的组件，可直接使用 this.props 来访问，不需要预先接收 props;
export default function Hello (props) {
	return (
		<div>
			<h1>
				这是用 JSX 文件创建的组件
			</h1>
			<p>
				{
					console.log(props)
				}
			</p>
		</div>
	)
}
```

## 第二种创建组件的方式
> 面向对象的三大特点：继承 / 封装 / 多态（多态 和 接口、虚拟方法有关）；

- ### 了解ES6中class关键字的使用
> 关键字： class / constructor / extends / super / static
	
	每个 class 类里面都会有一个 constructor 构造器，若没有显示的写入，则也会隐式的存在与类中；
	当 new 一个实例时，constructor 构造器会优先调用；
```js
class ClassHello {
	constructor (name, age) {
		this.name = name
		this.age = age
	}
	// 实例方法 say ，必须通过 new 出来的实例调用
	say () {
		console.info('This is say Fn')
	}
	// 静态方法/属性 在原型对象上
	// 静态属性
	static info = 999
	// 静态方法
	static sayStatic () {
		console.info('This is Static Fn')
	}
}
let cl = new ClassHello('cl', 27)
console.info(cl)
console.info(cl.say())
console.info(ClassHello.info)
console.info(ClassHello.sayStatic())
```

继承：
```js
class Person {
	constructor(name, age) {
		console.log(3)
		this.name = name
		this.age = age
	}

	say() {
		console.log('这是 Person中的 say 方法')
	}
	static info = 123
}
// 使用 extends 实现继承，extends 前面的是子类，后面的是父类
class Chinese extends Person {
	constructor(name, age, color, language) {
		console.log(1)
		// 注意： 当使用 extends 关键字实现了继承， 子类的 constructor 构造函数中，必须显示调用 super() 方法，这个 super 表示父类中 constructor 的引用
		super(name, age)
		this.color = color
		this.language = language
		console.log(2)
	}
}
```
继承-父类只搭架子，在子类中实现具体操作
```js
class Animal {
	// 父类只定义了方法的名称，和作用，但是并没有具体的实现逻辑
	say() {
		// console.log('喵喵')
	}
}
class Cat extends Animal {
	// 当子类继承了父类之后，必然要继承父类中的方法，但是，发现say方法空有其壳，如果子类想要调用 say， 必须自己先实现这个方法，才能调用；
	say() {
		console.log('miaomiao')
	}
}
class Dog extends Animal {
	say() {
		console.log('wangwang')
	}
}
```

- ### 基于class关键字创建组件
```js
import React, { Component } from 'react'
export default class ClassHello extends Component {
	// 通过报错提示得知：在class创建的组件中，必须定义一个render函数
	render () {
		// 在render函数中，必须返回一个null或者符合规范的虚拟DOM元素
		return (
			<div>
				<h1>
					这是用 class 创建的组件
				</h1>
			</div>
		)
	}
}
```

## 两种创建组件方式的对比
1. 用构造函数创建出来的组件：专业的名字叫做“无状态组件”
2. 用class关键字创建出来的组件：专业的名字叫做“有状态组件”

> 用构造函数创建出来的组件，和用class创建出来的组件，这两种不同的组件之间的**本质区别就是**：有无state属性！！！

> 有状态组件和无状态组件之间的本质区别就是：有无state属性！

## 详解两种创建方式（构造函数 / class ）区别和应用场景：
- 使用 function 构造函数创建的组件，内部没有 state 私有数据，只有 一个 props 来接收外界传递过来的数据；
- 使用 class 关键字 创建的组件，内部，除了有 this.props 这个只读属性之外，还有一个 专门用于 存放自己私有数据的 this.state 属性，这个 state 是可读可写的！
- 有状态组件和无状态组件，最本质的区别，就是有无 state 属性；同时， class 创建的组件，有自己的生命周期函数，但是，function 创建的 组件，没有自己的生命周期函数；
- 有状态组件 和 无状态组件的应用场景各自是什么？
	1. 如果一个组件需要存放自己的私有数据，或者需要在组件的不同阶段执行不同的业务逻辑，此时，非常适合用 class 创建出来的有状态组件；
	2. 如果一个组件，只需要根据外界传递过来的 props，渲染固定的 页面结构就完事儿了，此时，非常适合使用 function 创建出来的 无状态组件；（使用无状态组件的小小好处： 由于剔除了组件的生命周期，所以，运行速度会相对快一丢丢）;

使用 class 创建组件基础详解：
```jsx
import React, { Component } from 'react'

/**
 * 使用 class 创建的类，通过 extends 关键字，继承了 React.Component 之后，这个类，就是一个组件的模板了;
 */
export default class ClassHello extends Component {
	constructor (props) {
		// 必须在 constructor 第一行显示调用 super()
		// super() 表示父类的构造函数
		super(props)

		// 本组件中的私有数据，就如 Vue 中 data() { return {} } 函数；
		this.state = {
			msg: 'This is ClassHello Component',
			info: 'This is ClassHello INFO'
		}
	}

	// render() 函数必须要有，并且还要返回一个标签 或者 null；
	// 虽然在 React dev tools 中，并没有显示说 class 组件中的 props 是只读的，但是，经过测试得知，其实 只要是 组件的 props，都是只读的；
	render () {
		return (<div>
			<h1>这是 ClassHello 组件</h1>
			<h3>
				外界传值：
				{ this.props.address } --- { this.props.info }
			</h3>
			<h5>
				{ this.state.msg }
			</h5>
			<br></br>

			{/* 1.1 在React中，如果想要为元素绑定事件，不能使用 网页中 传统的 onclick 事件，而是需要 使用 React 提供的  onClick */}
			{/* 1.2 也就是说：React中，提供的事件绑定机制，使用的 都是驼峰命名，同时，基本上，传统的 JS 事件，都被 React 重新定义了一下，改成了 驼峰命名 onMouseMove  */}
			{/* 2.1 在 React 提供的事件绑定机制中，事件的处理函数，必须直接给定一个 function，而不是给定一个 function 的名称 */}
			{/* 2.2 在为 React 事件绑定 处理函数的时候，需要通过 this.函数名， 来把 函数的引用交给 事件 */}

			<input type="button" value="修改 msg" id="btnChangeMsg" onClick={this.changeMsg} />
		</div>)
	}

	changeMsg = () => {
		// 注意：this 指向 “本组件”
		console.log('This is ClassHello Component changeMsgFn', this)

		// 直接使用 this.state.msg 可以重新赋值给此变量，但是页面不会更新最新的数据，不推荐使用；
		// this.state.msg = '修改的 msg'

		// 推荐使用 this.setState({ 配置对象 }) , 来重新为 state 赋值；
		// 注意： this.setState 方法，只会重新覆盖那些 显示定义的属性值，如果没有提供最全的属性，则没有提供的属性值，不会被覆盖；
		this.setState({
			msg: 124
		})

		// this.setState 方法，也支持传递一个 function，如果传递的是 function，则在 function 内部，必须return 一个 对象；
		// 在 function 的参数中，支持传递两个参数，其中，第一个参数是 prevState，表示为修改之前的 老的 state 数据；第二个参数，是 外界传递给当前组件的 props 数据；
		this.setState((prevState, props) => {
			console.info('顺序二', 'prevState: ', prevState, 'props: ', props)
			return {
				msg: 'This is Fn in msg'
			}
		}, () => {
			// 由于 this.setState 是异步执行的，所以，如果想要立即拿到最新的修改结果，最保险的方式， 在回调函数中去操作最新的数据；
			console.info('顺序三；回调函数中 this ：', this)
		})

		// 经过测试发现， this.setState 在调用的时候，内部是异步执行的，所以，当立即调用完 this.setState 后，输出 state 值可能是旧的；
		console.info('顺序一；', this.state.msg)
	}
}
```

## 样式 style 和 样式模块化
```jsx
/**
 * 注意：在使用 import 的时候，import 只能放到模块的开头位置
 */
import React from 'react'
import 模块样式名称 from '样式路径'

// JS 生成的样式对象，个人建议不要使用；
// 默认情况下，没有启用 css 模块化，则 “模块样式” 输出为一个空对象（因为 .css 样式表中，不能直接通过 JS 的 export default 导出对象）；
// 启用 css 模块化之后，导入样式表得到的 “模块样式” 就变成了一个样式对象，其中，属性名是在样式表中定义的类名，属性值，是自动生成的一个复杂的类名（防止类名冲突）；

// 怎么启用 css 模块化：（webpack.config.js -> module -> rules）
{
	test: /\.css$/,
	use: [
		'style-loader',
		{
			options: {
				modules: {
					localIdentName: '[path][name]_[local]-[hash:base64:5]'
				}
			}
		}
	]
}

// JSX 语法中 style 内联样式表示：style={{ 样式属性：样式属性值。。。 }}；外层 {}：表示要写 JS 代码；内层 {}:表示用一个 JS 对象表示样式；
// 注意：在 style 的样式规则中，如果属性值的单位是 px ，则 px 可以省略，直接写数值就可以；


// 样式表示方法：
// 	方法一：
// 		const 样式1-1名称: {}
// 		const 样式1-2名称: {}
// 	方法二：把样式对象封装到唯一的一个对象中
// 		const 样式2 = {
// 			样式2-1: {}
// 			样式2-2: {}
// 		}
// 注意：react 中没有指令的概念；没有 vue 中 scoped 这样的指令；
:global()
:local()
```


## 总结
- 理解React中虚拟DOM的概念
- 理解React中三种Diff算法的概念
- 使用JS中createElement的方式创建虚拟DOM
- 使用ReactDOM.render方法
- 使用JSX语法并理解其本质
- 掌握创建组件的两种方式
- 理解有状态组件和无状态组件的本质区别
- 理解props和state的区别

## 相关文章
+ [React数据流和组件间的沟通总结](http://www.cnblogs.com/tim100/p/6050514.html)
+ [单向数据流和双向绑定各有什么优缺点？](https://segmentfault.com/q/1010000005876655/a-1020000005876751)
+ [怎么更好的理解虚拟DOM?](https://www.zhihu.com/question/29504639?sort=created)
+ [React中文文档 - 版本较低](http://www.css88.com/react/index.html)
+ [React 源码剖析系列 － 不可思议的 react diff](http://blog.csdn.net/yczz/article/details/49886061)
+ [深入浅出React（四）：虚拟DOM Diff算法解析](http://www.infoq.com/cn/articles/react-dom-diff?from=timeline&isappinstalled=0)
+ [一看就懂的ReactJs入门教程（精华版）](http://www.cocoachina.com/webapp/20150721/12692.html)
+ [CSS Modules 用法教程](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)
+ [将MarkDown转换为HTML页面](http://blog.csdn.net/itzhongzi/article/details/66045880)
+ [win7命令行 端口占用 查询进程号 杀进程](https://jingyan.baidu.com/article/0320e2c1c9cf0e1b87507b26.html)