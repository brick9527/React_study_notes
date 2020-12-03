# React样式和注释

# React Style

```js
// 注意要使用驼峰命名法
let exampleStyle = {
  background: 'skyblue',
  borderBottom: '4px solid black'
}

let element = (
  <div>
    <h1 style={exampleStyle}>hello world</h1>
  </div>
)

ReactDOM.render(
  element,
  document.getElementById('root')
)
```

要想style中不使用驼峰式命名，可以使用引号：

```js
let exampleStyle = {
  background: 'skyblue',
  'border-bottom': '4px solid black'
}
```

以下这样的style写法，他不会自动合并两个style。**style的值必须为对象格式。**

```js
let exampleStyle = {
  background: 'skyblue',
  borderBottom: '4px solid black'
}

// 要报错
let element = (
  <div>
    <h1 style="height:200px;" style={exampleStyle}>hello world</h1> 
  </div>
)
```

`class`值也不会自动合并

```js
let classStr = 'redBg'

// 只会显示一个class
let element = (
  <div className="other" className={classStr}>
    <span>hello world</span>
  </div>
)
```

`class`合并写法：

```js
let classStr = 'redBg'

let element = (
  <div className={'other ' + classStr}>
    <span>hello world</span>
  </div>
)
```

如果`class`使用数组写法：

```js
let classStr = ['other', 'redBg']

let element = (
  <div className={ classStr.join(' ') }>
    <span>hello world</span>
  </div>
)
```

# 注释

```js
let classStr = ['other', 'redBg']

let element = (
  {/* 这里写注释 */}
  <div className={classStr.join(' ')}>
    <span>hello world</span>
  </div>
)
```