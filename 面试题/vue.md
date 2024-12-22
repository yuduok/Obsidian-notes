# vue 是什么

vue是一个用于创建用户界面的开源js框架，旨在更好地组织与简化web开发。同时vue能更方便地获取数据更新，并通过组件内部特定的方法实现视图与模型的交互。

# vue 核心特性

## 数据驱动 MVVM

- model 模型层，负责处理业务逻辑以及和服务器端进行交互
- view：视图层，负责将数据模型转化为UI展示出来
- viewmodel：视图模型层，用来连接model和view层，是二者的通信桥梁
  
## 组件化

定义：把图形、非图形的各种逻辑抽象为一个统一的概念即组件

组件化的优势：
- 降低系统耦合度，在接口不变的情况下，替换不同组件即可快速完成需求
- 方便调试，因为系统是由各个组件组成，每个组件负责单一的功能，可以快速定位系统故障，系统逻辑清晰
- 提高可维护性，组件复用以及指责单一，对组件代码优化即可进行系统升级
  
## 指令系统

vue的特殊指令：

- `v-if` 条件渲染
- `v-for` 列表渲染
- `v-bind` 属性绑定
- `v-on` 时间绑定
- `v-model` 双向数据绑定

# vue 跟传统开发（jquery）的区别

- vue 所有的界面时间，都是去操作数据，而jq操作dom
- vue 所有界面的变动，都是根据数据自动绑定的，而jq操作dom
  
# vue 和 react 比较

## 相同点

- 都有组件化思想
- 都有SSR
- 都有虚拟DOM
- 都是数据驱动视图
- 都有支持的native方案，vue 的 weex react 的 react 的 react native
- 都有自己的构建工具，vue 的 vue-cli，react 的 create react app

## 不同点

- 数据流向不同，react推崇单项数据流，vue是双向数据流
- 数据变化的实现原理不同，react使用的是不可变数据，vue使用的是可变的数据
- 组件间通信不同，react使用回调函数进行通信，vue父子组件通过事件与回调函数通信
- diff算法不同，react主要使用diff队列保存需要更新哪些dom，得到patch树，再统一更新dom，vue使用双向指针，边对比，边更新dom

# SPA

定义：single-page application单页应用，是一种网络应用程序或网站的模型，通过动态重写当前页面来与用户交互，避免了页面之间切换打断用户体验。所有必要的代码都通过单个页面的加载而检索，或根据用户需要动态装载适当资源并添加到页面。

react vue都属于SPA

## SPA 与 MPA的区别

MPA多页面应用，每个页面哦都是一个主页面，我们访问另一个页面时，需要重新加载html、css、js文件

### 单页面与多页面应用的区别

|          |           SPA            |                   MPA                   |
| -------- | :----------------------: | :-------------------------------------: |
| 组成     | 一个主页面和多个页面片段 |               多个主页面                |
| 刷新方式 |         局部刷新         |                整页刷新                 |
| url模式  |         哈希模式         |                历史模式                 |
| seo      |   难实现，使用ssr改善    |                容易实现                 |
| 数据传递 |           容易           | 需要通过url、cookie、localstorage等传递 |
| 页面切换 |    速度快，用户体验好    |           切换慢，用户体验差            |
| 维护成本 |         相对容易         |                相对复杂                 |

### SPA 优缺点

优点
- 桌面应用的即时性、网站的可移植性和可访问性
- 用户体验谈好、快，内容改变不需要加载整个页面
- 良好的前后端分离，分工明确

缺点
- 不利于SEO
- 首次渲染速度相对较慢

## hash模式与history模式比较

### hash模式

工作原理：使用url # 后面的部分管理路由

优点：

- 兼容性好
- 简单易用，不需要配置服务端，前端直接处理hash变化
- 不刷新页面

缺点：

- url不美观，包含#
- seo不友好
- 无法利用浏览器的完整历史记录管理功能

### history模式

工作原理：使用html5 history api ，通过 pushstate，replacestate，popstate管理路由

优点：

- url美观
- seo友好
- 浏览器记录完整历史

缺点：

- 需要服务端配置url规则
- 兼容性差

### 适用场景

hash模式适用于seo要求不高的简单应用，尤其是旧浏览器

history模式适用于良好seo和用户体验复杂的应用，尤其是需要后端支持的项目

### 为SPA 做 SEO

- ssr：vue的nuxtjs，react的nextjs
- 使用meta标签
- 动态渲染：根据用户代理（user agent）动态返回不同内容，检测到搜索引擎爬虫时返回渲染的html静态页，对普通用户返回SPA

# v-show and v-if

## 共同点

```js
<Model v-show="isShow"/>
<Model v-show="isShow"/>
```

表达式都为 true 时，都会占据页面位置

表达式都为 false 时，都不会占据页面位置

## 不同点

- 控制手段： v-show 通过改变css的display属性实现，dom元素还在，而v-if隐藏时将dom元素删除，显现时添加
- 编译过程：v-if有局部编译/卸载的过程，切换过程中会销毁或重建事件监听和子组件，v-show只是css的简单切换
- 编译条件：v-if是真正的条件渲染，他会确保在切换过程中的事件监听器和子组件适当销毁与重建，渲染为假时，并不做操作，直到为真时才渲染
  - v-show切换时，并不会触发生命周期
  - 而v-if切换时，会触发生命周期钩子 
- 性能消耗：v-if有更高的切换消耗，v-show有更高的初始渲染消耗

## 原理分析概述

v-show总是会渲染，原理较为简单，通过虚拟dom利用vnode节点创建真实dom（后续了解一下v-patch），有transition就执行transition，没有则直接设置css display属性

v-if相对复杂，要通过条件判断，返回一个node节点，render函数通过表达式确认是否生成dom

## 使用场景

切换较为频繁时，使用v-show

而运行条件很少改变，则使用v-if

# vue在实例挂载的过程中发生了什么

## 挂载

- 在`beforeCreate`之前，数据初始化未完成，data、props这些属性无法访问
- 到了`created`，数据完成初始化，data、props可以访问，但并未挂载到`dom`上，无法访问`dom`元素
- 挂载方法调用了`vue.$mount`

## 初始化

- 初始化顺序：**props**、**methods**、**data**
- `data` 定义的时候选择 **函数** 形式或者 **对象** 形式（**对象**只能为函数形式）

## 渲染步骤

调用 `compileToFunctions`， 会将 `template` 解析成 `render`对`template` 的解析

- 将html文档解析成 `ast` 描述符
- 将 `ast` 描述符解析成字符串
- 生成`render`函数

`render`的主要作用是生成`vnode`

## 结论

- new Vue 的时候会调用`_init`
  - 定义 $set $get $delete $watch方法
  - 定义 $on $off $emit $off事件
  - 定义 _update $forceUpdate $destroy生命周期
