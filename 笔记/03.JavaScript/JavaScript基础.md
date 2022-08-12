# JavaScript基础

### 1.假值

JavaScript中有8个假值：flase、0、-0、0n、''/""/\`\`、undefined、null、NaN

### 2.typeof

typeof可以判断出基础类型（除了null）和Function，null和其余引用数据类型都返回Object。

intanceof检测右边的构造函数的prototype属性是否在左边的原型链上，若是返回true。

Object.prototype.toString.call()方法最好

```javascript
Object.prototype.toString({})       // "[object Object]"
Object.prototype.toString.call({})  // 同上结果，加上call也ok
Object.prototype.toString.call(1)    // "[object Number]"
Object.prototype.toString.call('1')  // "[object String]"
Object.prototype.toString.call(true)  // "[object Boolean]"
Object.prototype.toString.call(function(){})  // "[object Function]"
Object.prototype.toString.call(null)   //"[object Null]"
Object.prototype.toString.call(undefined) //"[object Undefined]"
Object.prototype.toString.call(/123/g)    //"[object RegExp]"
Object.prototype.toString.call(new Date()) //"[object Date]"
Object.prototype.toString.call([])       //"[object Array]"
Object.prototype.toString.call(document)  //"[object HTMLDocument]"
Object.prototype.toString.call(window)   //"[object Window]"
//可以使用slice（8，-1）取到object后面的值
```
