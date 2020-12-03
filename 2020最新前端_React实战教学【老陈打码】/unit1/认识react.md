# 认识React

## 特点：

- 声明式的设计
- 高效，采用虚拟DOM来实现DOM的渲染，最大限度的减少DOM的操作。
- 灵活，跟其他库灵活搭配使用。
- JSX，俗称JS里面写HTML，JavaScript 语法的扩展。
- 组件化，模块化。代码容易复用，2016年之前大型项目非常喜欢react
- 单向数据流。没有实现数据的双向绑定。数据-》视图-》事件-》数据

## 创建项目

1. 通过script引入使用，仅用于学习调试使用

```js
<script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
```

2. 通过react的脚手架，创建项目进行开发，部署。

- 安装脚手架`Create React App`。

```sh
cnpm i -g create-react-app
```

- 创建项目

```sh
create-react-app 项目名称
```