- 调用`$mount`进行页面挂载
- 挂载主要调用 **mountComponent**
- 定义 **updateComponent** 更新函数
- 执行 **render** 生成虚拟 **dom**
- _**update** 将虚拟 **dom** 生成真实 **dom**结构，并渲染

# 生命周期

## 生命周期是什么

在 **vue** 中，创建到销毁的过程就是生命周期，即指从创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、卸载等一系列过程。在 **Vue** 生命周期钩子会自动绑定 **this** 上下文到实例中，因此可以访问数据，对 property 和方法进行运算这意味着你不能使用箭头函数来定义一个生命周期方法 

## vue有哪些生命周期

| 生命周期 | 描述 |
| --- | --- |
| beforeCreate | 组件示例被创建之初 |
| created | 组件完全被创建 |
| beforeMount | 组件挂载之前 |
| mounted | 组件挂载到实例之后 |
| beforeUpdate | 组件数据发生变化之前 |
| updated | 组件数据发生更新之后 |
| beforeDestroy | 组件实例销毁前 |
| destroyed | 组件实例销毁后 |
| activated | keep-alive缓存的组件激活时 |
| deactivated | keep-alive缓存的组件被停用 |
| errorCaptured | 捕获一个来自子孙组件的错误时调用 |

## 具体分析

beforeCreate -> created

- 初始化 **vue** 实例，进行数据观测

created

- 完成数据观测、属性、方法的运算，**watch**、**event**事件回调的配置
- 可调用 **methods** 中的方法，访问和修改 data 数据触发响应式渲染 **dom** ，可通过 **computed** **watch**完成数据计算
- 此时 `vm.$el`还没被创建

created -> beforeMount

- 判断是否存在 **el** 选项，不存在则停止编译
- 优先级 render > template > outerHTML
- **vm.el** 获取到的是挂载 `dom` 的

# 为什么v-if和v-for不建议一起用

## 作用

`v-if`指令用于条件性渲染一块内容

`v-for`基于一个数组来渲染一个列表，在使用时建议设置一个独一无二的`key`值

## 优先级

二者在`vue`模版编译的时候都会被转化为render函数，创建一个实例，会发现对每个`item`都会进行一次`if`判断，故`v-for`优先级比`v-if`高

## 注意事项

因为优先级的原因，同时作用在同一元素上会带来性能上的浪费

为避免这种情况，在外层嵌套`template`，这样页面渲染不会生成`dom`节点

```vue
<template v-if="isShow">
    <p v-for="item in items">
</template>
```

而如果条件循环出现在内部，先使用计算属性`computed`过滤不需要显示的项（避免嵌套使用）

# SPA首屏加载速度慢怎么办

## 什么是首屏加载

首屏时间（first contentful paint）指的是浏览器从响应用户输入网址到首屏内容渲染完成的时间，此时整个网页不一定要全部渲染完成，但需要展示当前视窗需要的内容。

### 计算首屏时间

根据`performance.timing`提供的数据

![image-20240626234618141](/Users/yudu/Library/CloudStorage/OneDrive-hdu207/note/images/performancetimeing.png)

可通过下面两种方法计算

```js
// 方案一：
document.addEventListener('DOMContentLoaded', (event) => {
    console.log('first contentful painting');
});
// 方案二：
performance.getEntriesByName("first-contentful-paint")[0].startTime

// performance.getEntriesByName("first-contentful-paint")[0]
// 会返回一个 PerformancePaintTiming的实例，结构如下：
{
  name: "first-contentful-paint",
  entryType: "paint",
  startTime: 507.80000002123415,
  duration: 0,
};
```

## 加载慢

- 网络延时
- 资源文件体积过大
- 资源重复加载
- 加载脚本时，渲染内容堵塞

## 解决方案

### 减小入口文件体积

路由懒加载，将不同路由下的代码分割成不同的代码块，路由被请求时再单独打包

配置`vue-router`时，采用动态加载路由

### 静态资源本地缓存

前端合理利用`localStorage`

后端采用`http`缓存，设置`Cache-Control`等响应头

### ui框架按需导入

日常开发可能使用如下导入方式

```js
import ElementUI from 'element-ui'
Vue.use(ElementUI)
```

但实际上使用的却只有几个组件，所以可以采用

```js
import { Button, Input, Pagination, Table, TableColumn, MessageBox } from 'element-ui';
Vue.use(Button)
Vue.use(Input)
Vue.use(Pagination)
```

### 组件重复打包

假设`A.js`文件是一个常用的库，现在有多个路由使用了`A.js`文件，这就造成了重复下载

解决方案：在`webpack`的`config`文件中，修改`CommonsChunkPlugin`的配置

```js
minChunks: 3
```

`minChunks`为3表示会把使用3次及以上的包抽离出来放进公共依赖文件，避免组件重复加载

### 图片资源压缩

对于所有的图片资源进行适当压缩

对于所有的`icon`使用在线字体图标或者雪碧图（将多个小图标合并到一张图）

### 使用SSR

服务端渲染SSR，组件或页面通过服务器生成html字符串再发送到浏览器

# 为什么data属性是一个函数而不是一个对象

为了 **数据隔离**，每个组件实例需要有独立的数据副本，以避免不同实例之间的数据相互影响。

同时考虑了 **组件复用性**，每次创建组件实例时都会调用这个函数，从而返回一个数据对象，确保每个实例都有自己的数据副本而不是共享同一个数据对象。

# 直接给对象添加属性为什么界面不刷新

## vue响应式实现原理

`vue2`通过`Object.defineProperty`来实现响应式系统，但无法检测到对象属性的添加或删除

## 使用`Vue.set`方法

**vue**不允许再已经创建的实例上动态添加新的响应式属性，但可以采用该方式：

```js
Vue.set(this.someObject,'newProperty','newValue')
```

# 组件和插件有什么区别

## 组件

### 定义

组件是vue应用的基本构建块，是可复用的vue实例，包括模版、逻辑和样式

### 作用

用于构建用户界面的不同部分，每个组件通常对应应用的某个部分（按钮、表单等），目标是`App.vue`

### 使用方式

可使用`Vue.component`全局注册，也可使用`new Vue`局部注册

### 生命周期

每个组件都有自己的生命周期钩子函数

##### 数据流

组件之间通过`props`和`events`进行父子组件间通信

## 插件

### 定义

是扩展Vue功能的机制，通常用于向Vue添加全局功能

### 作用

扩展Vue功能，提供全局服务或功能，目标是`Vue`本身

### 使用方式

通过`Vue.use()`方式安装，插件通常还会暴露一个`install`方法，vue在安装插件时会调用这个方法

### 生命周期

插件本身没有生命周期钩子，可以通过Vue的生命周期钩子函数实现特定功能

