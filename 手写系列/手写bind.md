```javascript
Function.prototype.myBind = function (thisArg, ...list) {
  let self = this;
  if(typeof self !== 'function') {
      throw 'binder must be a function';
  }
  let bound = function (...arg) {
    return self.apply(thisArg, [...list, ...arg]);
  }

  bound.prototype = Object.create(self.prototype);
  bound.prototype.constructor = self;

  return bound;
}
```

关于bind

手写代码最重要的一点就是对本身的功能了解清楚

bind本身是Function对象来改变this指向的方法，第一个参数为要指向的对象，第二个及以后的参数传递给原函数，同时本身返回一个方法并且可以接参数

根据上述特点

- 先确保调用者本身是function（上述代码其实是双保险）
- 返回一个function（构建了一个bound并返回）
- bind支持多参数，同时保证返回的方法也支持参数
- 比较容易忽略的一点是原型链的完整需要保证
