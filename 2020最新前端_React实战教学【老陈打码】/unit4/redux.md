# redux

解决React数据管理(状态管理)，用于中大型，数据比较庞大，组件之间数据交互多的情况下使用。如果你不知道是否需要使用Redux，那么你就不需要用它!

- 解决组件的数据通信。
- 解决数据和交互较多的应用

Redux只是一种状态管理的解决方案!

- Store:数据仓库， 保存数据的地方。
- State:state是1个对象，数据仓库里的所有数据都放到1个state里。
- Action:1个动作，触发数据改变的方法。
- Dispatch:将动作触发成方法
- Reducer:是1个函数，通过获取动作，改变数据，生成1个新state。从而改变页面

## 安装

```bash
cnpm i redux --save
```

## 初始化数据

```js
// 创建仓库
const store = createStore(reducer)

// 用于通过动作，创建新的state
// reducer有2个作用，1：初始化数据；2：通过获取动作，改变数据
const reducer = function(state = { num: 0 }, action) {
  console.log(action);
  switch(action.type) {
    case 'add':
      state.num++;
      break;
    case 'decrement':
      state.num--;
      break;
    default:
      break;
  }
}
```

## 获取数据

```js
let state = store.getState()
```

## 修改数据（通过动作修改数据）

```js
store.dispatch({ type: 'add', content: { id: 1, msg: 'helloworld' } })
```

## 修改视图（监听数据的变化，重新渲染）

```js
store.subscribe(() => {
  ReactDOM.render(<Counter />, document.querySelector('#rrot'))
})
```

## 完整示例

```js
import { createStore } from 'redux';

// 初始化数据
let reducer = function(store = { num: 0 }, action) {
  switch(action.type) {
    case 'add':
      store.num++;
      break;
    case 'decrement':
      store.num--;
      break;
    default:
      break;
  }
  return { ...store };
}

// 创建仓库
const store = createStore(reducer);

// 点击+1事件，add
function add() {
  store.dispatch({ type: 'add' });
  console.log('add')
}

// 点击-1事件
function decrement() {
  store.dispatch({ type: 'decrement' });
  console.log('decrement')

}

function App(props) {
  const state = store.getState();
  return (
    <div>
      <p>计数器：{ state.num }</p>
      <button onClick={add}>+1</button>
      <button onClick={decrement}>-1</button>
    </div>
  )
}

// 渲染组件
ReactDOM.render(
  <App></App>,
  document.getElementById('root')
);

// 监听store，若修改重新渲染
store.subscribe(() => {
  ReactDOM.render(
    <App></App>,
    document.getElementById('root')
  );
})
```