### 数据流

插件通常不会直接参与组件间的数据流，而是提供辅助功能或全局状态管理

# vue组件间通信方式有哪些

## props

父组件通过`props`向子组件传递数据

```vue
// 父组件
<template>
  <child-component :message="parentMessage"></child-component>
</template>

<script>
import ChildComponent from './ChildComponent.vue';

export default {
  components: {
    ChildComponent
  },
  data() {
    return {
      parentMessage: 'Hello from parent'
    };
  }
}
</script>

// 子组件
<template>
  <div>{{ message }}</div>
</template>

<script>
export default {
  props: ['message']
}
</script>
```

## events

子组件通过`$emit`触发事件，父组件监听这些事件来进行数据传递

```vue
// 父组件
<template>
  <child-component @child-event="handleChildEvent"></child-component>
</template>

<script>
import ChildComponent from './ChildComponent.vue';

export default {
  components: {
    ChildComponent
  },
  methods: {
    handleChildEvent(data) {
      console.log('Received from child:', data);
    }
  }
}
</script>

// 子组件
<template>
  <button @click="sendToParent">Click me</button>
</template>

<script>
export default {
  methods: {
    sendToParent() {
      this.$emit('child-event', 'Hello from child');
    }
  }
}
</script>
```

## eventBus

- 使用场景：兄弟组件传值
- 创建一个中央事件总线`EventBus`
- 兄弟组件通过`$emit`触发自定义事件，`$emit`第二个参数为传递的数值
- 另一个兄弟组件通过`$on`监听自定义事件

```vue
// eventBus.js
import Vue from 'vue';
export const EventBus = new Vue();

// 组件A
<template>
  <button @click="sendToSibling">Send to sibling</button>
</template>

<script>
import { EventBus } from './eventBus';

export default {
  methods: {
    sendToSibling() {
      EventBus.$emit('event-from-a', 'Hello from A');
    }
  }
}
</script>

// 组件B
<template>
  <div>{{ message }}</div>
</template>

<script>
import { EventBus } from './eventBus';

export default {
  data() {
    return {
      message: ''
    };
  },
  mounted() {
    EventBus.$on('event-from-a', (data) => {
      this.message = data;
    });
  }
}
</script>
```

## provide/inject

用于祖先组件和后代组件之间的通信

```vue
// 祖先组件
<template>
  <child-component></child-component>
</template>

<script>
export default {
  provide() {
    return {
      message: 'Hello from ancestor'
    };
  }
}
</script>

// 后代组件
<template>
  <div>{{ message }}</div>
</template>

<script>
export default {
  inject: ['message']
}
</script>
```

## vuex

用于管理全局状态，vuex相当于一个用来存储共享变量的容器

