## render函数的初步了解

`template`标签下只允许有一个子节点，但是可以把所有的节点使用`div`包裹起来，就不会报错
```
Vue.component('child',{
  render: function(createElement){
    return createElement()
  }
})
```

## render函数的第一个参数

`render`函数的参数，第一个参数是必需的，必须是`createElement`，这个`createElement`本身就是一个方法，`createElement()`创造节点.
`createElement`这个方法中，第一个参数是必选，可以是`String | Object | Function`
- `String` ------ html标签
- `Object` ------ 一个含有数据项的选项
- `Function` ------ 方法返回含有数据选项的对象


## render函数的第二个参数

第二个参数是可选的，第二个参数是数据对象，只能是`Object`,对象属性有
- `'class':{}`
- `style:{}`
- `attrs:{}` 正常的html特性，比如`id`
- `domProps:{}`用来写原生的dom属性,`innerHTML,innerText,value`
- `on:{}`:添加事件

## render函数的第三个参数

第三个参数也是可选的，代表子节点，作为我们构建函数的子节点来使用，存的是虚拟节点.