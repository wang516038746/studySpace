```javascript
Function.prototype.myCall = function (thisArg) {
    const self = this;
     if(typeof self !== 'function') {
      throw 'binder must be a function';
    }
    thisArg._fn = this;
    const argList = [...arguments].slice(1);
    let result = thisArg._fn(...argList);
    delete thisArg._fn;

    return result
}
```

手写call

先思考call本身的功能

本身功能改变this指向为第一个参数，第2~~n个参数为原方法的参数，返回值为调用结果

解题思路
- 主要需要思考this指向的转化，将参数本身为对象主体，再将原本的function挂载上去进行调用即可