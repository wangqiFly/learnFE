```
const myNew = function (constructor) {
  return function (...args) {
    // 完成1、2两步，创建一个链接到构造函数的原型对象的对象
    const obj = Object.create(constructor.prototype)
    // 将obj作为构造函数的this上下文
    constructor.call(obj, ...args)
    // 如果构造函数有返回值，则将返回值作为实例对象返回，否则返回obj作为实例对象
    return constructor() || obj
  }
}
```

