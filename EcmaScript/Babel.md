# Babel的使用

- [Babel](#babel)
    - [Babel支持的语法特性](#babel%E6%94%AF%E6%8C%81%E7%9A%84%E8%AF%AD%E6%B3%95%E7%89%B9%E6%80%A7)
    - [babel-cli](#babel-cli)
    - [preset](#preset)
    - [webpack中使用babel](#webpack%E4%B8%AD%E4%BD%BF%E7%94%A8babel)
    - [polyfill](#polyfill)

Babel可以将ES6代码（目前也包括ES7,ES8）转换为ES5,使其可以在目前的浏览器或者NodeJS环境中执行。

## Plugins和Presets

Babel通过**解析(parsing)**，**转换(transforming)**，**生成(generation)** 三个阶段完成代码编译.
Babel通过**插件(plugins)**的形式支持对特定语法的转换。（影响第二阶段transformation）

> ps: Babel插件在NPM的名称以`babel-plugin-`为前缀，如`transform-es2015-arrow-functions`在NPM名称为`babel-plugin-transform-es2015-arrow-functions`

将一系列插件组合到一起，就是Presets，表示一个插件数组。

目前官方的Presets

- env
- es2015
- es2016
- es2017
- latest (deprecated in favor of env)
- react
- flow

目前`env`包括了`es2015`,`es2016`,`es2017`。可通过配置减少一些不必要的转换。

实验中的Presets

- Stage 0 - Strawman：任何人都可以提出自己的想法
- Stage 1 - Proposal：有TC39会员带头，值得跟进
- Stage 2 - Draft：草案
- Stage 3 - Candidate：候选阶段
- Stage 4 - Finished：已准备就绪
