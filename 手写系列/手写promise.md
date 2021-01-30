```javascript

// 基础版 （不支持异步）
const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected'

function myPromise (func) {
    const self = this;
    self.status = PENDING;
    self.value = null;
    self.reason = null;

    function resolve(value) {
        if(self.status === PENDING) {
            self.status = FULFILLED;
            self.value = value;
        }
    }

     function reject(value) {
        if(self.status === PENDING) {
            self.status = REJECTED;
            self.reason = value;
        }
    }

    func(resolve, reject);
}

myPromise.prototype.then = function(onFulfilled, onRejected) {
    const self = this;
    if(self.status === FULFILLED) {
        onFulfilled(self.value);
    }else if(self.status=== REJECTED) {
        onRejected(self.reason);
    }
}

```


``` javascript

// 支持异步版
const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected'

function myPromise (func) {
    const self = this;
    self.status = PENDING;
    self.value = null;
    self.reason = null;

    self.fulfilledAry = [];
    self.rejectedAry = [];

    function resolve(value) {
        if(self.status === PENDING) {
            self.status = FULFILLED;
            self.value = value;
            self.fulfilledAry.forEach(item => {
                item();
            })
        }
    }

     function reject(value) {
        if(self.status === PENDING) {
            self.status = REJECTED;
            self.reason = value;
            self.rejectedAry.forEach(item => {
                item();
            })
        }
    }

    func(resolve, reject);
}

myPromise.prototype.then = function(onFulfilled, onRejected) {
    const self = this;
    if(self.status === FULFILLED) {
        onFulfilled(self.value);
    }else if(self.status === REJECTED) {
        onRejected(self.reason);
    }else if(self.status === PENDING) {
        // 异步情况 将回调函数存入数组
        self.fulfilledAry.push(() => {onFulfilled(self.value)});
        self.rejectedAry.push(() => {onRejected(self.reason)});
    }

    return this;
}

```

手写promise

基础promise特点描述:


- 需要构建promise对象
- 自身有3个状态 默认为 pending
- 构建时的参数为要执行的函数，并自带两个参数 resolve reject 分别代表成功,失败
- 原型链上then函数负责触发回调，根据状态触发不同的回调
- 执行函数支持异步




