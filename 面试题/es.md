# var let const的区别

## var

用`var`声明的变量既是全局变量，也是顶层变量，存在变量提升的情况

在函数中使用使用`var`声明变量时候，该变量是局部的

```js
var a = 20
function change(){
    var a = 30
}
change()
console.log(a) // 20 
```

而如果在函数内不使用`var`，该变量是全局的

```js
var a = 20
function change(){
   a = 30
}
change()
console.log(a) // 30 
```

## let

let声明的变量只在所在的代码块内有效，且不存在变量提升

最后，`let`不允许在相同作用域中重复声明

```js
let a = 20
let a = 30
// Uncaught SyntaxError: Identifier 'a' has already been declared
```

## const

声明一个只读的常量，一旦声明不可改变

`const`实际上保证的并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动

对于简单类型的数据，值就保存在变量指向的那个内存地址，因此等同于常量

对于复杂类型的数据，变量指向的内存地址，保存的只是一个指向实际数据的指针，`const`只能保证这个指针是固定的，并不能确保改变量的结构不变

```js
const foo = {};

// 为 foo 添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123

// 将 foo 指向另一个对象，就会报错
foo = {}; // TypeError: "foo" is read-only
```

其它情况，`const`与`let`一致（块级作用域、不可重复声明）

# es6数组有哪些新增扩展

## ...

ES6通过扩展元素符`...`，好比 `rest` 参数的逆运算，将一个数组转为用逗号分隔的参数序列

```js
console.log(...[1, 2, 3])
// 1 2 3

console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

[...document.querySelectorAll('div')]
// [<div>, <div>, <div>]
```

通过扩展运算符实现的是浅拷贝，修改了引用指向的值，会同步反映到新数组

可以将字符串转为真正的数组

```javascript
[...'hello']
// [ "h", "e", "l", "l", "o" ]
```

## Array.from()

将两类对象转为真正的数组：类似数组的对象和可遍历`（iterable）`的对象（包括 `ES6` 新增的数据结构 `Set` 和 `Map`）

```js
let arrayLike = {
    '0': 'a',
    '1': 'b',
    '2': 'c',
    length: 3
};
let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
```

还可以接受第二个参数，用来对每个元素进行处理，将处理后的值放入返回的数组

```js
Array.from([1, 2, 3], (x) => x * x)
// [1, 4, 9]
```

## Array.of()

用于将一组值，转换为数组

```js
Array.of(3, 11, 8) // [3,11,8]
```

没有参数的时候，返回一个空数组

当参数只有一个的时候，实际上是指定数组的长度

参数个数不少于 2 个时，`Array()`才会返回由参数组成的新数组

```js
Array() // []
Array(3) // [, , ,]
Array(3, 11, 8) // [3, 11, 8]
```

## 实例对象新增方法

### find()

### findIndex()

### fill()

使用给定值，填充一个数组

```javascript
['a', 'b', 'c'].fill(7)
// [7, 7, 7]

new Array(3).fill(7)
// [7, 7, 7]
```

还可以接受第二个和第三个参数，用于指定填充的起始位置和结束位置

```js
['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
```

注意，如果填充的类型为对象，则是浅拷贝

### entries(),keys(),values()

`keys()`是对键名的遍历、`values()`是对键值的遍历，`entries()`是对键值对的遍历

### includes()

### flat

将数组扁平化处理，返回一个新数组，对原数据没有影响

```js
[1, 2, [3, 4]].flat()
// [1, 2, 3, 4]
```

`flat()`默认只会“拉平”一层，如果想要“拉平”多层的嵌套数组，可以将`flat()`方法的参数写成一个整数，表示想要拉平的层数，默认为1

```js
[1, 2, [3, [4, 5]]].flat()
// [1, 2, 3, [4, 5]]

[1, 2, [3, [4, 5]]].flat(2)
// [1, 2, 3, 4, 5]
```

### flatMap()

`flatMap()`方法对原数组的每个成员执行一个函数相当于执行`Array.prototype.map()`，然后对返回值组成的数组执行`flat()`方法。该方法返回一个新数组，不改变原数组

```js
// 相当于 [[2, 4], [3, 6], [4, 8]].flat()
[2, 3, 4].flatMap((x) => [x, x * 2])
// [2, 4, 3, 6, 4, 8]
```

