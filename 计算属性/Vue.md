## 计算属性

所有的计算属性都以函数的形式卸载Vue实例内的computed选项内，最终返回计算后的结果.
```
<div id = "demo">
  {{reverseText}}
</div>
var app = new Vue({
  el: '#demo',
  data: {
    text: '123,456,789';
  },
  computed: {
    reverseText: function(){
      return this.text.split(',').reverse().join(',');
    }
  }
})
```

## 计算属性的用法

在一个计算属性里可以完成各种复杂的逻辑，包括运算，函数调用等，只需要最终返回一个结果就可以（必须有return）。计算属性还可以依赖多个Vue实例的数据。只要其中任意数据变化，计算属性就会重新执行，视图也会更新。

## getter和setter函数

1. 如果计算属性直接跟一个function，默认就是getter函数.
  ```
  computed: {
    reverseText: function(){}
  }
  //等价于
  computed: {
    get: function(){}
  }
  ```
2. 每一个计算属性都包含一个setter和getter函数，在需要的时候，也可以提供一个seeter函数，当手动修改计算属性的值，就像修改一个普通数据那样时，就会触发setter函数，执行一些自定义操作。
3. 计算属还可以动态设置元素的样式名称class和内联样式style.
4. 计算属性可以依赖其他计算舒心，不仅可以依赖当前vue实例的数据，还可以依赖其他实例的数据。
  

## 计算属性的缓存

- 调用methods里的方法也可以起到和计算属性同样的作用。
- methods中的方法：如果调用方法，只要页面重新渲染，方法就会重新执行，不需要重新渲染，则不需要重新执行。
- 计算属性是基于它们的响应式依赖进行缓存的，只在相关响应式依赖发生改变时，它们才会重新求值。
- 计算属性不管渲不渲染，只要计算属性依赖的数据未发生改变，就永远不变。
- 何时使用计算属性，取决于你是否需要缓存，当遍历大数组和做大量计算时，应当使用计算属性，除非你不希望的到缓存。
  
## 倾听属性

Vue提供了一种更通用的方法来实现观察和响应Vue实例上的数据变动---倾听属性。
当需要在数据变化时执行异步或开销较大的操作时，这个方法很有用的。