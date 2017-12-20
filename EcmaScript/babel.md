# Babel的使用

- [Babel](#babel)
    - [Babel支持的语法特性](#babel%E6%94%AF%E6%8C%81%E7%9A%84%E8%AF%AD%E6%B3%95%E7%89%B9%E6%80%A7)
    - [babel-cli](#babel-cli)
    - [preset](#preset)
    - [webpack中使用babel](#webpack%E4%B8%AD%E4%BD%BF%E7%94%A8babel)
    - [polyfill](#polyfill)

Babel可以将ES6代码（目前也包括ES7,ES8）转换为ES5,使其可以在目前的浏览器或者NodeJS环境中执行。

## plugins

Babel通过**解析(parsing)**，**转换(transforming)**，**生成(generation)** 三个阶段完成代码编译.
Babel通过**插件(plugins)**的形式支持对特定语法的转换。（影响第二阶段transformation）

> ps: Babel插件在NPM的名称以`babel-plugin-`为前缀，如`transform-es2015-arrow-functions`在NPM名称为`babel-plugin-transform-es2015-arrow-functions`

目前Babel支持的语法特性(通过plugins形式)包括：

| 特性                                       | 插件名称 |
| ----------------------------------------- | ------: |
| [Arrow functions](https://babeljs.io/docs/plugins/transform-es2015-arrow-functions)(箭头函数) | `transform-es2015-arrow-functions` |
| [Async functions](https://babeljs.io/docs/plugins/syntax-async-functions)(async函数)|`syntax-async-functions`|
|[Async generator functions](https://babeljs.io/docs/plugins/syntax-async-functions)(async generator函数)|`syntax-async-generators`|
|[Block scoping](https://babeljs.io/docs/plugins/transform-es2015-block-scoping)(块级作用域)|`transform-es2015-block-scoping`|
|[Block scoped functions](https://babeljs.io/docs/plugins/transform-es2015-block-scoped-functions)(块级作用域函数)|`transform-es2015-block-scoped-functions`|
|[Classes](https://babeljs.io/docs/plugins/transform-es2015-classes)(类Class)|`transform-es2015-classes`|

## babel-cli

## preset

## webpack中使用babel

## polyfill