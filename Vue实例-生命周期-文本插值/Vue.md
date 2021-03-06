## Vue实例和数据绑定

1. Vue应用
每个Vue应用都是通过Vue函数创建一个新的Vue实例开始的。一个Vue应用由一个通过new Vue创建的根Vue实例以及可选的嵌套的，可复用的组件树组成。所有的Vue组件都是Vue实例，并且接受相同的选项对象（一些根实例特有的选项除外）。
2. 通过构造函数Vue就可以创建一个Vue的根实例，并启动Vue应用。----入口。
```
var app = new Vue({
    el: '',
    data: {
        msg: '你好';
    }
})
```
- 其中必不可少的一个选项就是el，el用于指定一个页面中已经存在的DOM元素，来挂载Vue实例。
- 通过Vue实例的data选项，可以声明应用内需要双向绑定的数据。建议所有会用到的数据都预先在data中声明，这样不至于将数据散落在业务逻辑中，难以维护，也可以指向一个已经有的变量。
- 访问属性
```
app.$el; //访问Vue实例的属性
app.msg; //访问data元素中的属性
```

## 生命周期钩子

1. created:实例创建完成后调用，此阶段完成了数据的观测等，但尚未挂载，$el还不可用，需要初始化处理一些数据时会比较有用。----还未挂载。
2. mounted:el挂载到实例上后，一般我们的第一个业务逻辑会在这里开始。相当于`$(document).ready()`----刚刚挂载.
3. beforeDestroy:实例销毁之前调用，主要解绑一些因共用。

- 生命周期钩子的this上下文指向调用它的Vue实例。
- 不要在选项属性或回调函数上使用箭头函数，比如`created:()=>console.log(this.a)`,因为箭头函数并没有this，this会作为变量一直向上级词法作用域查找，直到找到为止，经常报错。

## 模板语法

1. 模板语法
vue.js使用基于HTML的模板语法，允许开发者声明式的将DOM绑定至底层Vue实例的数据，所有的Vue.js的模板都是合法的HTML，所以能被遵循规范的浏览器和HTML解析器解析。
2. 文本插值与表达式
- 语法：使用“Mustache”语法：双大括号`{{}}`是最基本的文本插值方法，他会自动将我们双向绑定的数据实时显示出来。
- 在`{{}}`中，除了简单的绑定属性外，还可以使用JS表达式进行简单的运算，三元运算等。
- vue.js只支持单个表达式，不支持语句和流控制。
