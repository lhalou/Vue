## 使用组件的原因 

作用： 提高代码的复用性。

## 组件的使用方法：

1. 全局注册：
   ```
   Vue.component('my-component',{
     template: '<div>这是全局注册组件</div>'
   })
   //使用组件
   <my-component></my-component>
   ```
   优点： 所有的Vue实例都可用;
   缺点：权限太大，容错率降低。
   注意点：全局注册的组件一定要定义在所有的Vue实例之前。
2. 局部注册：
   ```
   var app = new Vue({
     el: '#app',
     components: {
       'my-component': {
         template: '<div>这是局部注册组件</div>'
       }
     }
   })
   ```
3. Vue组件的模板在某些情况下会受到HTML标签的限制，比如在`<table></table>`中只能还有`<tr></tr>,<td></td>`这些元素，所以直接在`<table></table>`中使用组件是无效的，此时可以使用**is属性**来挂载组件。
   ```
   <table>
    <tbody is = "my-component></tbody>
   </table>
   ```

## 组件的使用注意事项，奇技淫巧

- 组件的命名规则`小写字母 + -`;
- `template`中的内容必须使用DOM元素包裹，DOM元素可以嵌套；
- 在组件中，除了`template`之外，还可以使用`data,computed,methods`等选项;
- `data`在组件中使用时，必须是一个方法，因此每个实例可以维护一份被返回对象的独立的拷贝。
- 组件的复用
  ```
  <div>
    <div id="components-demo">
    <button-counter></button-counter>
    <button-counter></button-counter>
    <button-counter></button-counter>
  </div>
  ```
  **注意当点击按钮时，每个组件都会各自独立维护它的`count`。因为你每用一次组件，就会有一个它的新实例被创建。**

  