- `state`用来存放共享变量的地方
- `getter`，可以增加一个`getter`派生状态，(相当于`store`中的计算属性），用来获得共享变量的值
- `mutations`用来存放修改`state`的方法。
- `actions`也是用来存放修改state的方法，不过`action`是在`mutations`的基础上进行。常用来做一些异步操作

## ref

父组件通过在子组件定义`ref`直接访问子组件实例

```vue
<Children ref='foo'/>
...
this.$refs.foo //获取子组件实例，拿到相对应的数据
```

## parent/children

子组件可以通过 `$parent` 访问父组件实例，父组件可以通过 `$children` 访问子组件实例。

```vue
// 子组件
<template>
  <div>Child Component</div>
</template>

<script>
export default {
  mounted() {
    this.$parent.parentMethod();
  }
}
</script>

// 父组件
<template>
  <child-component></child-component>
</template>

<script>
import ChildComponent from './ChildComponent.vue';

export default {
  components: {
    ChildComponent
  },
  methods: {
    parentMethod() {
      console.log('Parent method called');
    }
  }
}
</script>
```

# 双向绑定

## 什么是双向绑定

`Model`与`View`绑定在一起，Model更新时View变化，View变化时Model也自动更新

## 基本原理

双向绑定的核心是 Vue.js 的响应式系统。Vue.js 通过数据劫持（data hijacking）和发布-订阅模式（publish-subscribe pattern）来实现数据的双向绑定。以下是其工作原理的详细解释：

1. **数据劫持（Data Hijacking）**：
   - Vue.js 使用 `Object.defineProperty` 方法将数据对象的属性转换为 getter 和 setter。
   - 当数据发生变化时，setter 会被触发，从而通知依赖该数据的视图进行更新。
2. **发布-订阅模式（Publish-Subscribe Pattern）**：
   - Vue.js 维护一个依赖收集器（Dep），用于追踪哪些组件依赖哪些数据。
   - 当数据变化时，依赖收集器会通知所有依赖该数据的订阅者（组件）进行更新。

## v-model 的工作机制

`v-model` 是双向绑定的核心指令，通常用于表单控件（如输入框、复选框、单选按钮、选择框等）。`v-model` 实际上是语法糖，它等同于以下两个操作：

1. 绑定控件的 `value` 属性。
2. 监听控件的 `input` 事件，并更新数据模型。

以下是 `v-model` 的等效代码：

```html
<!-- 使用 v-model -->
<input v-model="message">

<!-- 等效代码 -->
<input :value="message" @input="message = $event.target.value">
```

# 对nexttick的理解

## 定义

官方的定义：在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM

即可以理解为，`Vue` 在更新 `DOM` 时是异步执行的。当数据发生变化，`Vue`将开启一个异步更新队列，视图需要等队列中**所有数据变化完成之后**，再统一进行更新。

## 使用场景

有时候我们需要在数据更新后立即执行某些操作，比如操作更新后的 DOM 元素。这时候 `nextTick` 就派上用场了。

1. **在数据更新后操作 DOM**：有时你需要在数据更新后立即操作 DOM 元素，例如获取元素的尺寸或滚动位置。
2. **确保在 Vue 更新完成后执行代码**：有时你需要确保某些代码在 Vue 完成其更新周期后执行。

# 对mixin的理解

## mixin是什么

在 Vue.js 中，`mixin` 是一种非常有用的代码复用机制。它允许你将可复用的功能分离出来，然后在多个组件中共享这些功能。`mixin` 本质上是一个对象，可以包含组件的各种选项，如数据、生命周期钩子、方法等。当一个组件使用 `mixin` 时，`mixin` 中的内容会被“混合”到该组件中。

## 使用场景

1. **代码复用**：当多个组件中有相同的逻辑时，可以将这些逻辑提取到 `mixin` 中，从而避免代码重复。
2. **分离关注点**：将复杂的逻辑分离到 `mixin` 中，使组件代码更清晰、更易维护。
3. **扩展功能**：通过 `mixin` 扩展组件的功能，而不修改组件本身的代码。

# 对slot的理解

## slot是什么

`slot` 是一种非常强大且灵活的机制，用于在组件中分发内容。它允许你在父组件中定义内容，然后将这些内容插入到子组件的特定位置。这种机制使得组件更加灵活和可复用，因为它们可以接受不同的内容，而不仅仅是固定的模板。

## 使用

### 默认插槽

子组件用`<slot>`标签来确定渲染的位置，标签里面可以放`DOM`结构，当父组件使用的时候没有往插槽传入内容，标签内`DOM`结构就会显示在页面

父组件在使用的时候，直接在子组件的标签内写入内容即可

子组件`Child.vue`

```html
<template>
    <slot>
      <p>插槽后备的内容</p>
    </slot>
</template>
```

父组件

```html
<Child>
  <div>默认插槽</div>  
</Child>
```

### 具名插槽

子组件用`name`属性来表示插槽的名字，不传为默认插槽

父组件中在使用时在默认插槽的基础上加上`slot`属性，值为子组件插槽`name`属性值

子组件`Child.vue`

```html
<template>
    <slot>插槽后备的内容</slot>
  <slot name="content">插槽后备的内容</slot>
</template>
```

父组件

```html
<child>
    <template v-slot:default>具名插槽</template>
    <!-- 具名插槽⽤插槽名做参数 -->
    <template v-slot:content>内容...</template>
</child>
```

### 作用域插槽

作用域插槽（scoped slots）允许子组件向插槽传递数据，父组件可以使用这些数据。

##### 子组件定义

```vue
<template>
  <div>
    <slot :user="user"></slot> <!--第一个user为属性名，第二个user为数据-->
  </div>
</template>

<script>
export default {
  name: 'MyComponent',
  data() {
    return {
      user: {
        name: 'John Doe',
        age: 30
      }
    };
  }
};
</script>
```

##### 父组件使用

```vue
<template>
  <MyComponent v-slot:default="slotProps">
    <p>User Name: {{ slotProps.user.name }}</p>
    <p>User Age: {{ slotProps.user.age }}</p>
  </MyComponent>
</template>

<script>
import MyComponent from './MyComponent.vue';

export default {
  components: {
    MyComponent
  }
};
</script>
```

# 对key的理解

`key` 属性为每个节点提供唯一标识。当 Vue.js 更新虚拟 DOM 时，它会通过比较新旧虚拟 DOM 树来确定哪些部分需要更新、插入或删除。**`key` 属性帮助 Vue 快速找到对应的节点，从而避免不必要的重渲染。**

key是给每一个vnode的唯一id，也是diff的一种优化策略，可以根据key，更准确， 更快的找到对应的vnode节点

## 组件更新

在组件中使用 `key` 属性可以强制组件重新渲染。例如，当你希望在数据变化时强制组件重新创建，而不是复用现有组件实例时，可以使用 `key` 属性

```vue
<template>
  <my-component :key="componentKey" :some-prop="someProp"></my-component>
  <button @click="updateComponent">Update Component</button>
</template>

<script>
export default {
  data() {
    return {
      componentKey: 0,
      someProp: 'initial value'
    };
  },
  methods: {
    updateComponent() {
      this.componentKey += 1; // 改变 key 强制重新渲染组件
    }
  }
};
</script>
```

## 性能优化

使用 `key` 属性可以显著提高性能，因为它减少了 Vue 需要进行的 DOM 操作次数。没有 `key` 时，Vue 可能需要进行更多的比较和操作来确定哪些节点需要更新，而有了 `key` 后，Vue 可以直接通过 `key` 来找到对应的节点进行高效更新。

# 对keep-alive的理解

`keep-alive` 是 Vue.js 提供的一个内置组件，用于缓存动态组件，以避免不必要的重新渲染和重新创建组件实例。它通常用于需要在不同页面或组件之间切换时保持组件状态的场景。

## 基本用法

`keep-alive`可以设置以下`props`属性：

- `include` - 字符串或正则表达式。只有名称匹配的组件会被缓存
- `exclude` - 字符串或正则表达式。任何名称匹配的组件都不会被缓存
- `max` - 数字。最多可以缓存多少组件实例

关于`keep-alive`的基本用法：

```vue
<keep-alive>
  <component :is="view"></component>
</keep-alive>
```

使用`includes`和`exclude`：

```vue
<keep-alive include="a,b">
  <component :is="view"></component>
</keep-alive>

<!-- 正则表达式 (使用 `v-bind`) -->
<keep-alive :include="/a|b/">
  <component :is="view"></component>
</keep-alive>

<!-- 数组 (使用 `v-bind`) -->
<keep-alive :include="['a', 'b']">
  <component :is="view"></component>
</keep-alive>
```

## 生命周期钩子

使用 `keep-alive` 时，组件会新增两个生命周期钩子：

1. **`activated`**:
   当组件被激活时（从缓存中恢复显示）调用。
2. **`deactivated`**:
   当组件被停用时（被缓存而不是销毁）调用。

# vue常用的修饰符有哪些

## `v-on`修饰符

1. **`.stop`**:
   阻止事件冒泡。

   ```vue
   <button v-on:click.stop="doSomething">Click Me</button>
   ```

2. **`.prevent`**:
   阻止默认事件。

   ```vue
   <form v-on:submit.prevent="onSubmit">Submit</form>
   ```

3. **`.capture`**:
   使用事件捕获模式。

   ```vue
   <div v-on:click.capture="doSomething">Click Me</div>
   ```

4. **`.self`**:
   仅当事件是从元素本身触发时触发回调。

   ```vue
   <div v-on:click.self="doSomething">Click Me</div>
   ```

5. **`.once`**:
   事件只触发一次。

   ```vue
   <button v-on:click.once="doSomething">Click Me Once</button>
   ```

6. **`.passive`**:
   提高滚动性能。

   ```vue
   <div v-on:scroll.passive="onScroll">Scroll</div>
   ```

## `v-bind`修饰符

1. **`.sync`**:
   实现父子组件之间的双向绑定。

   ```vue
   <child-component v-bind:title.sync="parentTitle"></child-component>
   ```

2. **`.prop`**:
   将绑定的值作为 DOM 属性而不是特性。

   ```vue
   <div v-bind:innerHTML.prop="htmlContent"></div>
   ```

## `v-model`修饰符

1. **`.lazy`**:
   在 `change` 事件之后更新数据，而不是在 `input` 事件之后。

   ```vue
   <input v-model.lazy="message">
   ```

2. **`.number`**:
   将用户输入自动转换为数值类型。

   ```vue
   <input v-model.number="age">
   ```

3. **`.trim`**:
   自动过滤用户输入的首尾空白字符。

   ```vue
   <input v-model.trim="message">
   ```

## 按键修饰符

1. **`.enter`**:
   只在 `Enter` 键被按下时触发事件。

   ```vue
   <input v-on:keyup.enter="submitForm">
   ```

2. **`.tab`**:
   只在 `Tab` 键被按下时触发事件。

   ```vue
   <input v-on:keyup.tab="focusNext">
   ```

3. **`.delete`**:
   只在 `Delete` 键被按下时触发事件。

   ```vue
   <input v-on:keyup.delete="removeItem">
   ```

4. **`.esc`**:
   只在 `Escape` 键被按下时触发事件。

   ```vue
   <input v-on:keyup.esc="cancelEdit">
   ```

5. **`.space`**:
   只在 `Space` 键被按下时触发事件。

   ```vue
   <input v-on:keyup.space="togglePlay">
   ```

6. **`.up`、`.down`、`.left`、`.right`**:
   分别在方向键被按下时触发事件。

   ```vue
   <input v-on:keyup.up="moveUp">
   <input v-on:keyup.down="moveDown">
   <input v-on:keyup.left="moveLeft">
   <input v-on:keyup.right="moveRight">
   ```

## 系统修饰符

1. **`.ctrl`**:
   只在按下 `Ctrl` 键时触发事件。

   ```vue
   <input v-on:keyup.ctrl="saveDocument">
   ```

2. **`.alt`**:
   只在按下 `Alt` 键时触发事件。

   ```vue
   <input v-on:keyup.alt="openMenu">
   ```

3. **`.shift`**:
   只在按下 `Shift` 键时触发事件。

   ```vue
   <input v-on:keyup.shift="selectText">
   ```

4. **`.meta`**:
   只在按下 `Meta` 键（在 Mac 上是 `Command` 键，在 Windows 上是 `Windows` 键）时触发事件。

   ```vue
   <input v-on:keyup.meta="openApplication">
   ```

# 什么是虚拟DOM

## Vue.js 虚拟 DOM 的基本概念

1. **VNode**:
   Vue.js 中的虚拟 DOM 节点称为 VNode。每个 VNode 是一个 JavaScript 对象，包含了节点的标签、属性、子节点等信息。
2. **渲染函数**:
   Vue.js 使用渲染函数将模板转换为 VNode。渲染函数是一个返回 VNode 的函数，它可以是用户定义的，也可以是 Vue.js 编译模板生成的。

## Vue.js 虚拟 DOM 的工作流程

1. **模板编译**:
   在开发阶段，Vue.js 会将模板编译为渲染函数。这个过程**将模板字符串转换为 JavaScript 代码**，该代码在运行时生成 VNode 树。
2. **创建 VNode 树**:
   渲染函数在组件初始化时被调用，生成初始的 VNode 树。
3. **渲染真实 DOM**:
   Vue.js 会将 VNode 树转换为真实的 DOM 元素，并插入到页面中。
4. **响应式更新**:
   当组件的状态或数据发生变化时，Vue.js 的响应式系统会触发重新渲染。渲染函数会再次被调用，生成新的 VNode 树。
5. **Diff 算法**:
   Vue.js 使用 Diff 算法比较新旧 VNode 树，找出需要更新的部分。这个过程称为“patching”。
6. **更新真实 DOM**:
   根据 Diff 算法的结果，Vue.js 会生成最小的 DOM 操作集合，并应用到真实的 DOM 上。

## 核心代码

### VNode定义

VNode 是一个 JavaScript 对象，包含了节点的标签、属性、子节点等信息。以下是一个简单的 VNode 定义示例：

```javascript
class VNode {
  constructor(tag, data, children, text, elm) {
    this.tag = tag;         // 标签名
    this.data = data;       // 节点数据（属性、事件等）
    this.children = children; // 子节点数组
    this.text = text;       // 文本节点内容
    this.elm = elm;         // 对应的真实 DOM 元素
  }
}
```

ps：vue是通过`createElement`生成VNode

### 渲染函数

渲染函数是一个返回 VNode 的函数。以下是一个简单的渲染函数示例：

```javascript
function render() {
  return new VNode('div', { id: 'app' }, [
    new VNode('h1', null, [new VNode(undefined, undefined, undefined, 'Hello, Vue!')])
  ]);
}
```

## 虚拟DOM优势

1. **性能优化**:
   通过批量更新和最小化 DOM 操作，虚拟 DOM 提高了性能。直接操作真实 DOM 是昂贵的，而虚拟 DOM 通过减少不必要的 DOM 操作，提高了效率。
2. **跨平台**:
   虚拟 DOM 是一个平台无关的抽象层，可以用于浏览器、服务器端渲染（如 Node.js），甚至原生应用（如 Weex）。
3. **简化开发**:
   开发者可以专注于描述 UI 的最终状态，而不必手动处理 DOM 操作。框架会自动处理状态变化和 DOM 更新。

# vue中的diff算法

Vue.js 中的 Diff 算法用于比较新旧虚拟 DOM 树（VNode 树），找出需要更新的部分，并生成最小的 DOM 操作集合。这个过程被称为“patching”。Vue.js 的 Diff 算法基于 React 的 Diff 算法，但也有其独特的优化。

## diff算法基本原理

Vue.js 的 Diff 算法遵循以下基本原则：

1. **同层比较**:
   只比较同一层级的节点，不跨层级比较。这样可以大大减少比较的复杂度。
2. **键值优化**:
   使用 `key` 属性来标识节点，提高比较效率。具有相同 `key` 的节点被认为是相同的节点。
3. **最小化更新**:
   尽量复用现有节点，减少节点的创建和删除操作。

## 实现步骤

1. **比较根节点**:
   从根节点开始比较新旧 VNode 树。如果根节点不同，则直接替换整个节点。
2. **比较子节点**:
   如果根节点相同，则递归比较子节点。子节点的比较分为以下几种情况：
   - 新旧节点都是文本节点：直接更新文本内容。
   - 新旧节点都是元素节点：比较属性和子节点。
   - 一个是元素节点，一个是文本节点：替换节点。
   - 节点类型相同但 `key` 不同：替换节点。
3. **更新属性**:
   如果节点类型相同，则比较并更新节点的属性。
4. **处理子节点**:
   子节点的处理是 Diff 算法的核心，Vue.js 使用了一些优化策略来提高性能，包括：
   - **双端比较**：同时从两端开始比较新旧子节点，尽早发现相同的节点。
   - **使用 `key` 属性**：通过 `key` 属性快速定位相同的节点。
   - **最长递增子序列**：找出新节点序列中的最长递增子序列，尽量复用现有节点，减少不必要的DOM操作。

# 封装axios

`axios` 是一个轻量的 `HTTP`客户端，基于 `XMLHttpRequest` 服务来执行 `HTTP` 请求，支持丰富的配置，支持 `Promise`，支持浏览器端和 `Node.js` 端。

## 基本使用

发送请求

```js
axios({        
  url:'xxx',    // 设置请求的地址
  method:"GET", // 设置请求方法
  params:{      // get请求使用params进行参数凭借,如果是post请求用data
    type: '',
    page: 1
  }
}).then(res => {  
  // res为后端返回的数据
  console.log(res);   
})
```

## 为什么要封装

`axios` 的 API 很友好，但随着项目规模变大，每发起一次`HTTP`请求，就要重写一遍请求头、超时时间等。

## 封装请求方法

先引入封装好的方法，在要调用的接口重新封装成一个方法暴露出去

```js
// get 请求
export function httpGet({
  url,
  params = {}
}) {
  return new Promise((resolve, reject) => {
    axios.get(url, {
      params
    }).then((res) => {
      resolve(res.data)
    }).catch(err => {
      reject(err)
    })
  })
}

// post
// post请求
export function httpPost({
  url,
  data = {},
  params = {}
}) {
  return new Promise((resolve, reject) => {
    axios({
      url,
      method: 'post',
      transformRequest: [function (data) {
        let ret = ''
        for (let it in data) {
          ret += encodeURIComponent(it) + '=' + encodeURIComponent(data[it]) + '&'
        }
        return ret
      }],
      // 发送的数据
      data,
      // url参数
      params

    }).then(res => {
      resolve(res.data)
    })
  })
}
```

把封装的方法放在一个`api.js`文件中

```js
import { httpGet, httpPost } from './http'
export const getorglist = (params = {}) => httpGet({ url: 'apps/api/org/list', params })
```

页面中就能直接调用

```js
// .vue
import { getorglist } from '@/assets/js/api'

getorglist({ id: 200 }).then(res => {
  console.log(res)
})
```

这样可以把`api`统一管理起来，以后维护修改只需要在`api.js`文件操作即可

# axios原理

Axios 的核心原理包括以下几个方面：

## 请求配置

Axios 允许用户配置请求的各种参数，例如 URL、方法、头信息、超时时间等。

```javascript
const config = {
  url: '/user',
  method: 'get', // 默认是 get
  baseURL: 'https://api.example.com',
  headers: { 'X-Requested-With': 'XMLHttpRequest' },
  params: { ID: 12345 },
  timeout: 1000,
  responseType: 'json', // 默认是 json
};
```

## 拦截器

Axios 提供了请求拦截器和响应拦截器，允许用户在请求或响应被处理之前进行修改。

```javascript
// 添加请求拦截器
axios.interceptors.request.use(
  config => {
    // 在发送请求之前做些什么
    return config;
  },
  error => {
    // 对请求错误做些什么
    return Promise.reject(error);
  }
);

// 添加响应拦截器
axios.interceptors.response.use(
  response => {
    // 对响应数据做些什么
    return response;
  },
  error => {
    // 对响应错误做些什么
    return Promise.reject(error);
  }
);
```

## 请求发送

Axios 使用原生的 `XMLHttpRequest`（在浏览器中）或 `http` 模块（在 Node.js 中）发送 HTTP 请求。

```javascript
function sendRequest(config) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open(config.method, config.url, true);
    xhr.timeout = config.timeout;

    // 设置请求头
    for (const key in config.headers) {
      if (config.headers.hasOwnProperty(key)) {
        xhr.setRequestHeader(key, config.headers[key]);
      }
    }

    // 处理响应
    xhr.onreadystatechange = () => {
      if (xhr.readyState === 4) {
        if (xhr.status >= 200 && xhr.status < 300) {
          resolve(xhr.responseText);
        } else {
          reject(new Error(`Request failed with status code ${xhr.status}`));
        }
      }
    };

    // 处理请求错误
    xhr.onerror = () => {
      reject(new Error('Network Error'));
    };

    // 发送请求
    xhr.send(config.data);
  });
}
```

## Promise

Axios 使用 Promise 来处理异步操作，使得请求和响应处理更加简洁和直观。

```js
axios.get('/user') 
    .then(response =>{
    console.log(response.data);
  })  
    .catch(error => {
    console.error(error);
  });
```

## 响应处理

Axios 处理 HTTP 响应，并根据响应状态码进行相应的处理。

```javascript
axios.get('/user')
  .then(response => {
    // 处理成功的响应
    console.log(response.data);
  })
  .catch(error => {
    // 处理错误的响应
    console.error(error);
  });
```

# SSR解决了什么问题

## 定义

`Server-Side Rendering` 我们称其为`SSR`，意为服务端渲染。指由服务侧完成页面的 `HTML` 结构拼接的页面处理技术，发送到浏览器，然后为其绑定状态与事件，成为完全可交互页面的过程。

## 初始加载速度

在客户端渲染中，浏览器首先需要加载 HTML 框架，然后下载和执行 JavaScript 代码，最后生成和展示内容。这会导致初始加载时间较长，特别是在互联网连接较慢或设备性能较差的情况下。

SSR 通过在服务器上预先生成完整的 HTML 内容，浏览器可以直接展示这些内容，从而显著减少初始加载时间，提高用户体验。对于低性能设备，可以减轻其在客户端的负担。

## 搜索引擎优化（SEO）

搜索引擎爬虫在抓取和索引网页内容时，通常更擅长处理静态 HTML 内容。对于客户端渲染的页面，爬虫可能无法正确执行 JavaScript 代码，从而无法抓取到动态生成的内容。这会影响页面的搜索引擎排名。

SSR 提供了预渲染的 HTML 内容，使得搜索引擎爬虫能够轻松抓取和索引页面内容，从而改善 SEO。

## 更好的代码分离

SSR 允许开发者更好地分离服务器端逻辑和客户端逻辑。这可以使代码更清晰、更易于维护，同时也可以更好地利用服务器资源。

## 实现方式

### 设置服务器

首先，需要设置一个服务器来处理 HTTP 请求。常见的服务器框架包括 Node.js 的 Express、Koa 等。服务器的主要任务是接收客户端请求、生成 HTML 内容并返回给客户端。

```javascript
const express = require('express');
const app = express();

app.get('*', (req, res) => {
  // 处理所有的 GET 请求
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

### 引入视图引擎或框架

**Vue.js**：使用 `vue-server-renderer` 来生成 HTML。

```javascript
const Vue = require('vue');
const renderer = require('vue-server-renderer').createRenderer();

app.get('*', (req, res) => {
  const app = new Vue({
    template: `<div>Hello SSR</div>`
  });

  renderer.renderToString(app, (err, html) => {
    if (err) {
      res.status(500).end('Internal Server Error');
      return;
    }
    res.send(`
      <!DOCTYPE html>
      <html>
        <head>
          <title>My SSR App</title>
        </head>
        <body>
          ${html}
          <script src="/bundle.js"></script>
        </body>
      </html>
    `);
  });
});
```

### 数据预取

在生成 HTML 内容之前，服务器可能需要预取数据。例如，从数据库或 API 获取数据，然后将数据传递给视图引擎或框架。

```javascript
app.get('*', async (req, res) => {
  const data = await fetchData(); // 预取数据
  const html = ReactDOMServer.renderToString(<App data={data} />);
  res.send(`
    <!DOCTYPE html>
    <html>
      <head>
        <title>My SSR App</title>
      </head>
      <body>
        <div id="root">${html}</div>
        <script>
          window.__INITIAL_DATA__ = ${JSON.stringify(data)}
        </script>
        <script src="/bundle.js"></script>
      </body>
    </html>
  `);
});
```

### 客户端重建

客户端需要重建（hydrate）服务器生成的 HTML 内容，以便使页面变得可交互。客户端 JavaScript 代码会附加到已有的 HTML 上，并使其变得动态。

vuejs示例

```javascript
import Vue from 'vue';
import App from './App.vue';

const app = new Vue({
  render: h => h(App, { props: { data: window.__INITIAL_DATA__ } })
});

app.$mount('#app');
```

# vue的项目结构

## 目录结构

```
my-vue-project/
├── node_modules/           # 项目依赖包
├── public/                 # 公共静态资源，不会被 Webpack 处理
│   ├── favicon.ico         # 网站图标
│   └── index.html          # HTML 模板
├── src/                    # 源代码
│   ├── assets/             # 静态资源（图片、字体等）
│   ├── components/         # Vue 组件
│   ├── views/              # 页面级组件（视图）
│   ├── router/             # 路由配置
│   ├── store/              # Vuex 状态管理
│   ├── App.vue             # 根组件
│   ├── main.js             # 入口文件
├── .env                    # 环境变量文件
├── .gitignore              # Git 忽略文件
├── babel.config.js         # Babel 配置
├── package.json            # 项目配置文件
├── README.md               # 项目说明文件
└── vue.config.js           # Vue CLI 配置文件
```

## 目录说明

#### `public/`

- `favicon.ico`：网站的图标。
- `index.html`：HTML 模板文件。Vue CLI 会在构建时将生成的 JavaScript 文件自动插入到这个文件中。

#### `src/`

- `assets/`：存放静态资源，如图片、字体等。这些资源会被 Webpack 处理。
- `components/`：存放 Vue 组件。组件是可复用的 UI 单元。
- `views/`：存放页面级组件（视图）。这些组件通常通过路由进行导航。
- `router/`：存放路由配置文件。通常包含 `index.js` 文件，用于定义应用的路由。
- `store/`：存放 Vuex 状态管理相关文件。通常包含 `index.js` 文件，用于定义应用的状态、变更和动作。
- `App.vue`：根组件，所有其他组件都是这个组件的子组件。
- `main.js`：应用的入口文件。用于初始化 Vue 实例、配置路由和状态管理等。

#### 根目录

- `.env`：环境变量文件。可以在这里定义不同环境（开发、生产等）的变量。
- `.gitignore`：Git 忽略文件。定义哪些文件和目录不应该被 Git 版本控制。
- `babel.config.js`：Babel 配置文件。用于配置 Babel 转码器。
- `package.json`：项目配置文件。包含项目的依赖、脚本、元数据等信息。
- `README.md`：项目说明文件。通常包含项目的介绍、安装和使用说明等。
- `vue.config.js`：Vue CLI 配置文件。用于覆盖默认的 Vue CLI 配置。

# vue的权限管理

在 Vue.js 应用中实现权限管理是确保应用安全性和用户体验的关键。权限管理通常涉及以下几个方面：

1. **用户认证**：确定用户的身份（例如通过登录）。
2. **角色管理**：为用户分配不同的角色。
3. **权限控制**：根据用户的角色来控制访问不同的路由和组件。

## 用户认证

一般采用`jwt`来验证，登录完拿到`token`，将`token`存起来（store中），通过`axios`请求拦截器进行拦截，每次请求的时候头部携带`token`

`src/store/index.js`

```javascript
import Vue from 'vue';
import Vuex from 'vuex';
import axios from 'axios';

Vue.use(Vuex);

export default new Vuex.Store({
  state: {
    user: null,
    token: null
  },
  mutations: {
    setUser(state, user) {
      state.user = user;
    },
    setToken(state, token) {
      state.token = token;
    },
    logout(state) {
      state.user = null;
      state.token = null;
    }
  },
  actions: {
    async login({ commit }, credentials) {
      const response = await axios.post('/api/login', credentials);
      const { user, token } = response.data;
      commit('setUser', user);
      commit('setToken', token);
      axios.defaults.headers.common['Authorization'] = `Bearer ${token}`;
    },
    logout({ commit }) {
      commit('logout');
      delete axios.defaults.headers.common['Authorization'];
    }
  },
  getters: {
    isAuthenticated: state => !!state.token,
    userRole: state => state.user ? state.user.role : null
  }
});
```

## 角色管理和权限控制

在 Vue Router 中，可以使用导航守卫来实现权限控制，以下示例根据用户的角色控制路由访问：

`src/router/index.js`

```javascript
import Vue from 'vue';
import VueRouter from 'vue-router';
import store from '../store';
import Home from '../views/Home.vue';
import Admin from '../views/Admin.vue';
import Login from '../views/Login.vue';

Vue.use(VueRouter);

const routes = [
  { path: '/', name: 'Home', component: Home },
  { path: '/login', name: 'Login', component: Login },
  { 
    path: '/admin', 
    name: 'Admin', 
    component: Admin, 
    meta: { requiresAuth: true, role: 'admin' } 
  }
];

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
});

