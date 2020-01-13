# Vue内置指令

## 基本指令

- v-cloak:一般与display:none结合使用
 作用：解决初始化慢导致页面闪动的问题。在Vue实例编译完成之后才会渲染页面。在Vue.js还未加载完成的时候，不添加`v-cloak`便会在页面上看到{{mag}}，添加后便看不到了，但是存在渲染问题，所以一般与`display:none`结合使用。

- v-once
  定义它的元素或组件只渲染一次，后续无论怎么改变，都不会重新渲染。

## 条件渲染指令

- v-if，v-else-if，v-else
  1. `v-if`指令用于条件性的渲染一块内容，这块内容只会在指令的表达式返回`true`的时候被渲染。`v-if`后接等号，等号后的内容必须是布尔值.
  ```
  <div v-if = "9 > 5">因为9比5大，返回true，所以渲染</div>
  ```
  2. `v-if`和`v-else-if`和`v-else`三者必须跟着屁股走，否则将不会识别。
  3. `v-if`的弊端
    Vue在渲染元素时，出于效率考虑，会尽可能的复用已有元素而非重新渲染，因此会出现Bug。
  4. 解决办法：
    对不想被复用的元素，添加属性`key`,并且要保证`key`的值是唯一的。

- v-show
  `v-show`：显示与否取决于布尔甚至，值改变了css的`display`属性。
  ```
  <div v-show = "9 > 5">基本用法和v-if类似</div>
  ```

- v-if VS v-show
  1. `v-if`：是真正的条件渲染，因为它会确保在切换过程中条件块内的时间监听器和子组件适当地被销毁和重建。即实时渲染，页面显示就渲染，不显示就移除，不存在DOM结构中。
  2. `v-if`也是惰性的，如果在初始渲染时条件为假，则什么也不做，直到条件第一次变为真时，才会开始渲染条件。
  3. `v-show`：就简单很多了，不管初始条件是什么，元素总是会被渲染，并且只是简单的基于CSS进行条件切换。也就是说，元素永远存在于页面中，只是改变了css的`display`属性。
  4. `v-if`有更高的切换开销，而`v-show`有更高的渲染开销，因此如果需要非常频繁的切换，使用`v-show`较好，如果在运行时，条件很少改变，使用`v-if`较好。


## 列表渲染指令v-for

- 用法：当需要将一个数组遍历或枚举一个对象属性循环显示的时候，就会用到列表循环属性`v-for`。

- 使用场景：
  1. 遍历多个对象（遍历的一定是数组）
   `v-for`指令需要使用`item in items`形式的特殊语法，其中`items`是原始数据数组，而`item`则是被迭代的数组元素的别名（可以自己任意起名）。
   在`v-for`模块中，可以访问`items`（父作用域）的所有属性，例如`(item,index) in items`可以访问到元素`item`和索引`index`。
   在使用的时候，还可以使用`of`替代`in`作为分隔符，因为它更接近于JS迭代器的语法。
   ```
   <div v-for = "item of items"></div>
   ```
  2. 遍历一个对象的多个属性
   需要注意的是`(value,key,index) in items`中三者的顺序不可改变。

- 在v-for里使用值范围
  `v-for`也可以接受整数，在这种情况下，会把模板重复对应的次数。
  ```
  <span v-for = "n in 10">{{n}}</span> 
  // 1 2 3 4 5 6 7 8 9 10
  ```

- v-for维护状态
  当Vue正在更新使用`v-for`渲染的元素列表时，它默认使用"就地更新"的策略，如果数据项的顺序被改变，Vue将不会移动DOM元素来匹配数据项的顺序，而是就地更新每个元素，并且确保他们在每个索引位置正确的渲染。
  但是，这种只适用于依赖子组件状态或临时DOM状态。
  方法：为每个元素添加`key`。


## 数组更新检测

- 变异方法：会改变调用了这些方法的原始数组。
  Vue将被侦听的数组的变异方法进行了包裹，所以他们也将会触发视图的更新。
  1. `push()`：在数组末尾添加元素
  2. `pop()`：将数组的最后一项删除
  3. `shift()`：删除数组的第一个元素
  4. `unshift()`：在数组的开头添加一个元素
  5. `splice()`：添加或者删除元素
  6. `sort()`:排序
  7. `reverse()`：翻转

