# react路由

根据不同的路径，显示不同的组件(内容)。

react使用的库`react-router-dom`

安装

```js
cnpm install react-router-dom --save
```

ReactRouter三大组件：

- Router: 所有路由组件的根组件(底层组件)，包裹路由规则的最外层容器。
  - basename: 设置此路由根的路径，router可以在一个组件中写多个
- Route: 路由规则匹配组件，显示当前规则对应的组件
- Link: 路由跳转的组件
  - replace: 设置路由栈由堆叠改为替换。home->prod->me,点击返回，应该是回到home页。me替换了prod的栈的位置

注意:如果要精确匹配，那么可以在route.上设置exact属性。

## Router使用案例

```js
import {BrowserRouter as Router, Link, Route} from 'react-router-dom'

function page1(props) {
  return (
    <div>首页</div>
  )
}

function page2(props) {
  return (
    <div>介绍</div>
  )
}

function page3(props) {
  return (
    <div>产品</div>
  )
}

class Main extends React.Component {
  render() {
    return (
      <div>
        <Router>
          <div className="nav">
            <Link to="/">首页</Link>
            <Link to="/intro">介绍</Link>
            <Link to="/prod">产品</Link>
          </div>
          <Route path="/" exact component={page1}></Route>
          <Route path="/intro" exact component={page2}></Route>
          <Route path="/prod" exact component={page3}></Route>
        </Router>

        {/* 可以定义多个Router */}
        <Router basename="/admin">
          <Route path="/" exact component={() => (<div>admin-main</div>)}></Route>
          <Route path="/intro" exact component={() => (<div>admin-intro</div>)}></Route>
          <Route path="/prod" exact component={() => (<div>admin-prod</div>)}></Route>
        </Router>
      </div>
    )
  }
}

ReactDOM.render(
  <Main></Main>,
  document.getElementById('root')
);
```

## Link标签的to还可以这么写

```js
const obj = { 
  pathname: "/me", // 跳转的路径
  search: '?username=123', // get请求参数
  hash: '#hash911', // 锚值
  state: { msg: 'hello world' } // 数据
}
return (
  <Link to={obj}>产品</Link>
)
```

这个obj的数据在对应页面的`props`下的`location`属性获取

## Link的replace属性

点击链接后，将新地址替换成历史访问记录的原地址。

```js
return (
  <Link to={obj} replace>产品</Link>
)
```

## 动态路由

```js
function News(props) {
  console.log(props)
  return (
    <div>
      新闻{props.match.params.id}
    </div>
  )
}

class Main extends React.Component {
  render() {
    return (
      <Router>
        <Link to="/news/1">1111</Link>
        <Route path="/news/:id" component={News}></Route>
      </Router>
    )
  }
}
```