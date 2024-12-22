# JS数据类型

## 基本类型

- Number
- String
- Boolean
- Undefined
- null
- symbol ：Symbol （符号）是原始值，且符号实例是唯一、不可变的。符号的用途是确保对象属性使用唯一标识符，不会发生属性冲突的危险

## 引用类型

- Object
- Array
- Function

## 区别

基本数据类型和引用数据类型存储在内存中的位置不同：

- 基本数据类型存储在栈中
- 引用类型的对象存储于堆中

# 数组常用方法

## 操作方法

### 增

- push()：添加到数组末尾
- unshift()：添加到数组开头
- splice()：start，delete_num，item...改变原数组
- concat()

### 删

- pop()
- shift()
- splice()
- slice()：保留index从start到end的元素，不改变原数组

### 改

- splice()

### 查

- indexOf()
- includes()
- find()

## 排序方法

- reverse()
- sort：接受一个比较函数判断哪个值排在前面

## 转换方法

- jion()：返回包含数组所有项的字符串（以jion的参数为分割符）

## 迭代方法

- some()
- every()
- forEach()
- filter()
- map()

# 字符串常用方法

## 操作方法

### 增

- concat()

### 删

- slice()
- substr()
- substring()

### 改

- trim()	trimLeft()	trimRight()
- repeat()：接受一个整数参数，表示要将字符串复制多少次
- padStart()padEnd()：第一个参数表示指定长度，第二参数表示填充字符，不满足长度以该字符填充字符串（头或尾）
- toLowerCase()    toUpperCase()

### 查

- charAt()
- indexOf()
- startWith()：是否以某个字符串开头，返回布尔值
- includes()

## 转换方法

- split()

## 模版匹配方法

- match()
- search()
- replace()：但只修改第一个匹配到的字符串

# JS类型转换

## 显示转换

- Number()
- parseInt()
- String()
- Boolean()

## 隐式转换

即自动变化类型

我们这里可以归纳为两种情况发生隐式转换的场景：

- 比较运算（`==`、`!=`、`>`、`<`）、`if`、`while`需要布尔值地方
- 算术运算（`+`、`-`、`*`、`/`、`%`）

# 浅拷贝和深拷贝

## 浅拷贝

浅拷贝，指的是创建新的数据，这个数据有着原始数据属性值的一份精确拷贝

如果属性是基本类型，拷贝的就是基本类型的值。如果属性是引用类型，拷贝的就是内存地址

- Object.assign()
- slice()
- concat()
- 拓展运算符

## 深拷贝

深拷贝开辟一个新的栈，两个对象属完全相同，但是对应两个不同的地址，修改一个对象的属性，不会改变另一个对象的属性.

- _.cloneDeep()
- JSON.stringify()

# 闭包

## 什么是闭包

闭包是指在一个函数内部定义的函数可以访问其外部函数的变量，即使外部函数已经执行完毕并退出了作用域。简单来说，闭包使得内部函数“记住”了它创建时的环境（作用域）。

## 闭包的基本原理

闭包的形成依赖于以下几个关键点：

1. **函数嵌套**：一个函数内部定义了另一个函数。
2. **变量的作用域链**：内部函数可以访问外部函数的变量。
3. **内部函数被外部引用**：内部函数被外部作用域引用，从而使得外部函数的变量不会被垃圾回收机制回收。

## 实际应用

闭包可以用于创建私有变量和方法，从而实现数据隐藏和封装。

```javascript
function createCounter() {
    let count = 0;
    
    return {
        increment: function() {
            count++;
            return count;
        },
        decrement: function() {
            count--;
            return count;
        }
    };
}

const counter = createCounter();
console.log(counter.increment()); // 输出：1
console.log(counter.increment()); // 输出：2
console.log(counter.decrement()); // 输出：1
```

# 作用域链

## 作用域分类

### 全局作用域

任何不在函数中或是大括号中声明的变量，都是在全局作用域下，全局作用域下声明的变量可以在程序的任意位置访问

### 函数作用域

函数作用域也叫局部作用域，如果一个变量是在函数内部声明的它就在一个函数作用域下面。这些变量只能在函数内部访问，不能在函数以外去访问

### 块级作用域

## 词法作用域

词法作用域，又叫静态作用域，变量被创建时就确定好了，而非执行阶段确定的。也就是说我们写好代码时它的作用域就确定了，`JavaScript` 遵循的就是词法作用域

## 作用域链

