# ES6 - Set与Map集合

- [ES6 - Set与Map集合](#es6---set%E4%B8%8Emap%E9%9B%86%E5%90%88)
    - [1.Set](#1set)
    - [2.WeakSet](#2weakset)
    - [3.Map](#3map)
    - [4.WeakMap](#4weakmap)

---

## 1.Set

>定义:无重复元素的列表,重复性通过`Object.is()`判断

**构造函数:**
可接收所有*可迭代对象*作为参数

**元素操作方法:**

- `add(value)` 添加
- `delete(value)` 删除
- `has(value)` 是否存在
- `clear()` 清空

**特殊属性:**

- `size` 元素数量

**遍历方法:**

- `forEach(function(value,key,set){},[context]){}`

**迭代器:**

特点：key与value相同

- `keys()`
- `values()`
- `entries()`

**使用Set数组去重:**

```javascript
// 使用Array.from()
Array.from(new Set(arr));
// 或者使用解构
[...new Set(arr)];
```

## 2.WeakSet

> 定义:与Set类似，不同点在于存储的元素为**对象**的弱引用

与Set的区别

- 向`add(),has(),delete()`传入非对象参数会报错
- `WeakSet`不可迭代，因此不可使用`for-of`，不暴露任何迭代器
- `WeakSet`不支持`forEach()`方法
- `WeakSet`不支持`size`属性

## 3.Map

> 定义: 存储键值对的**有序**列表，**键**和**值**都可以为**任意类型**。

**构造函数:**
可接收键值对数组作为参数

```javascript
let map = new Map([["name":"Nicholas"],["age":25]]);
```

**键值对操作方法:**

- `set(key,value)` 添加/更新
- `get(key)` 读取
- `delete(key)` 删除
- `has(key)` 是否存在
- `clear()` 清空

**特殊属性:**

- `size` 键值对数量

**遍历方法:**

- `forEach(function(value,key,map){},[context]){}`

**迭代器:**

- `keys()`
- `values()`
- `entries()`

## 4.WeakMap

> 定义: 与Map类似, 不同点在于键值为**对象**(非null)的弱引用

`WeakMap`同样不可迭代,不支持`clear(),forEach(),keys(),values(),entries()`这些方法