# Stack 栈

## 栈数据结构

栈(stack) 是一种遵循先进后出(LIFO)原则的有序集合. 新添加的或待删除的元素保存在栈的同一端, 称为栈顶, 另一端称为栈底.

### 创建Stack

先创建一个class来表示栈

使用数组保存栈里的元素

为栈声明一些方法
* `push(element(s))`: 添加一个(或几个)新元素到栈顶
* `pop()`: 移除栈顶的元素, 返回被删除的元素
* `peek()`: 返回栈顶的元素, 不对栈做任何修改
* `isEmpty()`: 判断栈内元素是否为空; 为空返回`true`, 否则返回`false`
* `clear()`: 移除栈里所有元素
* `size()`: 返回栈里元素个数
* `print()`: 打印栈内所有元素

### 使用 Stack

## ES6和stack类

### 用ES6语法声明stack类

ES6的类, 变量只能在`constructor`中声明; 但是变量却是公共的

### 用ES6的限定作用域`Symbol`实现类
`Symbol` 基本类型, 不可变的, 可以用作对象的属性

但ES6中 `Object.getOwnPropertySymbols()` 可以获取类声明中所有`Symbols`属性; 通过这个方法就可以直接获得栈声明中的`items`数组, 并直接对其进行操作
```js
let objectSymbols = Object.getOwnPropertySymbols(stack);
```

### WeakMap

`Weakmap`可以存储键值对, key: object; value: 任意数据类型

使用闭包将items变为私有属性;

使用这种方法, 扩展类无法继承私有属性 ?

### 用栈解决问题

#### 十进制转换到二进制

### 中缀表达式变成等价的后缀表达式的算法

中缀表达式按操作符的优先级进行计算, 后缀表达式中只有操作数和操作符. 操作符在两个操作数之后. 严格按照从左到右的顺序依次执行每一个操作. 每遇到一个操作符, 就将前面两个数执行相应的操作

用后缀表达式计算中缀表达式: 遇到的操作数暂存在一个操作数栈中, 遇到操作数, 便从栈中pop()出两个操作数, 将结果存入操作数栈中, 直到后缀表达式中最后一个操作数处理完, 最后压入栈中的数就是后缀表达式的计算结果

0.3/(5*2+1)# == 0.3 5 2 * 1 + / #(操作数出现次序相同, 但运算符出现的次序是不同的)

需要一个栈单独存放`(`(新的计算空间?)

* 初始化一个空操作符栈和空结果字符串
* 从前到后读取中缀表达式的字符, 如果是操作数, 加到结果字符串后面
* 如果是操作符
  * 如果待入栈操作符优先级大于栈顶操作符, 直接入栈
  * 如果待入栈操作符优先级小于或等于栈顶操作符, 栈顶操作符加到结果字符串后面, 重复这一过程直到遇到"("或栈顶操作符优先级小于待入栈操作符, 待入栈操作符入栈
* "("直接入站
* ")", 将栈中操作符依次弹出至结果, 直到遇到一个"("结束(舍弃"(")

一个栈存放操作数, 一个数组存放结果(按顺序排放的后缀表达式)

对表达式每个字符进行处理
* 如果当前字符为操作数
  * 如果操作数栈顶存储的操作数的优先级大于或等于将要入栈的当前操作数时, 循环弹出栈顶元素, 将栈顶元素存入结果数组. 直到栈顶元素的优先级小于入栈操作数时, 或栈顶元素为"("时, 结束循环,当前操作数入栈
  * 如果操作数栈顶存储的操作数的优先级小于将要入栈的当前操作数时, 当前操作数入栈

* 如果当前字符为"("时, 直接入栈
* 如果当前字符为")"时, 循环弹出栈顶元素,存入结果数组. 直到栈顶元素为"("时(弹出,但不保存),结束循环(不保存当前字符).
    当前字符为数字, 存入结果数组 
* 最后如果操作数栈不为空, 依次弹出栈顶元素至结果数组

计算后缀表达式
创建新栈保存计算结果

对结果数组的每个字符进行处理
* .tirm() 去掉空白字符
* 如果当前字符为数字时, 存入计算结果栈
* 如果当前字符为操作数时, 进行两次弹出结果栈操作, 和当前字符拼接为字符串(表达式), 使用`eval()`计算结果. 再将结果重新`push`进结果数组

循环完毕后, 弹出结果数组栈顶元素(结果数组中应只存在唯一的元素)