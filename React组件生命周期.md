## 组件的生命周期
 + 概念：在组件创建、到加载到页面上运行、以及组件被销毁的过程中，总是伴随着各种各样的事件，这些在组件特定时期，触发的事件，统称为 组件的生命周期；
 + 组件生命周期分为三部分：
   - **组件创建阶段**：组件创建阶段的生命周期函数，有一个显著的特点：创建阶段的生命周期函数，在组件的一辈子中，只执行一次；
	> componentWillMount: 组件将要被挂载，此时还没有开始渲染虚拟DOM;

	> render：第一次开始渲染真正的虚拟DOM，当render执行完，内存中就有了完整的虚拟DOM了

	> componentDidMount: 组件完成了挂载，此时，组件已经显示到了页面上，当这个方法执行完，组件就进入都了 运行中 的状态


   - **组件运行阶段**：也有一个显著的特点，根据组件的state和props的改变，有选择性的触发0次或多次；
   > componentWillReceiveProps: 组件将要接收新属性，此时，只要这个方法被触发，就证明父组件为当前子组件传递了新的属性值;

   > shouldComponentUpdate: 组件是否需要被更新，此时，组件尚未被更新，但是，state 和 props 肯定是最新的;

   > componentWillUpdate: 组件将要被更新，此时，尚未开始更新，内存中的虚拟DOM树还是旧的;

   > render: 此时，又要重新根据最新的 state 和 props 重新渲染一棵内存中的 虚拟DOM树，当 render 调用完毕，内存中的旧DOM树，已经被新DOM树替换了！此时页面还是旧的;

   > componentDidUpdate: 此时，页面又被重新渲染了，state 和 虚拟DOM 和 页面已经完全保持同步;


   - **组件销毁阶段**：也有一个显著的特点，一辈子只执行一次；
   > componentWillUnmount: 组件将要被卸载，此时组件还可以正常使用；

