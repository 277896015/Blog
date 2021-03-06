

# forEach()

对数组的每个元素执行一次提供的函数。
遍历数组的每一项，特点是如果数组中途被修改，依然按照初始值进行不会随之改变。
原理是封装一个函数，接收函数作为参数，函数里面设置循环，遍历传进来的每个参数和对应的下标。

```
//forEach方法封装 _forEach
        Array.prototype._forEach = function (callback, context) {
            for (var k = 0; k < this.length; k++) {
                callback.call(context, this[k], k, this);
            }
        }

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
 //map方法封装 _map
        Array.prototype._map = function (callback, context) {
            var temp = [];
            for (var k = 0; k < this.length; k++) {
                temp.push(callback.call(context, this[k], k, this));
            }
            return temp;
        }
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

        //filter方法封装 _filter
        Array.prototype._filter = function (callback, context) {
            var temp = [];
            for (var k = 0; k < this.length; k++) {
                callback.call(context, this[k], k, this) ? temp.push(this[k]) : "";
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
     //some方法封装 _some
        Array.prototype._some = function (callback, context) {
            for (var k = 0; k < this.length; k++) {
                if (callback.call(context, this[k], k, this)) {
                    return true;
                }
            }
            return false;
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
        //every方法封装 _every
        Array.prototype._every = function (callback, context) {
            for (var k = 0; k < this.length; k++) {
                if (!callback.call(context, this[k], k, this)) {
                    return false;
                }
            }
            return true;
        }

```