# es6对象有哪些新增扩展

## 属性简写

当对象键名与对应值名相等的时候，可以进行简写

```js
const baz = {foo:foo}

// 等同于
const baz = {foo}
```

## 属性名表达式

允许字面量定义对象时，将表达式放在括号内

```js
let lastWord = 'last word';

const a = {
  'first word': 'hello',
  [lastWord]: 'world'
};

a['first word'] // "hello"
a[lastWord] // "world"
a['last word'] // "world"
```

## super

super指向当前对象的原型对象

```javascript
const proto = {
  foo: 'hello'
};

const obj = {
  foo: 'world',
  find() {
    return super.foo;
  }
};
Object.setPrototypeOf(obj, proto); // 为obj设置原型对象
obj.find() // "hello"
```

## 扩展运算符

在解构赋值中，未被读取的可遍历的属性，分配到指定的对象上面

```js
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
x // 1
y // 2
z // { a: 3, b: 4 }
```

注意：解构赋值必须是最后一个参数，否则会报错

ps：解构赋值是浅拷贝

## 对象新增方法

### Object.is()

严格判断两个值是否相等，与严格比较运算符（===）的行为基本一致，不同之处只有两个：一是`+0`不等于`-0`，二是`NaN`等于自身

### Object.assign()

```
Object.assign()`方法用于对象的合并，将源对象`source`的所有可枚举属性，复制到目标对象`target
```

`Object.assign()`方法的第一个参数是目标对象，后面的参数都是源对象

```javascript
const target = { a: 1, b: 1 };

const source1 = { b: 2, c: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```

### Object.setPrototypeOf()

### Object.getPrototypeOf()

### Object.keys()

### Object.values()

### Object..entries()

返回一个对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对的数组

```js
const obj = { foo: 'bar', baz: 42 };
Object.entries(obj)
// [ ["foo", "bar"], ["baz", 42] ]
```

### Object..fromEntries()

用于将一个键值对数组转为对象

```js
Object.fromEntries([
  ['foo', 'bar'],
  ['baz', 42]
])
// { foo: "bar", baz: 42 }
```

# es6函数有哪些新增扩展

## 参数

允许设置默认值

## 属性

### length属性

返回没有指定默认值的参数个数

```js
(function (a) {}).length // 1
(function (a = 5) {}).length // 0
(function (a, b, c = 5) {}).length // 2
```

`rest` 参数也不会计入`length`属性

```js
(function(...args) {}).length // 0
```

如果设置了默认值的参数不是尾参数，那么`length`属性也不再计入后面的参数了

```js
(function (a = 0, b, c) {}).length // 0
(function (a, b = 1, c) {}).length // 1
```

### name属性

返回函数名

`bind`返回的函数，`name`属性值会加上`bound`前缀

```javascript
function foo() {};
foo.bind({}).name // "bound foo"

(function(){}).bind({}).name // "bound "
```

## 箭头函数

# Set和Map

## Set

`Set`的实例关于增删改查的方法：

- add()
- delete()
- has()
- clear()：清楚所有成员

关于遍历的方法，有如下：

- keys()：返回键名的遍历器
- values()：返回键值的遍历器
- entries()：返回键值对的遍历器
- forEach()：使用回调函数遍历每个成员

实现并集、交集、和差集

```javascript
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
// Set {1, 2, 3, 4}

// 交集
let intersect = new Set([...a].filter(x => b.has(x)));
// set {2, 3}

// （a 相对于 b 的）差集
let difference = new Set([...a].filter(x => !b.has(x)));
// Set {1}
```

## Map

`Map`类型是键值对的有序列表，而键和值都可以是任意类型

`Map`本身是一个构造函数，用来生成 `Map` 数据结构

`Map` 结构的实例针对增删改查有以下属性和操作方法：

- size 属性
- set()
- get()
- has()：是否有某个键
- delete()
- clear()

遍历操作同Set

# 对Promise的理解

## 基本概念

- **状态**：一个 `Promise` 对象有以下几种状态：
  - `pending`（待定）：初始状态，既不是成功也不是失败。
  - `fulfilled`（已成功）：操作成功完成。
  - `rejected`（已失败）：操作失败。