使用一个变量时，会先在当前作用域下去寻找该变量，若没找到，再往上层作用域去找，直至全局作用域。

# 原型、原型链

## 原型

每个对象拥有一个原型对象

```js
function doSomething(){}
console.log( doSomething.prototype );
```

consoloe输出

```js
{
    constructor: ƒ doSomething(),
    __proto__: {
        constructor: ƒ Object(),
        hasOwnProperty: ƒ hasOwnProperty(),
        isPrototypeOf: ƒ isPrototypeOf(),
        propertyIsEnumerable: ƒ propertyIsEnumerable(),
        toLocaleString: ƒ toLocaleString(),
        toString: ƒ toString(),
        valueOf: ƒ valueOf()
    }
}
```

原型对象有一个自有属性`constructor`，这个属性指向该函数

## 原型链

原型链是由对象及其原型对象组成的一条链，用于实现属性和方法的继承。当访问一个对象的属性或方法时，JavaScript 引擎会首先查找对象自身的属性或方法，如果没有找到，则会沿着原型链逐级向上查找，直到找到该属性或方法或到达原型链的顶端（即 `null`）

## 实际应用

1. **继承**：通过原型链可以实现对象之间的继承，使得子对象能够继承父对象的属性和方法。
2. **方法共享**：将方法定义在原型对象上，可以实现所有实例对象共享这些方法，节省内存。

# this对象的理解

## this的使用场景

### 全局上下文

在全局上下文中（即在任何函数之外），`this` 指向全局对象。在浏览器中，全局对象是 `window`。

```javascript
console.log(this); // 在浏览器中输出：Window
```

### 函数调用

在普通函数调用中，`this` 的值取决于函数的调用方式。在非严格模式下，`this` 指向全局对象；在严格模式下，`this` 是 `undefined`。

```javascript
function showThis() {
    console.log(this);
}

showThis(); // 非严格模式下输出：Window（严格模式下输出：undefined）
```

### 方法调用

当函数作为对象的方法被调用时，`this` 指向调用该方法的对象。

### 构造函数调用

当使用 `new` 关键字调用构造函数时，`this` 指向新创建的实例对象。

### 箭头函数

箭头函数没有自己的 `this` 值，箭头函数中的 `this` 继承自外层（定义时的）上下文。

```javascript
const obj = {
    name: 'Alice',
    getName: function() {
        const innerFunction = () => {
            console.log(this.name);
        };
        innerFunction();
    }
};

obj.getName(); // 输出：Alice
```

### 事件处理器

在事件处理器中，`this` 通常指向触发事件的 DOM 元素。

```javascript
document.getElementById('myButton').addEventListener('click', function() {
    console.log(this); // 输出：触发事件的按钮元素
});
```

## 常见陷阱

### 丢失this

在回调函数中，`this` 的值可能会丢失，导致意外的行为。

```javascript
const obj = {
    name: 'Alice',
    getName: function() {
        setTimeout(function() {
            console.log(this.name); // 输出：undefined
        }, 1000);
    }
};

obj.getName();
```

可以使用箭头函数解决这个问题，因为箭头函数不会重新绑定 `this`。

```javascript
const obj = {
    name: 'Alice',
    getName: function() {
        setTimeout(() => {
            console.log(this.name); // 输出：Alice
        }, 1000);
    }
};

obj.getName();
```

### 方法赋值

将对象的方法赋值给一个变量后调用，会导致 `this` 丢失。

```javascript
const obj = {
    name: 'Alice',
    getName: function() {
        console.log(this.name);
    }
};

const getName = obj.getName;
getName(); // 输出：undefined（非严格模式下输出：undefined）
```

可以使用 `bind` 方法解决这个问题。

```javascript
const getName = obj.getName.bind(obj);
getName(); // 输出：Alice
```

ps：我个人理解，这可能是因为赋值getName时，只赋值了obj的getName方法，而其他属性没有传递，this.name找不到定义所以undefined，而bind方法将getName方法与obj进行绑定

# 执行上下文和执行栈

## 执行上下文

### 类型

- 全局执行上下文：只有一个，浏览器中的全局对象就是 `window`对象，`this` 指向这个全局对象
- 函数执行上下文：存在无数个，只有在函数被调用的时候才会被创建，每次调用函数都会创建一个新的执行上下文
- Eval 函数执行上下文： 指的是运行在 `eval` 函数中的代码，很少用而且不建议使用

### 生命周期

