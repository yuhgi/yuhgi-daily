# JSX

[Follow me on GitHub](https://github.com/yuhgi/yuhgi-daily/tree/master/react)

- [JSX](#jsx)
    - [1. 为什么会有JSX？](#1-%E4%B8%BA%E4%BB%80%E4%B9%88%E4%BC%9A%E6%9C%89jsx%EF%BC%9F)
    - [2. JSX的基本使用](#2-jsx%E7%9A%84%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8)
        - [2.1 JSX中可直接包含Javascript表达式](#21-jsx%E4%B8%AD%E5%8F%AF%E7%9B%B4%E6%8E%A5%E5%8C%85%E5%90%ABjavascript%E8%A1%A8%E8%BE%BE%E5%BC%8F)
        - [2.2 JSX本身也是表达式](#22-jsx%E6%9C%AC%E8%BA%AB%E4%B9%9F%E6%98%AF%E8%A1%A8%E8%BE%BE%E5%BC%8F)
        - [2.3 使用JSX中指定属性](#23-%E4%BD%BF%E7%94%A8jsx%E4%B8%AD%E6%8C%87%E5%AE%9A%E5%B1%9E%E6%80%A7)
        - [2.4 使用JSX指定Children](#24-%E4%BD%BF%E7%94%A8jsx%E6%8C%87%E5%AE%9Achildren)
        - [2.5 JSX可以阻止注入式攻击](#25-jsx%E5%8F%AF%E4%BB%A5%E9%98%BB%E6%AD%A2%E6%B3%A8%E5%85%A5%E5%BC%8F%E6%94%BB%E5%87%BB)
    - [3. JSX进阶](#3-jsx%E8%BF%9B%E9%98%B6)
        - [3.1 JSX的编译](#31-jsx%E7%9A%84%E7%BC%96%E8%AF%91)
        - [3.2 指定React Element类型](#32-%E6%8C%87%E5%AE%9Areact-element%E7%B1%BB%E5%9E%8B)
        - [3.3 JSX中的prop](#33-jsx%E4%B8%AD%E7%9A%84prop)
        - [3.4 JSX中的Children](#34-jsx%E4%B8%AD%E7%9A%84children)

JSX是对`Javascript`的语法扩展，而不是一种模板语言。JSX不是字符串，也不是HTML。

## 1. 为什么会有JSX？

React认为渲染逻辑跟UI逻辑（事件如何处理，状态如何改变，数据如何展示）实际上天然相关的。
React并没有使用传统的将表现(markup)与逻辑(javascript)分离的方式，而是使用松耦合的组件将表现和逻辑组合到了一起。
JSX实际上是组件渲染的语法糖，其糅合了标记语言与UI对应的优点，同时可以直接处理Javascript代码。

>ps：**表现与处理逻辑分离**仍旧有很大意义，Presentation Component与Container Component的提出正式这一原则的应用。
在逻辑复杂的系统中，将状态抽取到Redux中进行统一管理，将处理逻辑抽取到Container Component中，将UI展示抽取到Presentation Component中。
实现了**数据模型**，**处理逻辑**，**数据展示**的分离。

## 2. JSX的基本使用

### 2.1 JSX中可直接包含Javascript表达式

JSX将Javascript表达式包裹在大括号{}中使用。

```javascript
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

### 2.2 JSX本身也是表达式

JSX在编译后实际上是**Javascript对象**，因此可以直接在if或者for循环中使用，也可以赋值给变量，或者作为函数参数传递，也可以作为函数返回值。

```javascript
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

### 2.3 使用JSX中指定属性

可以使用双引号指定字符串字面量

```javascript
const element = <div tabIndex="0"></div>;
```

也可以使用大括号指定Javascript表达式

```javascript
const element = <img src={user.avatarUrl}></img>;
```

>注意：JSX中的属性使用camelCase（与HTML不同）

### 2.4 使用JSX指定Children

```javascript
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

### 2.5 JSX可以阻止注入式攻击

React DOM默认在渲染前对JSX中的值进行转义，这样就避免了使用应用中未显式指定的值就行注入式攻击，可以帮助防范XSS攻击。

## 3. JSX进阶

### 3.1 JSX的编译

JSX提供了`React.createElement(component,props,...children)`函数的语法糖。

```javascript
<MyButton color="blue" shadowSize={2}>
  Click Me
</MyButton>
```

会编译成

```javascript
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'Click Me'
)
```

```javascript
<div className="sidebar" />
```

会编译成

```javascript
React.createElement(
  'div',
  {className: 'sidebar'},
  null
)
```

### 3.2 指定React Element类型

JSX标签决定了React Element的类型，如果首字符是大写，那么代表是React Component，如果首字符是小写，那么是HTML DOM。

- React以及组件必须在作用域中

如果是React Component，那么标签的名称就代表着保存React组件实例变量的名称，因此此变量必须在当前作用域中。
同时，JSX编译后也要使用到React变量，因此React变量也要保证在当前作用域中。
> PS: 使用**函数组件**的时候，会忘记导入React模块，此时就会出现错误提示（React is undefined），其实就是因为模块中未导入React。

```javascript
import React from 'react';
import CustomButton from './CustomButton';

// React与CustomButton都需要在作用域中
function WarningButton() {
  // return React.createElement(CustomButton, {color: 'red'}, null);
  return <CustomButton color="red" />;
}
```

- 可使用点标识符

如下面的`MyComponents.DatePicker`

```javascript
import React from 'react';

const MyComponents = {
  DatePicker: function DatePicker(props) {
    return <div>Imagine a {props.color} datepicker here.</div>;
  }
}

function BlueDatePicker() {
  return <MyComponents.DatePicker color="blue" />;
}
```

- 用户自定义组件首字母需大写

自定义组件的首字母需大写，HTML支持的tag名称都已经作为React内置的组件，需小写。

```javascript
import React from 'react';

// Correct! This is a component and should be capitalized:
function Hello(props) {
  // Correct! This use of <div> is legitimate because div is a valid HTML tag:
  return <div>Hello {props.toWhat}</div>;
}

function HelloWorld() {
  // Correct! React knows <Hello /> is a component because it's capitalized.
  return <Hello toWhat="World" />;
}
```

- 运行时动态选择组件类型

如果需要动态选择组件类型，那么将组件保存在常量中（首字母大写），然后在JSX标签中可使用此变量名。

```javascript
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
  photo: PhotoStory,
  video: VideoStory
};

function Story(props) {
  // Correct! JSX type can be a capitalized variable.
  const SpecificStory = components[props.storyType];
  return <SpecificStory story={props.story} />;
}
```

### 3.3 JSX中的prop

在JSX中有一下几种方式指定props

- 字符串字面量

使用引号包裹表示字符串字面量，所以下面两种方式是等同的。

```javascript
<MyComponent message="hello world" />

<MyComponent message={'hello world'} />
```

当使用字符串字面量的时候，其值会进行HTML解析，所以下面两个JSX表达式是等同的。

```javascript
<MyComponent message="&lt;3" />

<MyComponent message={'<3'} />
```

- Javascript表达式

使用大括号包裹

```javascript
<MyComponent foo={1 + 2 + 3 + 4} />
```

- 默认为'True'

如果prop不指定值，那么其值默认为`true`（其表现跟HTML的disabled,checked,readOnly属性类似）

```javascript
<MyTextBox autocomplete />

<MyTextBox autocomplete={true} />
```

- 延展属性

如果已经有props对象，可使用ES6的扩展运算符`...`传递整个props对象。以下两种方式等同

```javascript
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;
}
```

`...`运算符也可以用来对props对象进行分割，例如下面代码提取`kind`，将其他属性放入新的对象`other`。

```javascript
const Button = props => {
  const { kind, ...other } = props;
  const className = kind === "primary" ? "PrimaryButton" : "SecondaryButton";
  return <button className={className} {...other} />;
};

const App = () => {
  return (
    <div>
      <Button kind="primary" onClick={() => console.log("clicked!")}>
        Hello World!
      </Button>
    </div>
  );
};
```

**延展属性**会传递不必要的props给组件（或者是无效的HTML属性给DOM）,所以，**不要滥用**。

### 3.4 JSX中的Children

JSX表达式包含一个打开标签和一个关闭标签，在这两个标签之前的内容会作为一个特殊属性传递`props.children`。
有以下几种方式可以传递children:

- 字符串字面量

props.children就是字符串字面量`"Hello World!"`

```javascript
<MyComponent>Hello world!</MyComponent>
```

HTML会被解析,所以转义字符在JSX中跟HTML中使用方式一样

```javascript
<div>This is valid HTML &amp; JSX at the same time.</div>
```

JSX会移除行首和行尾的空白字符，也会移除空白行，临近标签的空白行也会移除，字符串中的换行会被作为一个空格处理。
以下几种方式是相同的

```javascript
<div>Hello World</div>

<div>
  Hello World
</div>

<div>
  Hello
  World
</div>

<div>

  Hello World
</div>
```

> 想用JSX表示多个空格，需要使用`&nbsp;`

- JSX表达式作为Children

可使用JSX元素作为Children，便于组件嵌套

```javascript
<MyContainer>
  <MyFirstComponent />
  <MySecondComponent />
</MyContainer>
```

可以嵌套不同类型的children（like HTML）

```javascript
<div>
  Here is a list:
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
  </ul>
</div>
```

React组件可以返回元素数组（不强制使用元素进行包裹）

```javascript
render() {
  // No need to wrap list items in an extra element!
  return [
    // Don't forget the keys :)
    <li key="A">First item</li>,
    <li key="B">Second item</li>,
    <li key="C">Third item</li>,
  ];
}
```

- Javascript表达式作为Children

可使用大括号`{}`直接包裹表达式作为children

```javascript
function Item(props) {
  return <li>{props.message}</li>;
}

function TodoList() {
  const todos = ['finish doc', 'submit pr', 'nag dan to review'];
  return (
    <ul>
      {todos.map((message) => <Item key={message} message={message} />)}
    </ul>
  );
}
```

也可以跟其他类型混合使用

```javascript
function Hello(props) {
  return <div>Hello {props.addressee}!</div>;
}
```

- 函数作为Children

`props.children`可以传递任何类型的数据，例如函数，在React渲染之前将其
转换为React可以识别的对象（字符串，React元素，及其数组）即可。

如下面`ListOfTenThings`传递给`Repeat`组件的`props.children`是一个函数，但是在`Repeat`组件渲染前，将其转换
为了React元素数组`items`

```javascript
// Calls the children callback numTimes to produce a repeated component
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
    items.push(props.children(i));
  }
  return <div>{items}</div>;
}

function ListOfTenThings() {
  return (
    <Repeat numTimes={10}>
      {(index) => <div key={index}>This is item {index} in the list</div>}
    </Repeat>
  );
}
```

- Boolean,Null,Undefined都将被忽略

`false,true,null,undefined`都是有效的children,但是都不渲染,以下几种方式相同

```javascript
<div />

<div></div>

<div>{false}</div>

<div>{null}</div>

<div>{undefined}</div>

<div>{true}</div>
```

因此，可以使用&运算符进行条件渲染

```javascript
<div>
  {showHeader && <Header />}
  <Content />
</div>
```

需要注意的是一些[falsy value](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)，例如`0`仍旧会被渲染。如果要作为渲染条件使用，请将其转换为`Boolean`.

此外，如果需要渲染`false,null,true,undefined`这些值，可将其转换为字符串