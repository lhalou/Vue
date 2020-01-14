# 表单和 v-model

## v-model

Vue 提供了`v-model`指令，用于在**表单类元素**上双向绑定数据。它会根据控件类型自动选取正确的方法来更新元素。
`v-model`在内部为不同的输入元素使用不同的属性并抛出不同的事件：

1. `text`和`textarea`元素使用`value`属性和`input`事件；
2. `checkbox`和`radio`使用`checked`属性和`change`事件；
3. `select`字段将`value`作为 prop 并将`change`作为事件。

### input 和 textarea

`input`和`textarea`的用法几乎一样，所显示的值只依赖于所绑定的数据，不在关心初始化时插入的`value`。

```
<input type = "text" v-model = "value">{{value}}
```

在输入框中输入的数据，会让 vue 实例中的`data`中的`value`被赋相同的数据，{{value}}就会在页面实时渲染相同的数据，并且显示的数据值依赖于双向绑定的`value`。

### 单选框

1. 单个单选框，直接用``v-bind`绑定一个布尔值，此处使用`v-model`不生效。`v-bind:checked = "oneRadio"`.
2. 如果是组合使用，就需要`v-model`结合`value`使用。
   ```
   <input type = "radio" name = "checks" value = "run" v-model = "checkName">
   ```
   `v-model`绑定的是选中的单选框的`value`值，并且，此处所绑定的初始值可以使任意给的。即`checkName`的初始值可以为空，若想默认选中某一单选框，`checkName`的值就初始化为此单选框的`value`值即可。

### 复选框

1. 单个复选框，直接绑定一个布尔值，可以使用`v-model`，也可以使用`v-bind`。
   ```
   v-model = "oneRadio" / v-bind:checked = "oneRadio"
   ```
2. 如果是组合使用，就需要`v-model`来配合`value`使用，`v-model`绑定一个数组。如果绑定的是字符串，则会转化为`true / false`，所绑定的复选框与`checked`属性相对应。

### 下拉框

`v-modle`只能放在`<select></select>`标签上。

```
<select v-model = "selected"> ....... </select>
```

1. 单选下拉框：所绑定的`value`值初始化可以为数组，可以为字符串，有`value`直接优先匹配一个`value`值，没有`value`就匹配一个`text`值。
2. 多选下拉框：如果是多选，就需要`v-model`来配合`value`使用，`v-model`绑定一个数组，也可以使字符串。

**总结：**如果是单选，初始化最好是给定字符串，因为`v-model`此时绑定的是静态字符串或布尔值，如果是多选，初始化最好给定一个数组。

## 绑定值

对于单选按钮，复选框及选择框的选项，`v-model`绑定的值通常是静态字符串（对于复选框也可以是布尔值），但是有时我们想把值绑定到 Vue 实例的一个动态属性上，这时可以用`v-bind`实现，并且这个属性的值可以不是字符串。

### 单选框

给单选框动态动态绑定一个`value`值，就可以通过`v-model`来获取其动态`value`值。

```
<input type = "radio" v-model = "picked" v-bind:value = "value">
```

只需要用`v-bind`给单个单选框绑定一个`value`值，此时`v-model`绑定的就是它的`value`值。

### 复选框

```
<input type = "checkbox" v-model = "toggle" :true-value = "value1" :false-value = "value2">
```

这里的`true-value`和`false-true`特性并不会影响控件的`value`特性，因为浏览器在提交表单时并不会包含为选中的复选框。

### 下拉框

```
<select v-model = "selected" :value = {num:111}>
```

在`select`标签上绑定`value`值对`option`没有影响。

```
<option :value = {num:111}>run</option>
```

在`select`标签上使用`v-model`，在`option`上动态绑定`value`才会生效。

## 修饰符

1. `.lazy`：`v-model`默认是在`input`输入的时候同步输入框的数据，而`.lazy`修饰符，可以使其失去焦点或者敲回车键之后在更新。
2. `.number`：可以将输入类型转化为数字。
3. `.trim`：自动过滤输入过程中的首尾空格。
