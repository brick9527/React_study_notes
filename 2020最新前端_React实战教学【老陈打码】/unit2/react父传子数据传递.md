# react父传子数据传递

- props

父传递给子组件数据，单向流动，不能子传递给父。

props的传值，可以是任意的类型。

Props可以设置默认值

```js
HelloMessage.defaultProps = { name: '老陈', msg: 'hello world' }
```

**注意: props 可以传递函数，props 可以传递父元素的函数，就可以去修改父元素的state,从而达到传递数据给父元素。**

## 父元素控制子元素显示

```js
import './child.css';

// 在父元素中使用state去控制子元素props的从而达到父元素数据传递给子元素
class ParentComponent extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      isActive: true
    }
    this.changeShow = this.changeShow.bind(this)
  }

  render() {
    return (
      <div>
        <button onClick={this.changeShow}>显示/隐藏</button>
        <ChildComponent isActive={this.state.isActive} />
      </div>
    )
  }

  changeShow() {
    this.setState({
      isActive: !this.state.isActive
    })
  }
}

class ChildComponent extends React.Component {
  constructor(props) {
    super(props)
  }

  render() {
    let strClass = null
    if (this.props.isActive) {
      strClass = ' active'
    } else {
      strClass = ''
    }

    return (
      <div className={'content' + strClass}>
        这是子元素
      </div>
    )
  }
}

ReactDOM.render(
  <ParentComponent />,
  document.getElementById('root')
);
```

`child.css`文件内容

```css
.content {
  display: none;
  width: 400px;
  height: 400px;
  background-color: skyblue;
}

.content.active {
  display: block;
}
```