## 检测数组的方法

首先： `let arr = [];`

### 1.通过instanceof运算符判断

从构造函数入手:可以判断一个对象是否是在其原型链上原型构造函数中的属性。

```js
console.log(arr instanceof Array);   //true
复制代码
```

再说说 typeof 和 instanceof 的区别？ 两者都可以用来判断变量，typeof会返回基本类型，而instanceof只会返回一个布尔值。

### 2.通过constructor判断

这个属性是返回对象相对应的构造函数，Object的每个实例都有构造函数 constructor，用于保存着用于创建当前对象的函数。

```js
console.log(arr.constructor === Array);   //true
复制代码
```

### 3.通过数组自带的isArray方法判断

ES5中新增了Array.isArray方法,IE8及以下不支持，用于确定传递的值是否是一个 Array。

```js
console.log(Array.isArray(arr));   //true
复制代码
```

### 4.通过isPrototypeOf()方法判断

从原型入手，Array.prototype  属性表示 Array 构造函数的原型，

其中有一个方法是 isPrototypeOf() 用于测试一个对象是否存在于另一个对象的原型链上。

```js
console.log(Array.prototype.isPrototypeOf(arr));   //true
复制代码
```

### 5.通过Object.getPrototypeOf方法判断

Object.getPrototypeOf() 方法返回指定对象的原型，所以只要跟Array的原型比较即可。

```js
console.log(Object.getPrototypeOf(arr) === Array.prototype); // true
复制代码
```

### 6.通过Object.prototype.toString.call()判断

虽然Array也继承自Object，但js在Array.prototype上重写了toString，而我们通过toString.call(arr)实际上是通过原型链调用了。可以获取到变量的不同类型。

```js
console.log(Object.prototype.toString.call(arr) === '[object Array]');   //true

console.log(Object.prototype.toString.call(arr).slice(8,-1)=== 'Array');   //true

console.log(Object.prototype.toString.call(arr).indexOf('Array') !== -1);    //true
复制代码
```