1. **创建阶段**：
   - **变量对象（Variable Object, VO）**：创建变量对象，存储函数参数、内部变量和函数声明。在函数执行上下文中，这个对象称为活动对象（Activation Object, AO）。
   - **作用域链（Scope Chain）**：创建作用域链，包含当前执行上下文的变量对象和所有父执行上下文的变量对象。
   - **确定 `this` 的值**：根据调用方式确定 `this` 的值。
2. **执行阶段**：
   - **变量赋值**：执行代码，变量和函数声明被提升（Hoisting），并进行变量赋值。
   - **执行代码**：按照代码顺序执行具体的逻辑。
3. **回收阶段**：
   - 执行上下文出栈等待虚拟机回收执行上下文

## 执行栈

### 工作原理

1. **全局上下文入栈**：程序开始时，全局执行上下文被创建并压入执行栈。
2. **函数调用入栈**：每当一个函数被调用时，都会创建一个新的执行上下文并压入栈顶。
3. **函数执行完毕出栈**：当函数执行完毕后，其执行上下文会从栈顶弹出，控制权返回到上一个执行上下文。‘

# 事件模型

## 事件流

事件流描述了事件在 DOM 树中的传播过程，分为三个阶段：

1. **事件捕获阶段**：事件从根节点向目标节点传播。
2. **目标阶段**：事件在目标节点上触发。
3. **事件冒泡阶段**：事件从目标节点向根节点传播。

事件冒泡是一种从下往上的传播方式，由最具体的元素（触发节点）然后逐渐向上传播到最不具体的那个节点，也就是`DOM`中最高层的父节点

# typeof和instanceof的区别

- typeof会返回一个变量的基本类型，返回一个字符串
- instanceof用于检测构造函数的prototype是否出现在实例对象的原型链上，返回一个布尔值

# 事件代理

## 定义

俗地来讲，就是把一个元素响应事件（`click`、`keydown`......）的函数委托到另一个元素

## 应用场景

如果我们有一个列表，列表之中有大量的列表项，我们需要在点击列表项的时候响应一个事件，如果给每个列表项都绑定一个函数，十分消耗内存，这时候就可以事件委托，把点击事件绑定在父级元素`ul`上面，然后执行事件的时候再去匹配目标元素。

还有一种是上述列表项并不多，我们给每个列表项都绑定了事件，使用事件委托动态实现每次列表的增加都给元素绑定事件

```html
<input type="button" name="" id="btn" value="添加" />
<ul id="ul1">
    <li>item 1</li>
    <li>item 2</li>
    <li>item 3</li>
    <li>item 4</li>
</ul>
```

```js
const oBtn = document.getElementById("btn");
const oUl = document.getElementById("ul1");
const num = 4;

//事件委托，添加的子元素也有事件
oUl.onclick = function (ev) {
    ev = ev || window.event;
    const target = ev.target || ev.srcElement;
    if (target.nodeName.toLowerCase() == 'li') {
        console.log('the content is: ', target.innerHTML);
    }

};

//添加新节点
oBtn.onclick = function () {
    num++;
    const oLi = document.createElement('li');
    oLi.innerHTML = `item ${num}`;
    oUl.appendChild(oLi);
};
```

# new操作符干了什么

## 流程

1. 创建一个空对象obj

2. 将这个对象的`[[Prototype]]` 设置为构造函数的 `prototype` 属性

3. 绑定this，

4. 调用构造函数，并将 `this` 绑定到新创建的对象上：

   ```javascript
   let result = Person.call(obj, 'Alice', 30);
   ```

5. 返回对象，如果构造函数显式返回一个对象，则返回该对象；否则，返回新创建的对象：

   ```javascript
   return typeof result === 'object' && result !== null ? result : obj;
   ```

# apply call bind区别

## 作用

`call`、`apply`、`bind`作用是改变函数执行时的上下文，简而言之就是改变函数运行时的`this`指向

## apply

`apply`接受两个参数，第一个参数是`this`的指向，第二个参数是函数接受的参数，以**数组**的形式传入

## call

`call`方法的第一个参数也是`this`的指向，后面传入的是一个参数列表

## bind

`bind` 方法用于创建一个新的函数，这个新的函数在调用时 `this` 值被指定为 `bind` 的第一个参数，并且预先传入部分参数。

```javascript
function greet(greeting, punctuation) {
    console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: 'Alice' };

const greetPerson = greet.bind(person, 'Hello');
greetPerson('!');
```

