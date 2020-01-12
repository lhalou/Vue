# v-bind以及class与style的绑定

### 应用场景

DOM元素经常会动态的绑定一些class类名或style样式。

### v-bind复习

```
<div id = "demo">
  <a :href = "url">这是链接</a>
  <img :src = "imgSrc">
</div>
<script>
  var app = new Vue({
    el: '#demo',
    data: {
      url: 'http://www.baidu.com',
      imgSrc: 'https://img.iplaysoft.com/wp-content/uploads/2019/free-images/free_stock_photo.jpg'
    }
  })
</scrip>
```
链接的href属性和图片的src属性都可以被动态舍生孩子了，当数据变化时，就会重新渲染。

在数据绑定中，最常见的两个需求就是元素的样式名称.class和内联样式style的动态绑定，他们也是HTML的属性，因此可以使用`v-bind`指令。我们只需要用`v-bind`计算出表达式的最终字符串即可。不过有时候表达式逻辑较复杂，使用字符串的拼接方法较难阅读和维护，所以vue.js增强了对class和style的绑定。

### 绑定class

1. 对象语法：键表示class类名，值为布尔值，true表示应用样式，false表示不应用。
   ```
   <div :class = "{divStyle:isDiv,borderStyle:isBorder}"></div>
   data: {
     isDiv: true, //应用
     isBorder: false //不应用
   }
   ```
2. 当class表达式过长或逻辑复杂时，还可以绑定一个计算属性.键为类名。
   ```
   <div :class = "classNames"></div>
   data: {
     isDiv: true, //应用
     isBorder: false //不应用
   },
   computed: {
     classNames:function(){
       return {
         active: this.isDiv && !this.isBorder
       }
     } 
   }
   ```
3. 绑定class的数组语法：数组中的元素直接对应类名
   当需要应用多个class时，可以使用数组语法，给:class绑定一个数组，应用一个class列表.
   ```
   <div :class = "[activeClass,errorClass]"></div>
   data: {
     activeClass: 'active',
     errorClass: 'error'
   }
   ```
4. 数组语法和对象语法的混用
   数组中的数组样式一定会应用，对象样式应用与否取决于布尔值。
   ```
   <div :class = "[{'activeClass':isActive},errorClass]">
   data: {
     isActive: false,
     errorClass: 'error'
   }
   ```

### 绑定内联样式style 

使用`v-bind`绑定`style`与绑定`class`类似，也有对象语法和数组语法，看起来很像在元素上直接写css。
1. 对象语法：键表示css属性名，值表示属性值。
   ```
   <div :style = "{'color':color,'fontSize':fontSize}">
   data: {
     color: 'red',
     fontSize: '30px'
   }
   ```
2. 数组语法：几乎不使用
   ```
   <div :style = "[colorStyle,fontSizeStyle]"></div>
   data: {
     colorStyle: {
       color: red
     },
     fontSizeStyle: {
       fontSize: 30px
     }
   }
   ```
3. css属性名使用驼峰（fontSize）或段和县分隔符命名（font-size）,但是要用引号括起来。
4. 使用style时，Vue.js会自动给特殊的css属性名增加前缀.
   