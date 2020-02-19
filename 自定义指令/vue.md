# 自定义指令

### 自定义指令的基本用法

和组件类似分全局注册和局部注册，区别就是把`component`换成了`directive`。

### 钩子函数

指令定义函数提供了几个钩子函数
1. `bind`：只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个在绑定时执行一次的初始化操作。
2. `inserted`：被绑定元素插入父节点时调用（父节点存在即可，不必存在于document中).
3. `update`:被绑定的元素所在的模板更新时调用，而不论绑定值是否变化。通过比较更新前后的绑定值，可以忽略不必要的模板更新。
4. `componentUpdated`：被绑定元素所在模板完成一次更新周期时调用。
5. `unbind`：只调用一次，指令与元素解绑时调用。

### 钩子函数的参数

1. `el`：指令所绑定的元素，可以用来直接操作DOM。
2. `binding`：一个对象，包括以下属性
   - `name`:指令名，不包括v-前缀
   - `value`：所绑定的值，例如`v-my-directive = "1 + 1"`,则`value`的值是2.
   - `oldValue`:指令绑定的前一个值，仅在`update`和`componentUpdated`钩子函数中使用，无论值是否改变都可用。
   - `expression`：绑定值得字符串形式，例如`v-my-directive = "1 + 1"`,则`expression`的值是`"1 + 1"`.
   - `arg`：传给指令的参数，例如`v-my-directive:foo`,则`arg`的值是`"foo"`.
   - `modifiers`一个包含修饰符的对象。
3. `vnode`：Vue编译生成的虚拟节点
4. `oldVnode`:上一个虚拟节点，仅在`update`和`componentUpdated`钩子函数中使用。