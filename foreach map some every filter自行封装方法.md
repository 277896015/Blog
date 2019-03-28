

# forEach()

对数组的每个元素执行一次提供的函数。
遍历数组的每一项，特点是如果数组中途被修改，依然按照初始值进行不会随之改变。
原理是封装一个函数，接收函数作为参数，函数里面设置循环，遍历传进来的每个参数和对应的下标。

```
// 封装一个数组的 _forEach 方法 传参为一个函数
        function _forEach(fn){
            // 循环数组的每一项   谁调用的this就指向谁
            for(let i = 0; i < this.length; i++){
                // 循环传进来的函数的三个参数
                fn(this[i],i,this)
            }
        }
        
        // 定义一个数组
        let arr = ['4','5','6']
        // 将定义的这个数组方法放到Array的prototype下面
        Array.prototype._forEach = _forEach;
        console.log(Array.prototype)
        // 数组arr调用_forEach方法并传参
        arr._forEach(function(item,index,arr){
            // 打印传进来的参数
            console.log(item,index,arr)
        })
```

---

# map()

// map方法第一个参数 为回调函数，该函数拥有三个参数
// 第一个参数表示array数组中的每一个
// 第二参数表示当前遍历的索引值
// 第三个参数表示数组
// 该函数中的this指向map方法的第二个参数，若该参数不存在，则this指向丢失

封装:

```
Array.prototype._map = function(fn, context){
var tmp = [];
if(typeof fn === 'function'){
var k = 0;
var len = this.length;
for(; k<len; k++){
tmp.push(fn.call(context, this[k], k, this));
}
}else {
console.log("fn 不是一个函数");
}
return tmp;
}
var newArr = [1,2,3,4]._map(function(item, i, array){
console.log(item, i, array, this);
return item + 1;
}, {a: 1});
```

# Filter()

filter()方法使用指定的函数测试所有元素，并创建一个包含所有通过测试的元素的新数组。

    filter()基本语法：
       arr.filter(callback[, thisArg])

 　　filter()参数介绍：
   　　 参数名    说明
   　　 callback   用来测试数组的每个元素的函数。调用时使用参数 (element, index, array)
    　　返回true表示保留该元素（通过测试），false则不保留。
    　　thisArg    可选。执行 callback 时的用于 this 的值。

　　filter()用法说明：

　　　　filter 为数组中的每个元素调用一次 callback 函数，并利用所有使得 callback 返回 true 或 等价于 true 的值 的元素创建一个新数组。
　　　　callback 只会在已经赋值的索引上被调用，对于那些已经被删除或者从未被赋值的索引不会被调用。那些没有通过 callback 测试的元素会被跳过，不会被包含在新数组中。

　　　　callback 被调用时传入三个参数：

　　　　元素的值
　　　　元素的索引
　　　　被遍历的数组
　　　　如果为 filter 提供一个 thisArg 参数，则它会被作为 callback 被调用时的 this 值。否则，callback 的this 值在非严格模式下将是全局对象，严格模式下为 undefined。

　　　　filter 不会改变原数组。

　　　　filter 遍历的元素范围在第一次调用 callback 之前就已经确定了。在调用 filter 之后被添加到数组中的元素不会被 filter 遍历到。
　　　　如果已经存在的元素被改变了，则他们传入 callback 的值是 filter 遍历到它们那一刻的值。被删除或从来未被赋值的元素不会被遍历到。

***自封装Filter():***

```
Array.prototype._filter = function(func) {
var arr = this;
var temp = [];
for (var i = 0; i < arr.length; i++) {
if (func(arr[i],i,arr)) {
temp.push(arr[i]);
}
}
return temp;
}


```

# Array.prototype.some()


  `**some()**` 方法测试是否至少有一个元素通过由提供的函数实现的测试。

**注意：**对于放在空数组上的任何条件，此方法返回`false`。

## 语法

```
arr.some(callback(element[, index[, array]])[, thisArg])
```

```
callback
```

<h4> 参数</h4>h4>

用来测试每个元素的函数，接受三个参数：

- `element`

  数组中正在处理的元素。

- `index` 可选

  数组中正在处理的元素的索引值。

- `array`可选

  `some()`被调用的数组。

`thisArg`可选

执行 `callback` 时使用的 `this` 值。

<h3>返回值：</h3>

如果回调函数返回任何数组元素的truthy值，则返回**true**；否则为`**false**`。

# 自封装



```
if (!Array.prototype.some) {
  Array.prototype.some = function(fun/*, thisArg*/) {
    'use strict';

​```
if (this == null) {
  throw new TypeError('Array.prototype.some called on null or undefined');
}

if (typeof fun !== 'function') {
  throw new TypeError();
}

var t = Object(this);
var len = t.length >>> 0;

var thisArg = arguments.length >= 2 ? arguments[1] : void 0;
for (var i = 0; i < len; i++) {
  if (i in t && fun.call(thisArg, t[i], i, t)) {
    return true;
  }
}

return false;
​```

  };
}
```

----

# every() 方法

## 定义和用法

every() 方法用于检测数组所有元素是否都符合指定条件（通过函数提供）。

every() 方法使用指定函数检测数组中的所有元素：

- 如果数组中检测到有一个元素不满足，则整个表达式返回 *false* ，且剩余的元素不会再进行检测。
- 如果所有元素都满足条件，则返回 true。

**注意：** every() 不会对空数组进行检测。

**注意：** every() 不会改变原始数组。



## 语法

```
array.every(function(currentValue,index,arr), thisValue)
```

## 参数说明

*function(currentValue, index,arr)*  必须。函数，数组中的每个元素都会执行这个函数

函数参数:

1. *currentValue*   必须。当前元素的值
2. *index*    可选。当前元素的索引值
3. *arr*    可选。当前元素属于的数组对象



*thisValue*    : 可选。对象作为该执行回调时使用，传递给函数，用作 "this" 的值。
如果省略了 thisValue ，"this" 的值为 "undefined"

---

# 自行封装 every

```js
if (!Array.prototype.every) {
  Array.prototype.every = function(callbackfn, thisArg) {
    'use strict';
    var T, k;

    if (this == null) {
      throw new TypeError('this is null or not defined');
    }

    // 1. Let O be the result of calling ToObject passing the this 
    //    value as the argument.
    var O = Object(this);

    // 2. Let lenValue be the result of calling the Get internal method
    //    of O with the argument "length".
    // 3. Let len be ToUint32(lenValue).
    var len = O.length >>> 0;

    // 4. If IsCallable(callbackfn) is false, throw a TypeError exception.
    if (typeof callbackfn !== 'function') {
      throw new TypeError();
    }

    // 5. If thisArg was supplied, let T be thisArg; else let T be undefined.
    if (arguments.length > 1) {
      T = thisArg;
    }

    // 6. Let k be 0.
    k = 0;

    // 7. Repeat, while k < len
    while (k < len) {

      var kValue;

      // a. Let Pk be ToString(k).
      //   This is implicit for LHS operands of the in operator
      // b. Let kPresent be the result of calling the HasProperty internal 
      //    method of O with argument Pk.
      //   This step can be combined with c
      // c. If kPresent is true, then
      if (k in O) {

        // i. Let kValue be the result of calling the Get internal method
        //    of O with argument Pk.
        kValue = O[k];

        // ii. Let testResult be the result of calling the Call internal method
        //     of callbackfn with T as the this value and argument list 
        //     containing kValue, k, and O.
        var testResult = callbackfn.call(T, kValue, k, O);

        // iii. If ToBoolean(testResult) is false, return false.
        if (!testResult) {
          return false;
        }
      }
      k++;
    }
    return true;
  };
}
```