在这个示例中，`greet` 函数被 `bind` 生成了一个新的函数 `greetPerson`，这个函数的 `this` 被**永久**绑定为 `person` 对象，并且预先传入了第一个参数 `'Hello'`。调用 `greetPerson` 时，仍然可以传入其他参数。

# ajax

## 基本原理

AJAX 的核心是 `XMLHttpRequest` 对象（在现代浏览器中，也可以使用 `fetch` API）。它允许浏览器向服务器发送 HTTP 请求并处理服务器的响应，而无需刷新页面。

## 工作流程

1. **创建 `XMLHttpRequest` 对象**：浏览器创建一个 `XMLHttpRequest` 对象。
2. **配置请求**：使用 `open` 方法配置请求类型（如 `GET` 或 `POST`）、URL 和是否异步。
3. **发送请求**：使用 `send` 方法发送请求。如果是 `POST` 请求，还需要设置请求头并传递请求体。
4. **监听响应**：通过 `onreadystatechange` 事件处理程序或 `readystatechange` 事件监听器来处理服务器的响应。
5. **处理响应数据**：在响应到达后，检查响应的状态码和响应内容，并根据需要更新网页内容。

# 正则表达式

## 基本概念

1. **字面字符**：直接匹配字符本身。例如，正则表达式 `abc` 可以匹配字符串 "abc"。
2. **元字符**：具有特殊含义的字符，用于构建复杂的匹配模式。常见的元字符包括 `.`、`*`、`+`、`?`、`^`、`$`、`[]`、`{}`、`()`、`|`、`\` 等。

## 元字符及其含义

- **`.`**：匹配除换行符以外的任意单个字符。例如，正则表达式 `a.b` 可以匹配 "aab"、"acb" 等。
- **`\*`**：匹配前面的子表达式零次或多次。例如，正则表达式 `ab*c` 可以匹配 "ac"、"abc"、"abbc" 等。
- **`+`**：匹配前面的子表达式一次或多次。例如，正则表达式 `ab+c` 可以匹配 "abc"、"abbc" 等，但不匹配 "ac"。
- **`?`**：匹配前面的子表达式零次或一次。例如，正则表达式 `ab?c` 可以匹配 "ac" 和 "abc"。
- **`^`**：匹配字符串的开始位置。例如，正则表达式 `^abc` 只能匹配以 "abc" 开头的字符串。
- **`$`**：匹配字符串的结束位置。例如，正则表达式 `abc$` 只能匹配以 "abc" 结尾的字符串。
- **`[]`**：匹配方括号内的任意一个字符。例如，正则表达式 `[abc]` 可以匹配 "a"、"b" 或 "c"。
- **`{}`**：限定前面的子表达式的出现次数。例如，正则表达式 `a{2,3}` 可以匹配 "aa" 或 "aaa"。
- **`()`**：用于分组和捕获子表达式。例如，正则表达式 `(abc)+` 可以匹配 "abc"、"abcabc" 等。
- **`|`**：表示逻辑或。例如，正则表达式 `a|b` 可以匹配 "a" 或 "b"。
- **`\`**：转义字符，用于匹配元字符本身。例如，正则表达式 `\.` 可以匹配 "."。

# 事件循环

## 基本概念

1. **调用栈（Call Stack）**：
   - 调用栈是一个 LIFO（后进先出）的数据结构，用于存储正在执行的函数调用。
   - 当一个函数被调用时，它会被压入调用栈；当函数执行完毕时，它会从调用栈中弹出。
2. **任务队列（Task Queue 或者 Event Queue）**：
   - 任务队列是一个 FIFO（先进先出）的数据结构，用于存储异步任务的回调函数。
   - 常见的任务队列有宏任务队列（Macro Task Queue）和微任务队列（Micro Task Queue）。
3. **事件循环（Event Loop）**：
   - 事件循环不断地检查调用栈是否为空。如果调用栈为空，它会从任务队列中取出第一个任务并将其压入调用栈执行。
   - 事件循环的工作流程是一个不断重复的过程，确保异步任务能够被及时处理。

## 宏任务和微任务

- **宏任务（Macro Task）**：
  - 宏任务包括 `setTimeout`、`setInterval`、`I/O` 操作、UI 渲染等。
  - 每次事件循环的开始，都会先处理一个宏任务，然后检查微任务队列。
- **微任务（Micro Task）**：
  - 微任务包括 `Promise.then`、`MutationObserver`、`process.nextTick`（Node.js）等。
  - 微任务队列会在每个宏任务执行完之后立即执行，直到微任务队列为空。

## 工作流程

1. **执行全局代码**：将全局代码压入调用栈并执行，直到调用栈为空。
2. **执行微任务**：检查并执行微任务队列中的所有微任务，直到微任务队列为空。
3. **执行宏任务**：从宏任务队列中取出一个任务并执行。
4. **重复步骤 2 和 3**：事件循环不断重复上述过程，确保所有任务都能被处理。

# 常见DOM操作

## 创建节点

- createElement
- createTextNode
- createDocumentFragment
- createAttribute

## 获取节点

- querySelector
- querySelectorAll

## 更新节点

- innerHTML
- innerText textContent
- style

## 添加节点

- innerHTML
- appendChild
- insertBefore
- setAttribute

## 删除节点

- removeChild

# BOM

## 与DOM区别

浏览器的全部内容可以看成DOM，整个浏览器可以看成BOM

## window

window是BOM的核心对象。`window`对象有双重角色，即是浏览器窗口的一个接口，又是全局对象。因此所有在全局作用域中声明的变量、函数都会变成`window`对象的属性和方法

## navigator

包含有关浏览器的信息，如名称、版本、平台等。

## location

包含当前文档的 URL 信息，并提供了操作 URL 的方法。

## history

包含浏览器的历史记录，并提供了导航历史记录的方法。

## screen

包含有关用户屏幕的信息，如宽度、高度、颜色深度等。

# 尾递归

尾递归（Tail Recursion）是一种递归形式，其中递归调用是函数中的最后一个操作。尾递归优化（Tail Call Optimization, TCO）是编译器或解释器的一种优化技术，它可以在满足尾递归条件时，将递归调用转换为迭代，从而避免函数调用栈的增长，提升性能并防止栈溢出。

#### 普通递归

```javascript
function factorial(n) {
    if (n === 0) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}

