## Vue是什么？

Vue.js是一个轻巧、高性能、可组件化的MVVM库，同时具有非常容易上手的API。

Vue.js是一个构建数据驱动的Web界面的库。（数据是更新到modal，而不是界面）

Vue.js是一套构建用户界面的渐进式框架。与其他重量级框架不同的是，Vue采用自底向上增量开发的设计。Vue的核心库只关注视图层，并且非常容易学习，非常容易去其他库或已有项目整合。另一方面，Vue完全有能力驱动采用单文件组件和vue生态系统支持的库开发的复杂单页应用。数据驱动+组件化的前端开发。

简而言之：Vue.js是一个构建数据驱动的web界面的渐进式框架。VUe.js的目标是通过近可能简单的API实现响应的数据绑定和组合的视图组件。核心是一个响应式的数据绑定系统。

## Vue的引入

```
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
或者
```
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

## Vue.js的特性如下：

- 轻量级的框架；
- 双向数据绑定；
- 指令；
- 插件化（组件化）。

## 什么是MVVM框架

MVVM:MVVM是把MVC里的Controller和MVP里面的Presenter改成了VieModel。Model+ View+ViewModal。View的变化会自动更新到VieModel。VieModel的变化也会自动同步到View上显示。这种自动同步是因为VieModel中的属性实现了Observer。当属性变更时，都能触发对应的操作。

MVVM模式的框架有：AngularJS + Vue.js和Knockout + Ember.js.后两种的知名度较低以及是早起的框架模式。

View是HTML显示页面。
ViewModel，同时监控View和Modal两边的数据，是业务逻辑层（一切js可视业务逻辑，比如表单按钮提交，自定义事件的注册和处理逻辑都爱VieModel里面负责监控两边的数据。）
Model数据层，对数据进行处理，比如增删改查。

MVVM是Model-View-ViewModel的缩写。MVVM是一种设计思想。Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；View 代表UI 组件，它负责将数据模型转化成UI 展现出来，ViewModel 是一个同步View 和 Model的对象。

在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。

ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

## Vue的开发模式

- 通过script标签直接引入vue.js
- 通过vue的叫脚手架工具vue-cli来进行一键项目的搭建。

## vue.js的优点

- 低耦合。视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的"View"上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变。
- 可重用性。你可以把一些视图逻辑放在一个ViewModel里面，让很多view重用这段视图逻辑。
- 独立开发。开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计。
- 可测试。界面素来是比较难于测试的，而现在测试可以针对ViewModel来写
易用灵活高效