router.beforeEach((to, from, next) => {
  const requiresAuth = to.matched.some(record => record.meta.requiresAuth);
  const userRole = store.getters.userRole;

  if (requiresAuth && !store.getters.isAuthenticated) {
    next('/login');
  } else if (requiresAuth && to.meta.role && to.meta.role !== userRole) {
    next('/');
  } else {
    next();
  }
});

export default router;
```

## 组件使用权限控制

在组件中，可以使用 Vuex 的状态和 getters 来控制组件的显示和行为。

```vue
<template>
  <div v-if="isAuthorized">
    <p>Protected Content</p>
  </div>
  <div v-else>
    <p>You do not have permission to view this content.</p>
  </div>
</template>

<script>
export default {
  computed: {
    isAuthorized() {
      return this.$store.getters.isAuthenticated && this.$store.getters.userRole === 'admin';
    }
  }
};
</script>

```

# vue中解决跨域

## 什么是跨域

跨域本质是浏览器基于**同源策略**的一种安全手段

同源策略（Sameoriginpolicy），是一种约定，它是浏览器最核心也最基本的安全功能

所谓同源（即指在同一个域）具有以下三个相同点

- 协议相同（protocol）
- 主机相同（host）
- 端口相同（port）

反之非同源请求，也就是协议、端口、主机其中一项不相同的时候，这时候就会产生跨域。

## 解决方法

### proxy

#### 方案一

在 Vue 项目中，可以通过配置开发服务器的代理来解决跨域问题。Vue CLI 提供了一个方便的方式来配置代理。

在 `vue.config.js` 文件中添加如下配置：

```javascript
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://example.com', // 目标服务器
        changeOrigin: true, // 是否改变源
        pathRewrite: {
          '^/api': '' // 重写路径
        }
      }
    }
  }
};
```

在这种配置下，所有以 `/api` 开头的请求都会被代理到 `http://example.com`，并且路径中的 `/api` 部分会被去掉。