- **值**：一个 `Promise` 对象有一个值，表示异步操作的结果。这个值只有在 `fulfilled` 状态时才有意义。
- **原因**：一个 `Promise` 对象有一个原因，表示异步操作失败的原因。这个原因只有在 `rejected` 状态时才有意义。

## 特点

- 对象的状态不受外界影响，只有异步操作的结果，可以决定当前是哪一种状态
- 一旦状态改变（从`pending`变为`fulfilled`和从`pending`变为`rejected`），就不会再变，任何时候都可以得到这个结果

## 用法

```
Promise`构造函数接受一个函数作为参数，该函数的两个参数分别是`resolve`和`reject
```

- `resolve`函数的作用是，将`Promise`对象的状态从“未完成”变为“成功”
- `reject`函数的作用是，将`Promise`对象的状态从“未完成”变为“失败”

### then()

`then`是实例状态发生改变时的回调函数，第一个参数是`resolved`状态的回调函数，第二个参数是`rejected`状态的回调函数

`then`方法返回的是一个新的`Promise`实例，也就是`promise`能链式书写的原因

```javascript
getJSON("/posts.json").then(function(json) {
  return json.post;
}).then(function(post) {
  // ...
});
```

### catch()

用于指定发生错误时的回调函数

```javascript
getJSON('/posts.json').then(function(posts) {
  // ...
}).catch(function(error) {
  // 处理 getJSON 和 前一个回调函数运行时发生的错误
  console.log('发生错误！', error);
});
```

`Promise`对象的错误具有“冒泡”性质，会一直向后传递，直到被捕获为止

```javascript
getJSON('/post/1.json').then(function(post) {
  return getJSON(post.commentURL);
}).then(function(comments) {
  // some code
}).catch(function(error) {
  // 处理前面三个Promise产生的错误
});
```

### finally()

`finally()`方法用于指定不管 Promise 对象最后状态如何，都会执行的操作

```javascript
promise
.then(result => {···})
.catch(error => {···})
.finally(() => {···});
```

## Promise.all() and Promise.race()

- `Promise.all`：接受一个包含多个 `Promise` 的数组，返回一个新的 `Promise`。当所有 `Promise` 都成功时，新的 `Promise` 变为 `fulfilled`，其值是所有 `Promise` 的结果组成的数组。如果有任何一个 `Promise` 失败，新的 `Promise` 变为 `rejected`，其原因是第一个失败的 `Promise` 的原因。
- `Promise.race`：接受一个包含多个 `Promise` 的数组，返回一个新的 `Promise`。当任意一个 `Promise` 完成时，新的 `Promise` 立即以相同的状态完成。

# 对generator的理解

## 基本概念

生成器（Generator）是一种可以在执行过程中暂停和恢复的函数。生成器函数可以生成一系列的值，而不是一次性返回单个值。生成器函数由 `function*` 关键字定义，并使用 `yield` 关键字来暂停函数执行和生成值。

```javascript
function* generatorFunction() {
  // 生成器函数体
  yield value1;
  yield value2;
  // ...
  return finalValue;
}
```

生成器函数与 `Promise` 结合使用，可以实现更简洁的异步代码控制流。在引入 `async/await` 之前，生成器函数是处理异步操作的一个重要工具。

## 异步解决方案

- `promise`和`async/await`是专门用于处理异步操作的

- `async`实质是`Generator`的语法糖，相当于会自动执行`Generator`函数
- `async`使用上更为简洁，将异步代码以同步的形式进行编写，是处理异步编程的最终方案

# Proxy

## 基本概念

`Proxy` 对象由一个目标对象和一个处理器对象（handler）组成。目标对象是你希望代理的对象，而处理器对象包含一系列捕获器（trap），这些捕获器定义了在特定操作发生时的行为。

```js
const proxy = new Proxy(target, handler);
```

- `target`：要代理的对象（可以是任何类型的对象，包括数组、函数等）。
- `handler`：一个对象，其属性是捕获器函数，这些函数定义了拦截操作的行为。

## Reflect

若需要在`Proxy`内部调用对象的默认行为，建议使用`Reflect`，其是`ES6`中操作对象而提供的新 `API`

