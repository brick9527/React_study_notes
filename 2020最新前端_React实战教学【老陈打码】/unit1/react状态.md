# react状态

## 做一个时钟

时间每秒进行自动更新

```js
class Clock extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      time: new Date().toLocaleTimeString()
    }
  }

  render() {
    return (
      <div>
        <h1>当前时间：{this.state.time}</h1>
      </div>
    )
  }

// 生命周期函数，组件渲染完成时函数
  componentDidMount() {
    // 在这里定时刷新组件state中的数据
    // 切勿直接修改state数据，直接修改state值不会重新渲染内容，需要使用setState方法
    // 通过this.setState修改完数据后，并不会立即修改DOM里面的内容, react会在
    // 这个函数内容所有设置状态改变后，统一对比虚拟DOM对象，然后在统一修改，提升性能
    setInterval(() => {
      this.setState({
        time: new Date().toLocaleTimeString(),
      })
    }, 1000)
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```

## 做一个切换的Tab

```js
import './tab.css';

class Tab extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      c1: 'content active',
      c2: 'content'
    }

    // 需要额外绑定this指针给自定义的方法。把当前的this对象绑定到对应的
    this.clickEvent = this.clickEvent.bind(this)
  }

  render() {
    return (
      <div>
        <button data-index="1" onClick={this.clickEvent}>面板一</button>
        <button data-index="2" onClick={this.clickEvent}>面板二</button>
        <div className={this.state.c1}>面板1</div>
        <div className={this.state.c2}>面板2</div>
      </div>
    )
  }

  // 注册click方法（随意命名）
  clickEvent(e) {
    console.log(e.target.dataset.index)
    let index = e.target.dataset.index
    if (index === '1') {
      this.setState({
        c1: 'content active',
        c2: 'content'
      })
    } else {
      this.setState({
        c1: 'content',
        c2: 'content active'
      })
    }
  }
}

ReactDOM.render(
  <Tab />,
  document.getElementById('root')
);
```

再把`tab.css`文件补上样式

```css
.content {
  display: none;
}

.content.active {
  display: block;
}
```