#### 方案二

使用服务器中转

你可以在你的服务器上设置一个中转接口，服务器从目标服务器获取数据，然后将数据返回给前端。这样前端只需请求自己的服务器，不会触发跨域问题。

例如，在 Express.js 中：

```javascript
const express = require('express');
const axios = require('axios');

const app = express();

app.get('/api/proxy', async (req, res) => {
  try {
    const response = await axios.get('http://example.com/api/data');
    res.json(response.data);
  } catch (error) {
    res.status(500).send('Error occurred');
  }
});

app.listen(3000, () => {
  console.log('Proxy server listening on port 3000');
});
```

前端请求：

```javascript
axios.get('/api/proxy').then(response => {
  console.log(response.data);
});
```

### cors

跨域资源共享（CORS）是一种允许浏览器向跨源服务器发出请求的机制。你可以在后端服务器上设置 CORS 头来允许跨域请求。

例如，在一个 Express.js 应用中，可以使用 `cors` 中间件：

```javascript
const express = require('express');
const cors = require('cors');

const app = express();

app.use(cors());

app.get('/api/data', (req, res) => {
  res.json({ message: 'This is CORS-enabled for all origins!' });
});

app.listen(3000, () => {
  console.log('CORS-enabled web server listening on port 3000');
});
```

### jsonp