console.log(factorial(5)); // 输出 120
```

在这个普通递归函数中，递归调用 `factorial(n - 1)` 不是函数的最后一个操作，因为它需要乘以 `n`。

#### 尾递归

```javascript
function factorialTailRecursive(n, acc = 1) {
    if (n === 0) {
        return acc;
    } else {
        return factorialTailRecursive(n - 1, n * acc);
    }
}

console.log(factorialTailRecursive(5)); // 输出 120
```

# 垃圾回收机制

垃圾收集器会定期（周期性）找出那些不在继续使用的变量，然后释放其内存

通常情况下有两种实现方式：

- 标记清除
- 引用计数

## 标记清除

当变量进入执行环境是，就标记这个变量为“进入环境“。进入环境的变量所占用的内存就不能释放，当变量离开环境时，则将其标记为“离开环境“。随后垃圾回收程序做一次内存清理，销毁带标记的所有值并收回它们的内存

## 引用计数

语言引擎有一张"引用表"，保存了内存里面所有的资源（通常是各种值）的引用次数。如果一个值的引用次数是`0`，就表示这个值不再用到了，因此可以将这块内存释放

# js本地存储方式

## cookie

小型文本文件，为了辨别用户身份而储存在用户本地终端上的数据。是为了解决 `HTTP`无状态导致的问题

## localStorage

- LocalStorage 提供了一种在客户端存储大量数据的方法，数据没有过期时间，除非手动删除。
- 数据以键值对的形式存储，并且可以跨页面共享。

## sessionStorage

`sessionStorage`和 `localStorage`使用方法基本一致，唯一不同的是生命周期，一旦页面（会话）关闭，`sessionStorage` 将会删除数据

## indexedDB

- IndexedDB 是一种低级 API，用于在客户端存储大量结构化数据。
- 它是一个 NoSQL 数据库，可以存储大量数据，并且支持事务。

# 函数式编程

函数式编程是一种强大的编程范式，通过强调纯函数、不可变性和高阶函数等概念，可以编写出更简洁、可维护和可测试的代码。

## 纯函数

纯函数是指在相同输入下总是产生相同输出，并且没有任何副作用（即不改变外部状态）

## 不可变性

在函数式编程中，数据结构是不可变的，即一旦创建就不能改变。任何对数据的修改都会返回一个新的数据结构，而不是在原数据上进行修改。

## 高阶函数

高阶函数是指接受一个或多个函数作为参数，或返回一个函数作为结果的函数。

# 函数缓存

就是将函数运算过的结果进行缓存

## 实现

### 闭包

### 柯里化

### 高阶函数

## 应用场景

- 对于昂贵的函数调用，执行复杂计算的函数
- 对于具有有限且高度重复输入范围的函数
- 对于具有重复输入值的递归函数
- 对于纯函数，即每次使用特定输入调用时返回相同输出的函数

# js数字精度丢失

## 存储方式

在`JavaScript`中，现在主流的数值类型是`Number`，而`Number`采用的是`IEEE754`规范中64位双精度浮点数编码

64位比特又可分为三个部分：

- 符号位S：第 1 位是正负数符号位（sign），0代表正数，1代表负数
- 指数位E：中间的 11 位存储指数（exponent），用来表示次方数，可以为正负数。在双精度浮点数中，指数的固定偏移量为1023
- 尾数位M：最后的 52 位是尾数（mantissa），超出的部分自动进一舍零

## 解决方案

理论上用有限的空间来存储无限的小数是不可能保证精确的，但我们可以处理一下得到我们期望的结果

当你拿到 `1.4000000000000001` 这样的数据要展示时，建议使用 `toPrecision` 凑整并 `parseFloat` 转成数字后再显示，如下：

```js
parseFloat(1.4000000000000001.toPrecision(12)) === 1.4  // True
```

# 防抖和节流

## 防抖

防抖的原理是将多次执行变为最后一次执行，即在事件触发后，只有在指定时间内没有再次触发事件时，才会执行函数。防抖通常用于处理用户输入等需要在一段时间内稳定下来的操作。

```javascript
function debounce(func, wait) {
    let timeout;
    return function(...args) {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
            func.apply(this, args);
        }, wait);
    };
}