- 替换数组
  非变异方法：`filter()`，`concat()`，`slice()`他们将不会改变原始数组，而总是返回一个新数组，当使用以上方法时，可以用新数组替换旧数组。

- 两个数组变动的形式，Vue检测不到。
  1. 改变数组的指定项 `this.arr[0] = 'study'`
  2. 改变数组的长度 `this.arr.length = 1`

- 针对以上两个问题的解决办法
  1. `set`方法：用于改变数组的指定项。第一项为要改变的数组元素，第二项为要改变的元素的下标，第三项为要新插入的元素值。
   ```
   Vue.set(app.arr,1,'car) //原始数组下标1的元素值改为car
   ```
  2. `splice`方法：改变数组的长度
   ```
   this.arr.splice(0) 
   ```

- 显示过滤、排序后的结果
  `sort()`方法与`filter()`方法都要传入一个函数，作为排序、过滤的规则。
  1. 我们想要显示一个数组经过过滤或排序后的版本，而不是改变或重置原始数据，在这种情况下，可以使用一个计算属性来返回过滤后的数组。
   ```
   computed: {
       filterArr: function(){
           return this.arr.filter(function(i){
               return i.match(/oo/) //过滤出包含oo的元素
           })
       }
   }
   ```
  2. 在计算属性不适用的情况下（例如在v-for循环中）,可以使用一个方法。
   ```
   <li v-for = "i in enev(items)">{{i}}</li>
   methods: {
       even: function(items){
           return items.filter(function(item){
               return item.match(/oo/)
           })
       }
   }
   ```

## 事件以及修饰符

- 事件
  1. 用法：`v-on`绑定的事件类似于原生的`onclick`的写法，可以用`v-on`指令监听DOM事件，并在触发时运行一些JS代码。
   ```
   methods: {
       handle: function(count,event){
           count = count || 1
           this.count += count
       }
   }
   ```
   如果方法中带有参数（上实例为count)，但是在绑定时`@click = handle`不加括号，就会默认传入原生事件对象event。所以避免出错，应使用`@click = handle()`，此时也等价于用JS直接调用方法`app.handle()`。有时候，也需要在内联语句中访问原始的DOM事件，可以使用特殊的变量`$event`，把它传入方法。`@click = handle(8,$event)`。

- 修饰符
  使用修饰符时，顺序很重要，相应的代码会以同样的顺序产生，因此`v-on:click.prevent.self`会阻止所有的点击，而`v-on:click.self.prevent`只会阻止对元素自身的点击。
  包括：
  1. `.stop`:阻止单击事件继续传播
   ```
    <a v-on:click.stop="doThis"></a>
   ```
  2. `.prevent`：提交事件不再重载页面
   ```
    <form v-on:submit.prevent="onSubmit"></form>
   ```
  3. 修饰符可以串联
   ```
    <a v-on:click.stop.prevent="doThat"></a>
   ``` 
  4. 只有修饰符
   ```
    <form v-on:submit.prevent></form>
   ```
  5. `.once`：只执行一次，还可以应用到自定义的组件上。
   ```
   <a v-on.once>只执行一次</a>
   ```
  6. `.capture`:添加事件监听器时使用事件捕获模式,即内部元素触发的事件先在此处理，然后才交由内部元素进行处理
   ```
     <div v-on:click.capture="doThis">...</div>
   ```
  7. `.self`:只当在 event.target 是当前元素自身时触发处理函数.即事件不是从内部元素触发的
   ```
    <div v-on:click.self="doThat">...</div>
   ```
  8. `.passive`：滚动事件的默认行为 (即滚动行为) 将会立即触发，而不会等待 `onScroll` 完成。此修饰符尤其能够提升移动端的性能。
   ```
   <div v-on:scroll.passive="onScroll">...</div>
   ```

- 按键修饰符
  在监听键盘事件时，Vue允许为`v-on`在监听键盘事件时添加按键修饰符.
  ```
  <input v-on:keyup.enter = "submit">
  //只有在key是Enter时调用app.submit()
  ```

## 为什么在 HTML 中监听事件?

- 扫一眼 HTML 模板便能轻松定位在 JavaScript 代码里对应的方法。
- 因为你无须在 JavaScript 里手动绑定事件，你的 ViewModel 代码可以是非常纯粹的逻辑，和 DOM 完全解耦，更易于测试。
- 当一个 ViewModel 被销毁时，所有的事件处理器都会自动被删除。你无须担心如何清理它们。


   
   


    