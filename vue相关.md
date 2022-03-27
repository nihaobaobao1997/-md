# Vue的优点、Vue的缺点
## 优点
渐进式、组件化、轻量级、单页面路由、数据与视图分开、响应式
## 缺点
不支持IE8以下，首页加载慢

# Vue 和 React 的异同点
## 相同
* 使用虚拟Dom
* 可以组件化
* 单向数据流
* 可以服务端渲染 ssr
## 不同
* react手动变化数据，vue自动
* react单向绑定，vue双向绑定

# Vue底层实现原理
vue.js是采用 数据劫持 结合 发布者-订阅者 模式 的方式，
通过Object.defineProperty()来劫持各个属性的setter和getter，
在数据变动时发布消息给订阅者，触发相应的监听回调。

# MVVM是什么？比MVC好在哪里？
1. M：model 模型
2. V：view 视图
3. VM：view-model 视图模型双向绑定
把 MVC中的 controller 演变成 view-model
主要优点：解决了数据频繁更新的问题、代码低耦合、提高了代码复用性

# Vue和JQuery的区别，为什么放弃JQuery
1. JQuery直接操作dom，vue不直接操作dom，只需要关注数据即可，因为数据与视图分开
2. 在需要频繁更新dom的场景中，vue使用虚拟dom可以大大提高更新dom的性能
3. vue有vuex、router等集成库，提高了开发效率

# 为什么data是一个函数并返回一个对象
可以避免多次调用时产生数据污染 (原理是闭包)

# 组件之间的传值方式（用过)
1. 父传子 props
2. 子传父 $emit+事件调用
3. 组件中可以使用 $parent和 $children 获取父组件和子组件的实例，进而获取数据
4. 使用$refs获取组件实例，进而获取数据
5. 使用Vuex进行状态管理

# 路由有哪些模式，有哪些区别
## hash模式：通过 #号 后面内容的更改，触发hashchange事件，实现路由切换
## history模式：通过pushState事件，实现路由切换，需要后端配合 

# v-if和v-show的区别
## v-if
通过控制dom元素的删除和生成来实现显隐，每一次显隐都会重新跑一遍生命周期，因为显隐决定了组件的生成和销毁
## v-show
通过控制dom元素的css样式来实现显隐，不会销毁
## 使用场景
频繁大量使用时 v-show；否则使用 v-if

# computed 和 watch有何区别
conputed 是根据已有的变量来计算一个目标变量，大多数去情况都是多个变量算一个，依赖值不变的情况下，可以直接读取缓存，不能进行异步操作
computed 不支持异步
watch 是监听某一个变量的变化，并执行相应的回调函数，通常是一个变量的变化决定多个变量的变化，watch可以进行异步操作
watch 支持异步
简单来说：一般情况下，computed是多对一，watch是一对多

# watch可以监听computed吗？
可以，computed也是响应式的

# watch的immediate和deep是干什么用的？
* 不等监听属性变化，立即执行一次 hander 函数
* deep 为 true，表示深度监听，这时候就能监测到 userInfo 里的 name 值变化。

# 为什么 v-if 和 v-for 不建议用在同一标签？
 v-for的优先级高于v-if，会导致无效渲染（先渲染后销毁）
 可以使用computed代替v-if 先对需要历遍的数组进行计算
 
# key 的作用
* key的作用是为了在diff算法执行时更快的找到对应的节点，提高diff速度，更高效的更新虚拟DOM
* 为了在数据变化时强制更新组件，以避免“就地复用”带来的副作用。 (v-for)

# 不需要响应式的数据如何处理
1. 定义在 data 的return 对象外
2. 定义为 Object.freeze a: Object.freeze('b')

# watch监听引用数据类型时有什么属性（简单点就是对象）
* handler方法里执行回调
* deep 是否进行深度监听
* immediate 是否初始执行handler函数

# 对象新增属性无法更新视图，删除属性无法更新视图，为什么？怎么办？
原因：Object.defineProperty 没有对对象的新属性进行属性挟持
对象新属性无法更新视图：使用Vue.$set(obj,key,value)或this.$set(obj,key,value)
删除属性无法更新视图：使用Vue.$delete(obj,key)或this.$delete(obj,key)

# 直接arr[index] = xxx无法更新视图怎么办？为什么？怎么办？
原因：vue.derfineProperty 没有对数组进行挟持，使用直接arr[index]无法更新视图
解决：使用数组的splice方法，arr.splice(index,1,item)
     使用Vue.$set(arr,index,value)


# nextTick的用处？
获取最新的视图数据
之所以用 nextTick 是因为 Vue 是异步更新，所以数据更新，视图还没有更新
nextTick方法会在队列中加入一个回调函数，确保该函数在前面的dom操作完成后才调用

# vue 的SSR是什么？有什么好处？
ssr就是服务端渲染
基于 node.js serve服务环境开发，所有html
数据返回给前端，如何前端进行激活，即可成为浏览器识别的html代码
ssr首次加载更快，有更好的seo优化

