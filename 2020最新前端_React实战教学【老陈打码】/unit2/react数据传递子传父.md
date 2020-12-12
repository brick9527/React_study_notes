# react数据传递子传父

调用父元素的函数从而操作父元素的数据，从而实现数据从子元素传递至父元素

```js
class ParentComponent extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      childData: null
    }
  }

  render() {
    return (
      <div>
        <h1>子传父的数据：{this.state.childData}</h1>
        <ChildComponent setParentData={this.setParentData}/>
      </div>
    )
  }

  // 使用箭头函数省略绑定this那一步
  setParentData = (data) => {
    this.setState({
      childData: data
    })
  }
}

class ChildComponent extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      childData: 'hello world'
    }
  }

  render() {
    return (
      <div>
        <button onClick={this.setData}>传递数据</button>
        <button onClick={() => {this.props.setParentData(this.state.childData + '第二个')}}>传递数据</button> {/*也可以直接使用这样的形式调用方法*/}
      </div>
    )
  }

  // 使用箭头函数省略绑定this那一步
  setData = () => {
    this.props.setParentData(this.state.childData)
  }
}

ReactDOM.render(
  <ParentComponent />,
  document.getElementById('root')
);
```