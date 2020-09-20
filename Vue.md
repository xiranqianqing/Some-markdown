## Vue

### 介绍

vue的一切新特点都是为了使人在写代码时更加方便。

名词解释：

渐进式框架(Progressive):用到哪学到哪，不用全部学完才能用，自底向上增量开发。主张：特点，弱主张：不搞特殊化。只关注图层：不关注映射。声明式渲染：以结果为导向，不告诉计算机怎么做而是直接说做什么。响应式：根据不同终端变成不同布局。

它继承了[[MVVM]]模式。

### 基础知识

所有的Vue组件都是Vue实例，并且接受相同的选项对象。

响应式：vue实例中引入外部data，如果外部data改变了，vue实例中的data也会随之改变。

实例化：

```javascript
var vm = new Vue({
  // 选项
    el:'#[id]',//<div id="[id]"></div>使用，用于提供一个在
    //页面上已存在的 DOM 元素作为 Vue 实例的挂载目标
    //参数类型string|HTMLElement
    //vm是vue module的意思
})


```

vue内部的实例属性在外面使用时需要加上前缀$

Vue的作用范围是el选项命中的元素和它内部的后代元素

el是用来设置Vue实例挂载的元素。建议使用id选择器，也可以使用除了html和body以外的双标签。

#### 实例生命周期钩子

有很多个阶段

​	beforeCreate,created,beforeMount,mounted,beforeUpdate,updated,beforeDestroy,destroyed.



### 模板语法

#### 插值（vue的变量）

```
前提：标签内指的是<p  这里  ></p>
```

文本

标签内不需要添加v-txt，只需要有{{}}就行。

​	{{内容}}会随着绑定数据对象的变化而变化。v-once可以让内容不发生变化。

原始HTML

​	标签内添加v-html之后，{{html代码}}，浏览器会对html代码进行解析。

属性，Attribute

​	在标签内添加v-bind之后，可以       v-bind:属性名=".."       对标签的属性进行修改

表达式

​	{{}}内部可以添加表达式，{{5+5}}会显示10。

###### 	一些胡子语法：

​	{{*msg}}中msg是单向绑定的。

​	{{{msg}}}会产生纯文本而不是html文本

模板片段：Vue.partial{'',''}

#### 指令

​	v-if=""等，在MVVM里已经有了。

修饰符.

​	比如   submit.prevent表示上传的时候会调用event.preventDefault();

#### 缩写

​	v-bind:href=""可以缩写为:href=""

​	v-on可以缩写成@

### 计算属性

在viewModel里的computed:{}，存放用于计算的函数。

也可以换成methods:{},不会产生缓存。在使用method的变量，需要加上()。

message的值发生改变的时候会动态影响计算出的值。



```js
data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
```

只要message不发生改变，再次运行时，计算属性就会立即返回之前的结果。

### 侦听器

在vm里添加watch:{}，监听数据的变化并响应。

如果watch里面的值发生改变，里面的函数就会运行。

计算属性和侦听器，暂时无法理解这些。



响应分为五类：信息响应(`100`–`199`)，成功响应(`200`–`299`)，重定向(`300`–`399`)，客户端错误(`400`–`499`)和服务器错误 (`500`–`599`)。

### Class与Style绑定

##### HTML 内联Class属性

```
<div v-bind:class="{'active':isAct}">
```

使得（div的class属性为active）的结果为isActive。

如果isActive为true，效果等同于

```
<div class="active">
```

可以将这些css类的开关与计算属性相关，让计算属性函数决定是否要显示|隐藏css类。

### v-

###### 	**条件渲染**，v-if和v-show。

​	v-if在<template>元素上使用。

​	在上传字符串时，可以在input标签里添加key以清空输入框。

​	v-show可以直接展示



###### **列表渲染**v-for

v-for="item in items"

v-for="(item，index) in items"

index是索引

遍历对象会输出所有的属性的值value

也可选属性名name,索引值index

v-for="(value，name，index) in items"

将v-bind:key属性添加到div里与v-for配合，可以用更好的diff算法维护DOM数据。

数组更新检测：

下面重新复习一下数组方法

![img](https://img-blog.csdnimg.cn/20200713112934848.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDMyNDEyNA==,size_16,color_FFFFFF,t_70)

- 先确定index为0的地方是头
- `push()`添加尾巴，返回length
- `pop()`去除尾巴，返回尾巴
- `shift()`去除头，返回头
- `unshift()`添加头，返回length
- `splice(a,b)`起始索引a，要删除的项数b，可选：要添加的数组
- `sort()`字符串从小到大排序
- `reverse()`反转



###### v-on="动作"||||@"动作"

动作可以直接是a=a-1;

也可以是methods里的js函数（js函数放在computed里会立即执行一次



v-on:click之后也可以添加字符修饰，修饰符可以串联使用

- `.stop` - 阻止冒泡
- `.prevent` - 阻止默认事件
- `.capture` - 阻止捕获
- `.self` - 只监听触发该元素的事件
- `.once` - 只触发一次
- `.left` - 左键事件
- `.right` - 右键事件
- `.middle` - 中间滚轮事件



###### v-model双向绑定

v-model后面的值是双向绑定的

双向绑定的意思是客户端对数据的修改也可以影响到页面。

它支持的标签有：textarea，input:text,checkbox,radio,select

文本框里，model.lazy:按下enter之后数据才会发生改变.同样model.number之后才能自动识别成数字。



### 组件component

和自定义标签有点像，不同之处是自定义标签需要字符。

全局注册方法**Vue.component（tagName，options）**

但是不会这样做，一般就是在src/view新建一个vue文件来封装一个组件。



局部注册