# 子组件 mounted时调用父组件的方法
//父组件
<rl-child @hook:mounted="childMountedHandle"/>
//子组件
$emit

# 用computed返回值和用method返回值有什么区别？
计算参数变化时 computed有缓存不需要重新计算，methods需要

# 你理解 v-model 了吗？
## v-model 的本质是语法糖
大部分时间v-model="foo"等价于:value="foo" 加上 @input="foo=$event"
v-model封装了部分方法从而让用户忽视 html 在 api 的差异性
例如：textarea元素、select下拉框、input type="radio"单选框、input type="checkbox"多选框
## 对于未定义在响应式对象中的属性，会自动创建
## v-model 是双向绑定还是单向数据流？
二者都是
单向数据流：子组件不能改变父组件传递给它的 prop 属性，推荐的做法是它抛出事件，通知父组件自行改变绑定的值。
:value="foo" 传给子组件的props ；@input="foo=$event" 子组件抛出的事件；二者结合等于 v-model
## 如何让你开发的组件支持 v-model （子组件利用$emit使父组件更改props的值）
改写子组件中的 model
  model: { // 自定义v-model的格式
    prop: 'ame', // 代表 v-model 绑定的prop名
    event: 'zard' // 代码 v-model 通知父组件更新属性的事件名
  },
详看 [](https://juejin.cn/post/7049135444310622245)

# 说一下你平时用过的 Vue 修饰符
## .sync
父子组件交互，父组件传递给子组件 prop 值，子组件抛出事件，通知父组件改变这个绑定的值，可以用 .sync 修饰符简写。
1. 子组件里:this.$emit('update:xx', newValue)
2. 父组件里:<children :xx.sync="fatherValue" ></children> //@update:value="val => fatherValue = val"

## .native
.native 修饰符是加在自定义组件的事件上，保证自定义组件的原生事件能执行
## .stop
.stop 修饰符，用于阻止冒泡，同 event.stopPropagation()
用于父标签与子标签都同一个 @xx时，阻止子标签执行完@xx后父标签继续执行

## .self
.self 修饰符，只当在 event.target 是当前元素自身时触发处理函数(不冒泡，点击什么标签触发什么标签上的方法)

## .once
.once 修饰符，点击事件仅触发一次

## .prevent
.prevent 阻止默认事件，同event.preventDefault()
例如：阻止a标签的跳转行为
<a href="#" @click.prevent="handleClick">点击跳转</a>
阻止复选框被勾选
<input type="checkbox" @click.prevent />

## 键盘按键修饰符
太多了，需要再查吧55

## .trim
.trim 自动过滤用户输入的首尾空白字符 （空格）

## .number
.number 修饰符，会将用户的输入值转为数值类型

## .lazy
v-model 在每次input事件触发后将输入框的值与数据进行同步。添加.lazy修饰符，会在change事件之后进行同步

# 谈谈你对vue什么周期的理解
简单来说就是Vue实例从创建到销毁的过程
记几个常用的
 beforeCreate-》create-》beforeMounted-》mounted(创建完成)-》(开始运行)-》(结束销毁)

# created阶段可以操作及访问DOM吗？
不可以，但可以操作 data；到mounted阶段才可以

# Vue开发中，在哪个生命周期内调用异步请求
* created、beforeMounted、mounted
* 建议在 created 阶段进行异步请求，因为可以更快获取到服务端数据，减少页面 loading 时间。

# Vue的父组件和子组件生命周期钩子函数执行顺序是怎样的?
父 beforeCreated-》父created-》父beforeMounted-》
子 beforeCreated-》子created-》子beforeMounted-》子mounted
父 mounted

# 父组件可以监听到子组件的生命周期吗？
可以，可以使用这两种方法
* 子组件emit事件  
* 父组件@hook:mounted

# vue指令的本质是什么？
vue的本质就是语法糖，或者说标志位

# 如何实现vue自定义指令？
Vue允许注册自定义组件，有全局和局部注册两种方式
1. 全局：main.js 文件中 Vue.directives
2. 局部：新增 directives 

# 说一下你对vue插槽的理解（slot）
一个再复杂的Vue组件，都是三部分组成的：prop、event、slot
插槽通俗的理解就是'占坑'，在组件模板中占好了位置，当使用该组件标签的时候，组件标签里的内容就会自动填坑（替换模板中slot的位置）
写法 v-slot

# 父组件能否通过插槽的形式使用子组件的数据？
* 直接使用不能，使用作用域插槽能 *
* 作用域插槽：子组件在slot标签上绑定数据，父组件通过v-slot：xx="data" 获取数据

# $slots 和 $scopedSlots是干嘛用的？
* $slots 用来访问被插槽分发的内容
* $scopedSlots 用来访问作用域插槽

## render 函数
个人理解：在没有<template> 的情况下，生成 DOM 节点并渲染 
简单说明：[](https://juejin.cn/post/6844903823194980360)

## vue性能优化
