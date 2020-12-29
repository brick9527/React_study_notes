# react插槽

组件中写入内容，这些内容可以被识别和控制。React 需要自己开发支持插槽功能。

原理：

组件中写入的HTML，可以传入到props中。

## 简单的插槽

```js
class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
    console.log(props);
  }

  render() {
    return (
      <div>
        <h1>插槽</h1>
        {/* 插槽在props.children属性下 */}
        {this.props.children}
      </div>
    )
  }
}

ReactDom.render(
  <ParentComponent>
    <h2>插槽1</h2>
    <h2>插槽2</h2>
    <h2>插槽3</h2>
  </ParentComponent>,
  document.querySelector('#root')
)
```

## 分结构插槽

```js
class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
    console.log(props);
  }

  render() {
    let headCom, bodyCom, tailCom;
    this.props.children.forEach(item => {
      // 注意这里是item.props
      if (item.props['data-type'] === 'head') {
        headCom = item
      } else if (item.props['data-type'] === 'body') {
        bodyCom = item
      } else {
        tailCom = item
      }
    })
    return (
      <div>
        <h1>头插槽</h1>
        {headCom}
        <h1>body</h1>
        {bodyCom}
        <h1>tail</h1>
        {tailCom}
      </div>
    )
  }
}

class ChildComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      arr: [1,2,3]
    }
  }

  render() {
    return (
      <ParentComponent>
        <h2 data-index={this.state.arr[0]} data-type="head">头部插槽1</h2>
        <h2 data-index={this.state.arr[1]} data-type="body">中部插槽2</h2>
        <h2 data-index={this.state.arr[2]} data-type="tail">尾部插槽3</h2>
      </ParentComponent>
    )
  }
}



ReactDOM.render(
  <ChildComponent></ChildComponent>,
  document.getElementById('root')
);
```