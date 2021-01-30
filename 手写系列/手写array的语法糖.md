### array.map
```javascript
Array.prototype.myMap = function(func) {
    const self = this;
    const result = [];
    for(let i = 0; i < self.length; i ++) {
        result.push(func(self[i], i));
    }
    return result;
}
```

Array.prototype.map方法特点

- 参数第一项function， 该function 自带2个参数 指针指向的value和对应的index
- function返回的结果为数组当前位置的值
- 返回为新生成的数组，原数组不变
- 第二个参数为一个初始值




### array.reduce
```javascript
Array.prototype.reduce = function(func, origin) {
    const self = this;
    if(self.length === 0) {
        return;
    }
    // 其实应该用arguments 来判断是否有origin,节省时间先用undefined吧
    
    let result = origin === undefined ? self[0] : func(origin, self[0]);

    for(let i = 1; i < self.length; i ++) {
        result = func(result, self[i]);
    }

    return result;
}


```

Array.prototype.reduce方法特点

- 参数为一个function,该function 自带两个参数 计算结果值和当前值
- 最终返回为一个结果
- 不影响原数组


### array.filter
```javascript
Array.prototype.filter = function(func) {
    const self = this;
    let result = [];
    for(let i = 0; i < self.length; i ++) {
        if(func(self[i])) {
          result.push(self[i]);
        }
    }
    return result;
}

```

Array.prototype.filter 方法特点

- 参数为一个function,该function 自带1个参数 为数组遍历到的当前值，function返回true的时候 当前值保留 否则放弃

- 最终返回为一个新数组
- 不影响原数组
