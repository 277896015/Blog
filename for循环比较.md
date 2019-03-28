# 1.  for循环

用于创建一个循环,它包含了三个可选的表达式,三个可选的表达式包围在圆括号中并由分号分隔,后面跟随一个语句或一组语句在循环中执行.

语法：

```
for ([initialization]; [condition]; [final-expression])
   statement
```

参数：

`initialization ` 一个表达式 (包含赋值语句) 或者变量声明。典型地被用于初始化一个计数器。该表达式可以使用var关键字声明新的变量。初始化中的变量不是该循环的局部变量，而是与该循环处在同样的作用域中。该表达式的结果无意义。

`condition`  一个条件表达式被用于确定每一次循环是否能被执行。如果该表达式的结果为true， 循环体内的语句将被执行。 这个表达式是可选的。如果被忽略，那么就被认为永远为true。如果计算结果为false，那么执行流程将被跳到for语句结构后面的第一条语句。

final-expression  每次循环的最后都要执行的表达式。执行时机是在下一次`condition的计算之前。通常被用于更新或者递增计数器变量。

`statement`只要`condition的结果为true就会被执行的语句。` 要在循环体内执行多条语句，使用一个 [block](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Statements/block) 结构 (`{ ... }`) 来包含要执行的语句。没有任何语句要执行，使用一个 [empty](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/Empty) 语句 (`;`)。

### 一般使用

以下例子声明了变量i并被初始赋值为0，for语句检查i的值是否小于9，如果小于9，则执行语句块内的语句，并且最后将i的值递增。

```
for (var i = 0; i < 9; i++) {
   console.log(i);
   // more statements
}
```

---

# 2.   for...in

以任意顺序遍历一个对象的可枚举属性。对于每个不同的属性，语句都会被执行。

语法：for` `(variable ``in` `object) {...}

参数：

- `variable`

  在每次迭代时,将不同的属性名分配给*变量*。

- `object`

  被迭代其枚举属性的对象。

#### **for..in 不应该被用来迭代一个下标顺序很重要的 Array .**

----

# 3.   forEach()

`**forEach()**` 方法对数组的每个元素执行一次提供的函数。

语法：

```
array.forEach(callback(currentValue, index, array){
    //do something
}, this)

array.forEach(callback[, thisArg])
```

参数：

​		callback`为数组中每个元素执行的函数，该函数接收三个参数：

- currentValue(当前值)

  数组中正在处理的当前元素。

- index(索引)

  数组中正在处理的当前元素的索引。

- array

  forEach()方法正在操作的数组。

`thisArg`可选可选参数。当执行回调 函数时`用作``this的`值(参考对象)。



### **描述：**

```
forEach` 方法按升序为数组中含有效值的每一项执行一次`callback` 函数，那些已删除（使用`delete`方法等情况）或者未初始化的项将被跳过（但不包括那些值为 `undefined 的项）（例如在稀疏数组上）。
```

`callback` 函数会被依次传入三个参数：

- **数组当前项的值**
- **数组当前项的索引**
- **数组对象本身**

如果`给forEach传递了thisArg`参数，当调用时，它将被传给`callback` 函数，作为它的this值。否则，将会传入 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined) 作为它的this值。callback函数最终可观察到this值，这取决于 [函数观察到`this`的常用规则](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)。

`forEach` 遍历的范围在第一次调用 `callback` 前就会确定。调用`forEach` 后添加到数组中的项不会被 `callback` 访问到。如果已经存在的值被改变，则传递给 `callback` 的值是 `forEach` 遍历到他们那一刻的值。已删除的项不会被遍历到。