JSONP（JSON with Padding）是一种绕过跨域限制的方法，但只能用于 **GET** 请求。它通过动态插入一个 `<script>` 标签来实现跨域数据传输。

在 Vue 中可以使用 JSONP：

```javascript
import jsonp from 'jsonp';

jsonp('http://example.com/api/data', null, (err, data) => {
  if (err) {
    console.error(err.message);
  } else {
    console.log(data);
  }
});
```

# vue3和vue2的区别

## 性能提升

- **编译器优化**：Vue 3 的编译器进行了重写，优化了静态内容的提升和模板编译，使得生成的渲染函数更加高效。
- **更小的打包体积**：Vue 3 的核心库更小，打包体积减少了约50%，这得益于 Tree-shaking 和模块化设计。

## composition api

Vue 3 引入了 Composition API，这是一个用于组织组件逻辑的新方法。它使得代码更加灵活和可重用，特别是在大型应用中。

### setup函数

`setup` 函数是 Composition API 的核心。它是一个新的组件选项，在组件实例创建之前调用，用于初始化组件的状态和定义其行为。

### 响应式变量和对象

- **`ref`**：用于定义基本类型的响应式变量。`ref` 创建的变量需要通过 `.value` 访问和修改。
- **`reactive`**：用于定义对象类型的响应式数据。`reactive` 创建的对象可以直接访问和修改其属性。

