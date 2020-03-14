# React路由.antd引入


## React 路由：

若要使用路由模块，起手式需要两步走：

1. `yarn add react-router-dom`（安装包）；
2. 组件中导入路由模块: `import { HashRouter, Route, Link, ... } from 'react-router-dom'`

## 使用 react-router-dom 实现路由跳转

+ HashRouter：是一个路由的根容器，一个应用程序中，一般只需要唯一的一个HashRouter容器即可！将来，所有的Route和Link都要在HashRouter中进行使用;

+ 注意：HashRouter中，只能有唯一的一个子元素;
```jsx
render () {
	return (<HashRouter>
		<div>
			...
		</div>
	</HashRouter>)
}
```

+ Link：是相当于超链接一般的存在；点击Link，跳转到相应的路由页面！负责进行路由地址的切换！

+ Route：是路由匹配规则，当路由地址发生切换的时候，就会来匹配这些定义好的Route规则，如果有能匹配到的路由规则，那么，就会展示当前路由规则所对应的页面！Route 标签上有两个重要的属性：path / component;

+ Route：除了是一个匹配规则之外，还是一个占位符，将来，此Route所匹配到的组件页面，将会展示到Route所在的这个位置；也就是说：Route 有两种身份：
	1. 它是一个路由匹配规则；
	2. 它是一个占位符，表示将来匹配到的组件都放到这个位置，再者，react-router 中的路由匹配默认是进行模糊匹配的，可以通过`Route`身上的`exact`属性， 来表示当前的 `Route`是进行精准匹配；

```jsx
// 其中path指定了路由匹配规则，component指定了当前规则所对应的组件

<Route path="" component={}></Route>

```

+ 可以使用`Redirect`实现路由重定向;

```jsx
    // 导入路由组件

    import {Route, Link, Redirect} from 'react-router-dom'

    <Redirect to="/movie/in_theaters"></Redirect>
```

+ 若要匹配参数，可以在匹配规则中使用：修饰符，表示这个位置匹配到的是 参数；

```jsx
<Route path="/home/:id/:name" component={ Movie } exact></Route>
```

+ 若要从路由规则中获取匹配到的参数，进行使用，可以使用 `this.porps.match.params.XXX`来访问；或者可以写成这样：

```jsx
...
constructor (props) {
	super(props)
	this.state = {
		routeParams: props.match.params
	}
}
```

## antd 的全局引入 和 按需引入 ， 按照官方介绍即可：

> 全局引入时，需要在 `main.js` 中引入样式 `import 'antd/dist/antd.css'`;

> 一般第三方UI组件，他们的样式表都是以 `.css` 文件结尾，则我们在写代码时，最好不要写 `.css`文件，并且不要启用 `.css` 文件的模块化 （在 `webpack.config.js`中配置的）；否则将会导致样式问题；

> 一般推荐使用样式表的预编译 `.less`/ `.scss` ，并且启用样式模块化；