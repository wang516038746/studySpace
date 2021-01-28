```javascript
Function.prototype.myApply = function (thisArg) {
    const self = this;
     if(typeof self !== 'function') {
      throw 'binder must be a function';
    }
    thisArg._fn = this;
    const argList = [...arguments].slice(1);
    let result = thisArg._fn(argList);
    delete thisArg._fn;

    return result
}
```

手写apply

先思考call本身的功能

本身功能改变this指向为第一个参数，第2~~n个参数为原方法的参数，返回值为调用结果

解题思路
- 参数手写call