// 使用示例
window.addEventListener('resize', debounce(() => {
    console.log('窗口尺寸改变');
}, 300));
```

## 节流

节流的原理是将多次执行变为每隔一段时间执行一次，即在指定时间间隔内只会执行一次函数。节流通常用于控制滚动事件、窗口调整大小事件等频繁触发的操作。

```javascript
function throttle(func, wait) {
    let lastTime = 0;
    return function(...args) {
        const now = Date.now();
        if (now - lastTime >= wait) {
            lastTime = now;
            func.apply(this, args);
        }
    };
}

// 使用示例
window.addEventListener('scroll', throttle(() => {
    console.log('窗口滚动');
}, 200));
```

# 判断一个元素在可视区域内

## 条件

如果一个元素在视窗之内的话，那么它一定满足下面四个条件：

- top 大于等于 0
- left 大于等于 0
- bottom 小于等于视窗高度
- right 小于等于视窗宽度

## 步骤

1. **获取元素的位置信息**：使用`Element.getBoundingClientRect()`方法获取元素的边界框信息。
2. **获取窗口的可视区域信息**：通过`window.innerHeight`和`window.innerWidth`获取窗口的高度和宽度。
3. **判断元素是否在可视区域内**：比较元素的边界框信息和窗口的可视区域信息。

```javascript
function isElementInViewport(el) {
    const rect = el.getBoundingClientRect();
    return (
        rect.top >= 0 &&
        rect.left >= 0 &&
        rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
        rect.right <= (window.innerWidth || document.documentElement.clientWidth)
    );
}

// 使用示例
const element = document.getElementById('myElement');
if (isElementInViewport(element)) {
    console.log('元素在可视区域内');
} else {
    console.log('元素不在可视区域内');
}
```

# 大文件断点续传

## 文件分块

将大文件分成多个chunk，分块上传，记录总的chunk数量

## 处理断点续传

通过异步实现

在上传过程中，记录每个块的上传状态。如果上传中断，可以从未完成的块继续上传。

在过程中要记录已上传的chunk即uploadedChunks

# 下拉刷新，上拉加载

下拉刷新和上拉加载这两种交互方式通常出现在移动端中，本质是通过页面触底（计算页面属性），可以使用第三方库解决

# 单点登录

单点登录（Single Sign-On，SSO）是一种认证机制，允许用户使用一个账户在多个系统或应用中进行登录，而不需要为每个系统或应用分别进行登录。SSO 提高了用户体验和安全性，因为用户只需要记住一个密码，并且减少了多次登录的麻烦。

实现 SSO 的常见方法有多种，包括基于令牌的认证（如 JWT）、OAuth2、SAML 等。

# web常见攻击

