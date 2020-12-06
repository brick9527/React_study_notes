# react组件

- 函数式组件
- 类组件
- 符合组件：组件中又有其他的组件，复合组件即可有类组件又可以有函数组件。

函数式组件与类组件的区别和使用，函数式比较简单，一般用于静态没有交互事件内容的组件页面。
类组件，一般又称为动态组件，那么一般会有交互或者数据修改的操作。


## 函数式组件

```js
function HelloComponent(props) {
  let isGo = props.weather === '下雨' ? '不出门' : '出门';
  // 直接返回JSX
  return (
    <div>
      <h1>今天是否出门？</h1>
      <span>{isGo}</span>
    </div>
  )
}

ReactDOM.render(
  <HelloComponent weather='下雨' />,
  document.getElementById('root')
)
```

## 类组件

```js
class HelloComponent extends React.Component{
  // 组件JSX写在render方法中
  render() {
    console.log(this);
    let isGo = this.props.weather === '下雨' ? '不出门' : '出门';
    return (
      <div>
        <h1>今天是否出门？</h1>
        <span>{isGo}</span>
      </div>
    )
  }
}

ReactDOM.render(
  <HelloComponent weather='下雨' />,
  document.getElementById('root')
)
```

## 复合组件

```js
function ChildComponent(props) {
  let isGo = props.weather === '下雨' ? '不出门' : '出门';
  return (
    <div>
      <h1>今天是否出门？</h1>
      <span>{isGo}</span>
    </div>
  )
}

class FatherComponent extends React.Component{
  render() {
    return (
      <div>
        <h1>你好：{this.props.name}</h1>
        <ChildComponent weather={this.props.weather} /> // 只需要在组件中使用组件即可，传入需要的参数
      </div>
    )
  }
}

ReactDOM.render(
  <FatherComponent weather='下雨' name='hello' />,
  document.getElementById('root')
)
```