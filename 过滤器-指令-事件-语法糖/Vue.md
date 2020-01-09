## 过滤器

- Vue.js支持在`{{}}`插值的尾部添加一小管道符`|`对数据进行过滤，经常用于格式化文本，比如字母全部大写，货币千位使用逗号分隔符，过滤的规则是自定义的，通过给Vue实例添加选项filters来设置。
`{{date | formateDate}} //|后面直接接过滤器的名字，不写（）`.
- 过滤器不只一个，所以将filters声明一个对象
```
var app = new Vue({
    el: '',
    data: {},
    filters: {
        formatDate: function(){}
    }
})
```
- 过滤器可以串联
```
{{date | filter1 | filter2....}}
```
- 过滤器可以接受参数
```
{{date | formatDate('arg1','arg2')}}
//其中的第一个参数和第二个参数分别对应过滤器的第二个和第三个参数，因为过滤器中的value是永远存在的。
```

## 指令和事件

- 指令（Directives)是Vue.js模板中最常用的一项功能，它带有前缀`v-`,能帮我们快速完成DOM操作，循环渲染，显示和隐藏。
- 指令的职责是：当表达式的值改变时，将其产生的连带影响，响应式的作用于DOM。
- 分类：
    1. v-text:解析文本。等价于{{apple}}`<span v-text = "apple"></span>`
    2. v-html:解析HTML。不能用`v-html`来复合局部模板，因为Vue不是基于字符串的模板引擎，反之，对用户界面（UI）,组件更适合作为重用和可组合的基本单位。`<span v-html = "apple"></span>"`
    3. v-bind:动态的更新HTML元素上的属性，比如id和class，绑定活的属性。
    4. v-on:用来绑定事件监听器。在普通元素上，`v-on`可以监听原生的DOM事件，除了`click`，还有`dbclick,keyuo,mousemove`等。表达式可以使一个方法名，这些方法都写在Vue实例的`methods`属性内，并且使函数的形式。函数内的`this`指向当前Vue实例本身，因此可直接使用`this.xxx`的形式来访问或修改数据。
        ```
        var app = new Vue({
            el:'',
            data: {},
            methods: {
                click: function(){}
            }
        })
        ```


## 语法糖

- 语法糖是指在不影响功能的情况下，添加某种简洁方法实现同样的效果，从而更加方便程序开发。
- 两种语法糖
```
v-bind ---> :
v-on ---> @
```