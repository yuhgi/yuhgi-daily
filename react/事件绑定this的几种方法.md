# React事件处理函数绑定this的集中方法

[Follow me on GitHub](https://github.com/yuhgi/yuhgi-daily/tree/master/react)

- [React事件处理函数绑定this的集中方法](#react%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E5%87%BD%E6%95%B0%E7%BB%91%E5%AE%9Athis%E7%9A%84%E9%9B%86%E4%B8%AD%E6%96%B9%E6%B3%95)
    - [1. 在构造函数中绑定](#1-%E5%9C%A8%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0%E4%B8%AD%E7%BB%91%E5%AE%9A)
    - [2.使用class properties进行绑定](#2%E4%BD%BF%E7%94%A8class-properties%E8%BF%9B%E8%A1%8C%E7%BB%91%E5%AE%9A)
    - [3. 使用箭头函数](#3-%E4%BD%BF%E7%94%A8%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0)
    - [4. 使用bind()](#4-%E4%BD%BF%E7%94%A8bind)

目前React有三种方法可以创建组件，其中使用React.createClass()函数创建的组件，this会自动
绑定到组件的每个方法中；而使用Class Component或者Functional Component时，需要手动绑定this.

## 1. 在构造函数中绑定

```javascript
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

## 2.使用class properties进行绑定

class properties目前处于[state-2草案阶段](https://github.com/tc39/proposals)，[babel](https://babeljs.io/docs/plugins/transform-class-properties/)已经支持

```javascript
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  // Warning: this is *experimental* syntax.
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

## 3. 使用箭头函数

```javascript
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // This syntax ensures `this` is bound within handleClick
    return (
      <button onClick={(e) => this.handleClick(e)}>
        Click me
      </button>
    );
  }
}
```

这种方式有一个潜在的**性能问题**，就是每次组件渲染时，onClick的回调函数都是不同的匿名函数，如果这个组件把回调函数通过props传递到其子组件，那么由于每次组件的渲染时，由于传递的props中回调函数的变化，就会导致子组件的额外渲染（是不同的回调函数，但实际上处理逻辑完全相同）。

## 4. 使用bind()

```javascript
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // This syntax ensures `this` is bound within handleClick
    return (
      <button onClick={this.handleClick.bind(this)}>
        Click me
      </button>
    );
  }
}
```

bind跟使用箭头函数一样，实际上每次组件渲染时都生成了新的回调函数。

---

建议使用**构造函数中绑定**或者使用**class properties特性绑定**，但**bind**和**箭头函数**在特殊场景下需要使用，即需要传递额外参数的情况。

```javascript
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```