## Vue与React对比？

**数据流：**

**react**主张函数式编程，所以推崇纯组件，数据不可变，单向数据流，

**vue**的思想是响应式的，也就是基于是数据可变的，通过对每一个属性建立Watcher来监听，当属性变化的时候，响应式的更新对应的虚拟dom。

**监听数据变化实现原理**：

- `Vue` 通过 `getter/setter` 以及一些函数的劫持，能精确知道数据变化，不需要特别的优化就能达到很好的性能
- `React` 默认是通过比较引用的方式进行的，如果不优化(`PureComponent/shouldComponentUpdate`)可能导致大量不必要的VDOM的重新渲染。

组件通信的区别：jsx和.vue模板。

- `HoC和Mixins`(在Vue中我们组合不同功能的方式是通过`Mixin`，而在`React`中我们通过`HoC`(高阶组件))。

**性能优化**

- `React: shouldComponentUpdate`
- `Vue`:内部实现`shouldComponentUpdate`的优化，由于依赖追踪系统存在，通过`watcher`判断是否需要重新渲染(当一个页面数据量较大时，`Vue`的性能较差，造成页面卡顿，所以一般数据比较大的项目倾向使用`React`)。