### 组合函数

组合函数是使用 Composition API 的核心理念之一。它们是可以复用的函数，用于封装和组织逻辑。通过组合函数，可以将组件逻辑拆分成更小、更独立的部分，方便复用和测试。

```javascript
// useCounter.js
import { ref } from 'vue';

export function useCounter() {
  const count = ref(0);

  function increment() {
    count.value++;
  }

  return { count, increment };
}
```

在组件中使用组合函数：

```javascript
import { useCounter } from './useCounter';

export default {
  setup() {
    const { count, increment } = useCounter();

    return { count, increment };
  }
};
```

Composition API 提供了一种更灵活和模块化的方式来组织和复用组件逻辑。它特别适合复杂应用和大型项目，使得代码更易于维护和测试。通过 `setup` 函数、响应式变量和对象、生命周期钩子和组合函数，开发者可以更高效地管理组件的状态和行为。

相同功能的代码编写在一块，而不像`options API`那样，各个功能的代码混成一块

## 以proxy为基础的响应式

Vue 3 使用 ES6 的 Proxy 对象来实现响应式系统，取代了 Vue 2 中的 `Object.defineProperty`。Proxy 能够更好地处理数组和对象属性的添加和删除。

## 新的组件生命周期钩子

Vue 3 添加了一些新的生命周期钩子，例如 `onBeforeMount`、`onMounted`、`onBeforeUpdate`、`onUpdated`、`onBeforeUnmount` 和 `onUnmounted`，这些钩子可以在 Composition API 中使用。

## TS支持

Vue 3 从设计上更好地支持 TypeScript，提供了更好的类型推断和类型安全。

# vue3的设计目标

## 更小

vue3移除了一些不常用的api

引入`tree-shaking`，可以将无用模块“剪辑”，仅打包需要的，使打包的整体体积变小了

### tree-shaking基本步骤

1. **静态分析**：打包工具会解析所有的 ES6 模块，构建一个依赖图，确定哪些模块和函数被导入和使用。
2. **标记未使用代码**：通过依赖图，打包工具可以标记出哪些导入的模块和函数没有被使用。
3. **移除未使用代码**：在打包过程中，打包工具会移除这些未使用的代码，从而减小最终的打包文件大小。

## 更快

- diff算法优化
- 静态提升
- 事件监听缓存
- SSR优化

## 更友好

推出了`composition api`

# vue3性能提升

## diff算法

`vue3`在`diff`算法中相比`vue2`增加了静态标记，已经标记为静态节点的标签不会比较，提高性能

## 静态提升

vue3对不参与更新的元素做静态提升，只会被创建一次，在渲染时直接服用。

## 事件监听缓存

默认情况下绑定事件行为会被视为动态绑定，所以每次都会去追踪它的变化，但开启事件监听缓存后，没有了静态标记。也就是说下次`diff`算法的时候直接使用

## ssr优化

当静态内容大到一定量级时候，会用`createStaticVNode`方法在客户端去生成一个static node，这些静态`node`，会被直接`innerHtml`，就不需要创建对象，然后根据对象渲染

# vue3为什么要用proxy代替defineProperty

`Proxy`的监听是针对一个对象的，那么对这个对象的所有操作会进入监听操作，这就完全可以代理所有属性了