基本特点：

- 只要`Proxy`对象具有的代理方法，`Reflect`对象全部具有，以静态方法的形式存在
- 修改某些`Object`方法的返回结果，让其变得更合理（定义不存在属性行为的时候不报错而是返回`false`）
- 让`Object`操作都变成函数行为

例如：

```javascript
let handler = {
  get: function(target, property, receiver) {
    console.log(`Getting ${property}`);
    return Reflect.get(target, property, receiver);
  },
  set: function(target, property, value, receiver) {
    console.log(`Setting ${property} to ${value}`);
    return Reflect.set(target, property, value, receiver);
  }
};

let obj = new Proxy({}, handler);

obj.name = 'Alice'; // Setting name to Alice
console.log(obj.name); // Getting name // Alice
```

# 模块

## 基本概念

模块（module）是一种将代码组织成独立、可重用单元的机制。模块化编程允许开发者将代码分割成逻辑上独立的部分，每个模块封装自己的功能和状态，从而提高代码的可维护性和可读性。

## 意义

1. **代码组织**：模块化使得代码更易于管理和维护，通过将相关功能封装在一个文件或模块中，减少了全局命名空间污染。
2. **重用性**：模块可以在不同项目中重复使用，提升开发效率。
3. **依赖管理**：模块化系统允许显式声明模块依赖关系，确保模块加载顺序和依赖的正确性。
4. **隔离性**：模块封装自己的作用域，避免了全局变量污染和命名冲突问题。

## ES6

### 导出

```javascript
// math.js
export const pi = 3.14159;

export function add(a, b) \{
  return a + b;
}

export class Circle \{
  constructor(radius) \{
    this.radius = radius;
  }
  
  getArea() \{
    return pi * this.radius * this.radius;
  }
}
```

### 导入

```javascript
// main.js
import \{ pi, add, Circle } from './math.js';

console.log(`Value of pi: $\{pi}`);
console.log(`Add 2 and 3: $\{add(2, 3)}`);

const circle = new Circle(5);
console.log(`Area of circle: $\{circle.getArea()}`);
```

### 默认导出

使用 `export default` 导出模块默认值，一个模块只能有一个默认导出。导入默认导出时，可以使用任意名称

## CommonJS

使用`module.exports`导出模块内容

使用`require`导入模块内容

# 对decorator的理解

## 基本概念

装饰器的主要作用是增强或改变类的行为，而不需要修改类本身的代码。

## 语法

在 TypeScript 中，装饰器的语法如下：

```typescript
function MyDecorator(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  // 装饰器逻辑
}
```

- `target`：被装饰的对象（类的原型或构造函数）。
- `propertyKey`：被装饰的属性或方法的名称。
- `descriptor`：属性描述符对象，包含关于属性或方法的信息。

## 方法装饰器

```typescript
function Log(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;

  descriptor.value = function (...args: any[]) {
    console.log(`Calling ${propertyKey} with arguments:`, args);
    const result = originalMethod.apply(this, args);
    console.log(`Result of ${propertyKey}:`, result);
    return result;
  };
}

class Calculator {
  @Log
  add(a: number, b: number): number {
    return a + b;
  }
}

const calculator = new Calculator();
calculator.add(2, 3); // 调用 add 方法时会记录日志
```

## 类装饰器

类装饰器用于修改类的构造函数或添加新的属性和方法。

```typescript
function AddTimestamp(constructor: Function) {
  constructor.prototype.timestamp = new Date();
}

@AddTimestamp
class User {
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}

const user = new User('Alice');
console.log(user.timestamp); // 类实例会有一个 timestamp 属性
```

## 属性装饰器

属性装饰器用于修改类属性的行为。

```typescript
function Readonly(target: any, propertyKey: string) {
  const descriptor: PropertyDescriptor = {
    get() {
      return 'This is a readonly property';
    },
    set() {
      throw new Error('Cannot set readonly property');
    }
  };

  Object.defineProperty(target, propertyKey, descriptor);
}

class Person {
  @Readonly
  name: string = 'John';
}

const person = new Person();
console.log(person.name); // 'This is a readonly property'
person.name = 'Doe'; // Error: Cannot set readonly property
```