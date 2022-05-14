```javascript
Function.prototype.myCall = function (context, ...args) {
  if (!context || context === null) {
    context = window;
  }
  // 创造唯一的key值  作为我们构造的context内部方法名
  let fn = Symbol();
   context[fn] = this //给context添加一个方法 指向this
            // 处理参数 去除第一个参数this 其它传入fn函数
   return context[fn](...args) //执行fn
  delete context[fn] //删除方法


};

// apply原理一致  只是第二个参数是传入的数组
Function.prototype.myApply = function (context, args) {
  if (!context || context === null) {
    context = window;
  }
  // 创造唯一的key值  作为我们构造的context内部方法名
  let fn = Symbol();
   context[fn] = this //给context添加一个方法 指向this
            // 处理参数 去除第一个参数this 其它传入fn函数
   return context[fn](...args) //执行fn
  delete context[fn] //删除方法


};

//bind实现要复杂一点  因为他考虑的情况比较多 还要涉及到参数合并(类似函数柯里化)

Function.prototype.myBind = function (context, ...args) {
  if (!context || context === null) {
    context = window;
  }
  // 创造唯一的key值  作为我们构造的context内部方法名
            //返回一个绑定this的函数，我们需要在此保存this
            let self = this
                // 可以支持柯里化传参，保存参数
            let arg = [ ...args]
                // 返回一个函数
            return function() {
                //同样因为支持柯里化形式传参我们需要再次获取存储参数
                let newArg = [...arguments]
                console.log(newArg)
                    // 返回函数绑定this，传入两次保存的参数
                    //考虑返回函数有返回值做了return
                return self.apply(context, arg.concat(newArg))
            }
};

//用法如下

// function Person(name, age) {
//   console.log(name); //'我是参数传进来的name'
//   console.log(age); //'我是参数传进来的age'
//   console.log(this); //构造函数this指向实例对象
// }
// // 构造函数原型的方法
// Person.prototype.say = function() {
//   console.log(123);
// }
// let obj = {
//   objName: '我是obj传进来的name',
//   objAge: '我是obj传进来的age'
// }
// // 普通函数
// function normalFun(name, age) {
//   console.log(name);   //'我是参数传进来的name'
//   console.log(age);   //'我是参数传进来的age'
//   console.log(this); //普通函数this指向绑定bind的第一个参数 也就是例子中的obj
//   console.log(this.objName); //'我是obj传进来的name'
//   console.log(this.objAge); //'我是obj传进来的age'
// }

// 先测试作为构造函数调用
// let bindFun = Person.myBind(obj, '我是参数传进来的name')
// let a = new bindFun('我是参数传进来的age')
// a.say() //123

// 再测试作为普通函数调用
// let bindFun = normalFun.myBind(obj, '我是参数传进来的name')
//  bindFun('我是参数传进来的age')

```

```js
   Function.prototype.bind = function(context) {
        //返回一个绑定this的函数，我们需要在此保存this
        let self = this
            // 可以支持柯里化传参，保存参数
        let arg = [...arguments].slice(1)
            // 返回一个函数
        return function() {
            //同样因为支持柯里化形式传参我们需要再次获取存储参数
            let newArg = [...arguments]
            console.log(newArg)
                // 返回函数绑定this，传入两次保存的参数
                //考虑返回函数有返回值做了return
            return self.apply(context, arg.concat(newArg))
        }
    }

    // 搞定测试
    let fn = Person.say.bind(Person1)
    fn()
    fn(18)
```
