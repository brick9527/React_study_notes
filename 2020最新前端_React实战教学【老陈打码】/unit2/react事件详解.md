# react事件详解

## 特点

- react事件，绑定事件的命名，驼峰命名法。
- 使用`{}`关键字传入1个函数，而不是字符串。

### 事件对象

事件对象: React 返回的事件对象是代理的原生的事件对象，如果想要查看事件对象的具体值，必须之间输出事件对象的属性。如：

```js
class Parent extends React.Component {
  constructor(props) {
    super(props)
  }

  render() {
    return (
      <div onClick={this.parentEvent}>
        <h1>点击</h1>
      </div>
    )
  }

  parentEvent = (e) => {
    console.log(e); // 这里输出的很多事件属性是null，因为使用了代理
    console.log(e.preventDefault); // 要想查看事件属性，直接输出对应属性的值即可查看
  }

}
```


### 阻止默认行为

原生JS阻止默认行为时，可以直接返回return false;

React中，阻止默认必须`e.preventDefault()`

```js
class Parent extends React.Component {
  constructor(props) {
    super(props)
  }

  render() {
    return (
      <div>
        <form action="https://www.baidu.com">
          <button onClick={this.parentEvent}>提交</button>
        </form>
      </div>
    )
  }

  parentEvent = (e) => {
    // return false; // 无效

    e.preventDefault(); // 阻止form跳转
  }
}
```

### 事件传参

```js
class Parent extends React.Component {
  constructor(props) {
    super(props)
  }

  render() {
    return (
      <div>
        <form action="https://www.baidu.com">
          <button onClick={this.parentEvent}>提交</button>
        </form>
        {/*可以使用如下方法进行传参*/}
        <button onClick={ (e) => {this.parentEvent1('hello world', e)} }>提交1</button>
        {/*也可以使用如下方法进行传参，就是不使用箭头函数，但是要绑定this指针*/}
        <button onClick={ function (e) {this.parentEvent2('123', e)}.bind(this) }>提交2</button>
      </div>
    )
  }

  parentEvent = (e) => {
    // return false; // 无效
    console.log('clicked')
    e.preventDefault(); // 阻止form跳转
  }

  parentEvent1 = (msg, e) => {
    console.log(msg);
  }

  parentEvent2 = (msg, e) => {
    console.log(msg);
  }
}
```

