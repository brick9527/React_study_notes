# React JSX

# 优点

- JSX执行更快，编译为JavaScript代码时进行了优化
- 类型更安全，编译过程如果出错就不能编译，及时发现错误
- JSX编写模板更加简单快速。( 不要跟VUE比)

# 注意

- JSX必须要有根节点。
- 正常的普通HTML元素要小写。如果是大写，默认认为是组件。

# demo1

```js
let man = '发烧';

let element2 = (
  <div>
    <span>横着躺</span>
    <span>竖着躺</span>
  </div>
)

console.log(element2) // element2是一个js对象

let element = (
  <div>
    <h1>今天是否隔离</h1>
    <h2>{ man === '发烧' ? <button>隔离</button> : element2 }</h2>
  </div>
)

ReactDOM.render(
  element,
  document.getElementById('root')
)
```

# demo2

写`class`的时候，尽可能写成`className`。如果写`class`可能存在BUG，因为`class`在js中是一个关键词，容易冲突

`style.css`

```css
.redBg {
  background-color: red;
}
```

`index.js`

```js
import * from 'style.css';

let type = 'redBg';
let logo = 'https://www.baidu.com/img/flexible/logo/pc/result.png';
let element = (
  <div className={type}>
    <span>hello world</span>
    <img src={logo}/>
  </div>
)

ReactDOM.render(
  element,
  document.getElementById('root')
)
```

# JSX表达式

1. 由HTML元素构成
2. 中间如果需要插入变量用`{}`
3. `{}`可以使用表达式
4. `{}`表达式中可以使用JSX对象（见demo1）
5. 属性和html内容一样都是用`{}`来插入内容（见demo2）