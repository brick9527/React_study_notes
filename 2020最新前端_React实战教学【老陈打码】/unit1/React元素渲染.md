# React元素渲染

使用JSX的写法，可以创建JS元素对象

```js
let h1 = <h1>hello world</h1>
```

**注意：**JSX元素对象，或者组件对象，必须只有1个根元素（根节点）


函数式组件开发

```js
function Clock() {
  return (
    <div>
      <h1>现在的时间是:{props.date.toLocaleTimeString()}</h1>
      <h2>这是函数式组件开发</h2>
    </div>
  )
}

function run() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  )
}

setInterval(run, 1000);

```