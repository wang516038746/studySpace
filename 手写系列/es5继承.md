``` javascript
function parent() {
    this.name = 'parent';
    this.age = '30';
}
parent.prototype.sayName = function() {
    console.log(this.name);
}

function child() {
    parent.call(this);
    this.other = 'other';
}

child.prototype = parent.prototype;
child.prototype.constructor = child;
```


核心要点:
- 保留携带的属性 通过call获取
- 获取prototype
- 保证prototype.constructor 是自己