[vue中的生命周期图](https://cn.vuejs.org/v2/guide/instance.html#生命周期图示)
[React Native 中组件的生命周期](http://www.race604.com/react-native-component-lifecycle/)


![React中组件的生命周期](./images/React中组件的生命周期.png)

React生命周期详解：
![React中组件的生命周期详解](./images/React中组件的生命周期详解.png)

### defaultProps
> 在组件创建之前，会先初始化默认的props属性，这是全局调用一次，严格地来说，这不是组件的生命周期的一部分。在组件被创建并加载候，首先调用 constructor 构造器中的 this.state = {}，来初始化组件的状态。

React生命周期的回调函数总结成表格如下：
![React生命周期表格](./images/React生命周期表格.png)

组件生命周期的执行顺序：
+ Mounting：
	- constructor()
	- componentWillMount()
	- render()
	- componentDidMount()
+ Updating：
	- componentWillReceiveProps(nextProps)
	- shouldComponentUpdate(nextProps, nextState)
	- componentWillUpdate(nextProps, nextState)
	- render()
	- componentDidUpdate(prevProps, prevState)
+ Unmounting：
	- componentWillUnmount()

## 通过Counter计数器的小案例 - 了解生命周期函数
1. 给组件设置默认属性：`static defaultProps = {}`
2. 给属性进行类型校验，需要先运行`cnpm i prop-types --save`，然后导入类型校验，最后 `static propType = {}`
3. 通过改变 state 状态，来重新运行；
```jsx
import React from 'react'
import ReactTypes from 'prop-types'

// console.log('类型校验包', ReactTypes)

/**
 * 组件的封装/参数校验
 */
export default class Counter extends React.Component {
	constructor(props) {
		super(props)

		// 初始化组件的私有状态，保存的是组件私有数据
		this.state = {
			msg: 'ok',
			// 基数, 把 外界传递过来的 initcount 赋值给 state 中的 count值，这样，就把 count 值改成了可读可写的 state 属性，今后，就能实现 点击 按钮 ，count 值 + 1 的需求了
			count: props.initcount
		}
	}

	// 静态属性；defaultProps 静态属性，为组件提供默认值；
	static defaultProps = {
		initcount: 0
	}

	// 静态属性；静态的 propTypes 对象，此对象会把外界传递过来的属性，做类型校验；
	// 注意： 如果要为 传递过来的属性做类型校验，必须安装 React 提供的 第三方包，叫做 prop-types （安装：npm install -S prop-types）;
	// prop-types 大概在 v.15.* 之前，并没有单独抽离出来，那时候，还和 react 包 在一起；后来， 从 v.15.* 之后，官方把类型校验的 模块，单独抽离为 一个包，就叫做 prop-types
	static propTypes = {
		initcount: ReactTypes.number // 使用 prop-types 包，来定义 initcount 为 number 类型
	}

	// 在组件即将挂载到页面上的时候执行，此时，组件尚未挂载到页面中；虚拟DOM 也未在内存中开始创建；
	// componentWillMount 函数，等同于 Vue 中的 created 生命周期函数；
	componentWillMount() {
		// 此时，无法获取到 页面上的 任何元素，因为 虚拟DOM 和 页面 都还没有开始渲染呢！【在这个阶段中，不能去操作页面上的DOM元素】
		// console.log(document.getElementById('myh3'));
		// console.log(this.props.initcount);
		// console.log(this.state.msg);
		// this.myselfFunc()
	}

	// 此生命周期函数，表示即将开始渲染内存中的 虚拟DOM ，当此函数执行完，内存中就有了一个渲染好的 虚拟DOM，但是此时页面上还未显示正真的DOM元素；
	render() {
		// 在 return 之前，虚拟DOM还没有开始创建，页面上也是空的，根本拿不到任何的 元素;
		// console.log(document.getElementById('myh3'));

		// 在 组件运行阶段中，每当调用 render 函数的时候，页面上的 DOM元素，还是之前旧的;
		// console.log(this.refs.h3 && this.refs.h3.innerHTML);

		// 不要在 render 中使用 this.setState,因为 会陷入死循环;
		/*  this.setState({
		   count: this.state.count + 1
		 }) */

		return <div>
			<h1>这是 Counter 计数器组件</h1>
			<input type="button" value="+1" id="btn" onClick={this.increment} />
			<hr />
			<h3 id="myh3" ref="h3">当前的数量是：{this.state.count}</h3>
		</div>

		// 当 return 执行完毕后， 虚拟DOM创建好了，但是，还没有挂载到真正的页面中;
	}

	increment = () => {
		this.setState({
			count: this.state.count + 1
		})
	}

	// 当组件挂载到页面上之后，会进入这个生命周期函数，只要进入这个生命周期函数了，必然说明，页面上，已经有可见的DOM元素了;
	// 当组件执行完 componentDidMount 函数后，就进入到了 运行中的状态，所以，componentDidMount 是创建阶段的最后一个函数;
	// componentDidMount 相当于 Vue 中的 mounted 函数;
	componentDidMount() {
		// 在这个函数中，我们可以放心的去 操作 页面上你需要使用的 DOM 元素了；
		// console.log(document.getElementById('myh3'));

		/* document.getElementById('btn').onclick = () => {
		  // console.log('ok');
		  // console.log(this);
		  // this.props.initcount++
		  this.setState({
			count: this.state.count + 1
		  })
		} */
	}

	// 组件的运行中状态;
	// 判断组件是否需要更新;
	shouldComponentUpdate(nextProps, nextState) {
		// 1. 在 shouldComponentUpdate 中要求必须返回一个布尔值
		// 2. 在 shouldComponentUpdate 中，如果返回的值是 false，则 不会继续执行后续的生命周期函数，而是直接退回到了 运行中 的状态，此时有序 后续的 render 函数并没有被调用，因此，页面不会被更新，但是， 组件的 state 状态，却被修改了；
		// return false

		// 需求： 如果 state 中的 count 值是偶数，则 更新页面，如果 count 值 是奇数，则不更新页面，我们想要的页面效果：4，6，8，10，12....
		// 经过打印测试发现，在 shouldComponentUpdate 中，通过 this.state.count 拿到的值，是上一次的旧数据，并不是当前最新的；
		// console.log(this.state.count + ' ---- ' + nextState.count);
		// return this.state.count % 2 === 0 ? true : false
		// return nextState.count % 2 === 0 ? true : false
		return true
	}

	// 组件将要更新，此时尚未更新，在进入这个 生命周期函数的时候，内存中的虚拟DOM是旧的，页面上的 DOM 元素 也是旧的;
	componentWillUpdate() {
		// 经过打印分析，得到，此时页面上的 DOM 节点，都是旧的，应该慎重操作，因为你可能操作的是旧DOM;
		// console.log(document.getElementById('myh3').innerHTML)
		// console.log(this.refs.h3.innerHTML);
	}

	// 组件完成了更新，此时，state 中的数据、虚拟DOM、页面上的DOM，都是最新的，此时，你可以放心大胆的去操作页面了;
	componentDidUpdate() {
		// console.log(this.refs.h3.innerHTML);
	}



	myselfFunc() {
		console.log('这是我自己定义的函数，和生命周期函数无关');
	}
}
```
4. 通过更新 props 属性来重新运行组件；
```jsx
import React from 'react'

// 父组件
export default class Parent extends React.Component {
	constructor(props) {
		super(props)

		this.state = {
			msg: '这是父组件中的 msg 消息'
		}
	}
	render() {
		return <div>
			<h1>这是父组件</h1>
			<input type="button" value="点击修改父组件的 MSG" onClick={this.changeMsg} />
			<hr />
			<Son pmsg={this.state.msg}></Son>
		</div>
	}
	changeMsg = () => {
		this.setState({
			msg: '娃哈哈'
		})
	}
}

// 子组件
class Son extends React.Component {
	constructor(props) {
		super(props)

		this.state = {}
	}

	render() {
		return <div>
			<h3>这是子组件 --- {this.props.pmsg}</h3>
		</div>
	}

	// 组件将要接收外界传递过来的新的 props 属性值
	// 当子组件第一次被渲染到页面上的时候，不会触发这个 函数；
	// 只有当 父组件中，通过 某些 事件，重新修改了 传递给 子组件的 props 数据之后，才会触发 componentWillReceiveProps
	componentWillReceiveProps(nextProps) {
		// console.log('被触发了！');
		// 注意： 在 componentWillReceiveProps 被触发的时候，如果我们使用 this.props 来获取属性值，这个属性值，不是最新的，是上一次的旧属性值
		// 如果想要获取最新的属性值，需要通过 componentWillReceiveProps 的参数列表来获取
		console.log(this.props.pmsg + ' ---- ' + nextProps.pmsg);
	}
}
```

## 组件初始化时生命周期事件总结
1. componentWillMount：
2. render：
3. componentDidMount：
4. 注意：在render函数中，不能调用`setState()`方法

## 通过原生的方式获取元素并绑定事件


## React中使用ref属性获取DOM元素引用


## 使用React中的事件，绑定count自增


## 组件运行中事件的对比
1. shouldComponentUpdate：
2. componentWillUpdate：
3. render：
4. componentDidUpdate：


## 绑定this并传参的三种方式
1. 在事件中绑定this并传参：
```
    <input type="button" value="在事件中绑定this并传参" onClick={this.handleMsg1.bind(this, '🍕', '🍟')} />

    // 在事件中绑定this并传参
    handleMsg1(arg1, arg2) {
        console.log(this);
        // 此时this是个null
        this.setState({
            msg: '在事件中绑定this并传参：' + arg1 + arg2
        });
    }
```
2. 在构造函数中绑定this并传参:
```
    // 修改构造函数中的代码：
    this.handleMsg2 = this.handleMsg2.bind(this, '🚗', '🚚');

    <input type="button" value="在构造函数中绑定this并传参" onClick={this.handleMsg2} />

    // 在构造函数中绑定this并传参
    handleMsg2(arg1, arg2) {
        this.setState({
            msg: '在构造函数中绑定this并传参：' + arg1 + arg2
        });
    }
```
3. 用箭头函数绑定this并传参：
```
    <input type="button" value="用箭头函数绑定this并传参" onClick={() => { this.handleMsg3('👩', '👰') }} />

    // 用箭头函数绑定this并传参
        handleMsg3(arg1, arg2) {
            this.setState({
                msg: '用箭头函数绑定this并传参：' + arg1 + arg2
            });
        }
```

## 绑定文本框与state中的值
1. 在Vue.js中，默认可以通过`v-model`指令，将表单控件和我们的`data`上面的属性进行双向数据绑定，数据变化和页面之间的变化是同步的！
2. 在React.js中，默认没有提供双向数据绑定这一功能，默认的，只能把`state`之上的数据同步到界面的控件上，但是不能默认实现把界面上数据的改变，同步到`state`之上，需要程序员手动调用相关的事件，来进行逆向的数据传输！
3. 绑定文本框和state的值：
```
    {/*只要将value属性，和state上的状态进行绑定，那么，这个表单元素就变成了受控表单元素，这时候，如果没有调用相关的事件，是无法手动修改表单元素中的值的*/}
    <input style={{ width: '100%' }} ref="txt" type="text" value={this.state.msg} onChange={this.handleTextChange} />

    // 这是文本框内容改变时候的处理函数
    handleTextChange = () => {
        this.setState({
            msg: this.refs.txt.value
        });
    }
```
4. 注意`setState的一个问题`：
```
// 保存最新的state状态值，在保存的时候，是异步地进行保存的，所以，如果想要获取最新的，刚刚保存的那个状态，需要通过回掉函数的形式去获取最新state
this.setState({
    msg: this.refs.txt.value
    // msg: e.target.value
}, function () {
    // 获取最新的state状态值
    console.log(this.state.msg);
});
```
5. this 绑定和文本框双向数据绑定；
```jsx
import React from 'react'

export default class BindThis extends React.Component {
	constructor(props) {
		super(props)

		this.state = {
			msg: '这是默认的msg'
		}

		// 可以在构造函数中，通过 bind 改变方法的 this 指向，并传参；
		// 注意，当为一个函数，调用 bind 改变了this指向后，bind 函数调用的结果，有一个返回值，这个值，就是被改变this指向后的函数的引用；
		// 注意： bind 不会修改 原函数的 this 指向
		this.changeMsg1 = this.changeMsg1.bind(this, '🚗', '👫')
	}

	render() {
		return <div>
			<h1>绑定This并传参的几种方式</h1>
			<h3>{this.state.msg}</h3>
			
			{/* bind 的作用： 为前面的函数，修改函数内部的 this 指向，让 函数内部的this，指向 bind 参数列表中的 第一个参数；
			bind 和 call/apply 之间的区别：
			call/apply 修改完this指向后，会立即调用前面的函数，但是 bind 只是修改this指向，并不会调用;
			注意： bind 中的第一个参数，是用来修改 this 指向的，第一个参数后面的所有参数，都会当作将来调用 前面函数 时候的入参; */}

			<input type="button" value="绑定this并传参的方式1" style={{margin: 10}} onClick={this.changeMsg1} />
			<input type="button" value="绑定this并传参的方式2" style={{margin: 10}} onClick={this.changeMsg2.bind(this, 'params-2', 'params2-1')} />
			<input type="button" value="绑定this并传参的方式3" style={{margin: 10}} onClick={() => { this.changeMsg3('😊', '😘') }} />

			<hr />

			{/* + 在 Vue 中，有 v-model 指令来实现双向数据绑定，但是，在 React 中， 根本没有指令的概念，因此React 默认也不支持 双向数据绑定;
			+ React 只支持，把数据从 state 上传输到 页面，但是，无法自动实现数据从 页面 传输到 state 中 进行保存，也就是，React 不支持数据的自动逆向传输， 只是实现了数据的单向绑定;
			+ 注意：如果为 表单元素，提供了 value 属性绑定，那么，必须同时为 表单元素 绑定 readOnly, 或者提供要给 onChange 事件;
			readOnly: 表示此元素只读；
			onChange：表示此元素可以修改，但是，需要自己定义修改的逻辑； */}

			<input type="text" style={{ width: '100%' }} value={this.state.msg} onChange={this.txtChanged} ref="txt" />
		</div>
	}

	// 方式1：在构造函数中改变 this 指向；
	changeMsg1(arg1, arg2) {
		this.setState({
			msg: '绑定this并传参的方式1' + arg1 + arg2
		})
	}

	// 方式2：在 事件处理函数中，直接使用 bind 绑定 this 传参；
	changeMsg2(arg1, arg2) {
		this.setState({
			msg: '绑定this并传参的方式2' + arg1 + arg2
		})
	}

	// 方式3：在 事件处理函数中，直接使用箭头函数绑定 this 并传参；
	changeMsg3 (arg1, arg2) {
		this.setState({
			msg: '绑定this并传参的方式3' + arg1 + arg2
		})
	}

	// 为 文本框 绑定 txtChanged 事件
	txtChanged = (e) => {
		// console.log('ok');
		// 如果想让 文本框在触发 onChange 的时候，同时把文本框最新的值，保存到 state 中，那么，我们需要手动调用 this.setState

		/**
		 * 获取文本框中 最新文本的3种方式：
		 1. 使用 document.xxx
		 2. this.refs.xxx.value
		 3. 使用 事件对象的 参数 e 来拿   e.target 就表示触发 这个事件的 事件源对象，得到的是一个原生的JS DOM 对象
		 */
		
		// console.log(e.target.value);
		this.setState({
			msg: e.target.value
		})
	}
}
```

## 发表评论案例

## context特性，上下文环境
简单记忆：`getChildContextTypes`
+ 前 3 个：getChildContext---(方法)；
+ 后 3 个：childContextTypes---(静态属性)；
+ 后 2 个：contextTypes---(静态属性)；
一个方法、两个静态属性

代码展示：
```jsx
import React from 'react'
import ReactTypes from 'prop-types'

/* // 最外层的父组件
export default class Com1 extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      color: 'red'
    }
  }

  render() {
    return <div>
      <h1>这是 父组件 </h1>
      <Com2 color={this.state.color}></Com2>
    </div>
  }
}



// 中间的子组件
class Com2 extends React.Component {
  render() {
    return <div>
      <h3>这是 子组件 </h3>
      <Com3 color={this.props.color}></Com3>
    </div>
  }
}


// 内部的孙子组件
class Com3 extends React.Component {
  render() {
    return <div>
      <h5 style={{ color: this.props.color }}>这是 孙子组件 </h5>
    </div>
  }
} */


/**
 * 穿透传值，上下文环境 context;
 * 简单记忆：getChildContextTypes
 */

// 最外层的父组件
export default class Com1 extends React.Component {
	constructor(props) {
		super(props)

		this.state = {
			color: 'red'
		}
	}

	//   getChildContextTypes
	// 1. 在 父组件中，定义一个 function，这个function 有个固定的名称，叫做 getChildContext ，内部，必须 返回一个 对象，这个对象，就是要共享给 所有子孙组件的  数据
	getChildContext() {
		return {
			color: this.state.color
		}
	}

	// 2. 使用 属性校验，规定一下传递给子组件的 数据类型， 需要定义 一个 静态的（static） childContextTypes（固定名称，不要改）
	static childContextTypes = {
		color: ReactTypes.string // 规定了 传递给子组件的 数据类型
	}

	render() {
		return <div>
			<h1>这是 父组件 </h1>
			<Com2></Com2>
		</div>
	}
}

// 中间的子组件
class Com2 extends React.Component {
	render() {
		return <div>
			<h3>这是 子组件 </h3>
			<Com3></Com3>
		</div>
	}
}

// 内部的孙子组件
class Com3 extends React.Component {

	// 3. 上来之后，先来个属性校验，去校验一下父组件传递过来的 参数类型
	static contextTypes = {
		color: ReactTypes.string // 这里，如果子组件，想要使用 父组件通过 context 共享的数据，那么在使用之前，一定要先 做一下数据类型校验
	}

	render() {
		return <div>
			<h5 style={{ color: this.context.color }}>这是 孙子组件  ---  {this.context.color} </h5>

		</div>
	}
}
```



## 相关文章
[类型校验](https://facebook.github.io/react/docs/typechecking-with-proptypes.html)
[Animation Add-Ons](https://reactjs.org/docs/animation.html#high-level-api-reactcsstransitiongroup)