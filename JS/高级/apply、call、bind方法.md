### 1. **`call()` 方法**

`call()` 方法是 JavaScript 中非常常用的一种技巧，它允许你指定函数执行时的 `this` 指向，并且可以传递一系列参数给函数。`call()` 会立即执行该函数。

#### **用法：**
```js
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: 'Alice' };

// 使用 call() 改变 this 指向并传递参数
greet.call(person, 'Hello', '!');

```


### 2. **`apply()` 方法**

`apply()` 和 `call()` 类似，唯一的区别是 `apply()` 接收参数的方式不同，`apply()` 将参数以数组或类数组的形式传入，而 `call()` 则是将参数逐一列出。

#### **用法：**
```js
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: 'Bob' };

// 使用 apply() 改变 this 指向并传递参数（数组形式）
greet.apply(person, ['Hi', '?']);

```
 


### 3. **`bind()` 方法**

`bind()` 方法与 `call()` 和 `apply()` 很相似，不同的是 `bind()` 不会立即调用函数，而是返回一个新的函数，这个新函数已经将 `this` 和参数绑定好。当你调用这个新函数时，`this` 和参数会自动应用。

#### **用法：**
```js
function greet(greeting, punctuation) {
  console.log(greeting + ', ' + this.name + punctuation);
}

const person = { name: 'Charlie' };

// 使用 bind() 返回一个新的函数
const boundGreet = greet.bind(person, 'Hey');
boundGreet('!'); // 返回新函数，并传递剩余的参数

```



## 20个练习习题

好的，下面是 20 个关于 `apply()`、`call()` 和 `bind()` 的练习题目，帮助你更好地掌握这几个方法。每个题目都带有提示和预期的答案，你可以通过这些题目来深入理解它们的使用场景和区别。

### 1. **练习：使用 `call()` 调用方法并改变 `this`**

- **问题**：写一个函数 `greet()`，它接受一个 `name` 参数，打印一个问候消息。在一个对象 `person` 上调用 `greet()`，并将 `this` 指向该对象。
- **提示**：使用 `call()` 方法。
- **预期输出**：`Hello, Alice!`

### 2. **练习：使用 `apply()` 改变 `this`**

- **问题**：写一个函数 `sum(a, b)`，它返回两个数字的和。在一个对象 `calculator` 上调用 `sum()`，并将 `this` 指向该对象。
- **提示**：使用 `apply()` 方法，并传递数组作为参数。
- **预期输出**：`10`

### 3. **练习：使用 `bind()` 绑定 `this`**

- **问题**：创建一个对象 `person`，其中包含 `name` 和一个方法 `sayHello()`。使用 `bind()` 使得 `sayHello()` 始终打印 `Hello, <name>`，并确保 `this` 始终指向 `person` 对象。
- **提示**：使用 `bind()` 方法。
- **预期输出**：`Hello, Alice`

### 4. **练习：`call()` 和 `apply()` 的参数传递**

- **问题**：创建一个函数 `multiply(a, b)`，它返回两个数字的乘积。使用 `call()` 和 `apply()` 分别传递不同数量的参数。
- **提示**：使用 `call()` 和 `apply()` 分别传递单个和数组参数。
- **预期输出**：`20`（`call()`）`20`（`apply()`）

### 5. **练习：`bind()` 和事件处理**

- **问题**：在一个对象 `timer` 中定义一个方法 `start()`，该方法通过 `setInterval` 每秒钟输出 `this.time`（时间）。使用 `bind()` 确保 `this` 始终指向 `timer`。
- **提示**：使用 `bind()` 绑定 `this`。
- **预期输出**：每秒钟输出 `this.time`，直到停止。

### 6. **练习：借用构造函数**

- **问题**：创建两个构造函数 `Person` 和 `Employee`。`Employee` 继承自 `Person`，请使用 `call()` 来借用 `Person` 的构造函数，给 `Employee` 添加 `name` 和 `job` 属性。
- **提示**：使用 `call()` 方法。
- **预期输出**：`name: Alice, job: Developer`

### 7. **练习：使用 `bind()` 预设参数**

- **问题**：创建一个函数 `add(a, b)`，它返回两个数的和。使用 `bind()` 返回一个新的函数，该函数默认第一个参数为 10。
- **提示**：使用 `bind()` 来预设参数。
- **预期输出**：`15`（假设第二个参数为 5）

### 8. **练习：`apply()` 和 `arguments`**

- **问题**：创建一个函数 `getMax()`，它接受任意数量的数字参数，使用 `apply()` 获取参数中的最大值。
- **提示**：使用 `Math.max()` 和 `apply()`。
- **预期输出**：`50`（假设传入的是 `10, 20, 30, 50`）

### 9. **练习：改变 `this` 的指向**

- **问题**：定义一个对象 `user`，它有一个方法 `getName()` 返回其 `name`。使用 `call()` 调用 `getName()`，并改变 `this` 指向另一个对象。
- **提示**：使用 `call()` 方法。
- **预期输出**：`Bob`

### 10. **练习：使用 `call()` 改变数组中的元素**

- **问题**：创建一个函数 `sumNumbers()`，它接受一个数组并返回该数组所有数字的总和。使用 `call()` 改变数组中的元素。
- **提示**：使用 `call()` 和 `Array.prototype.reduce()`。
- **预期输出**：`10`（假设传入 `[1, 2, 3, 4]`）

### 11. **练习：模拟 `bind()` 功能**

- **问题**：自己实现一个简易版的 `bind()` 方法，要求它返回一个新的函数，能够正确绑定 `this` 和参数。
- **提示**：实现 `bind()` 的基本逻辑。
- **预期输出**：`Hello, Alice!`

### 12. **练习：`bind()` 和部分应用**

- **问题**：写一个函数 `multiply(a, b)`，返回两个数的乘积。使用 `bind()` 创建一个函数，该函数始终将第一个参数固定为 `2`。
- **提示**：使用 `bind()` 返回部分应用的新函数。
- **预期输出**：`6`（假设第二个参数为 `3`）

### 13. **练习：使用 `apply()` 和类数组对象**

- **问题**：创建一个类数组对象 `args`，它模拟 `arguments` 对象，并使用 `apply()` 调用 `Math.min()`，返回其中的最小值。
- **提示**：使用 `apply()` 方法。
- **预期输出**：`1`（假设传入的是 `3, 1, 4, 2`）

### 14. **练习：`call()` 传递多个参数**

- **问题**：创建一个函数 `concatenateStrings()`，它接收任意多个字符串参数，并返回它们的连接结果。使用 `call()` 传递多个参数。
- **提示**：使用 `call()` 方法。
- **预期输出**：`Hello, Alice!`

### 15. **练习：使用 `bind()` 与函数式编程**

- **问题**：创建一个函数 `add(a, b)`，使用 `bind()` 生成一个新的函数，将 `a` 固定为 10。然后调用该新函数，传入 `b` 的值。
- **提示**：使用 `bind()` 方法。
- **预期输出**：`15`（假设传入 `5`）

### 16. **练习：借用 `setTimeout`**

- **问题**：创建一个对象 `person`，它有一个 `name` 和一个方法 `sayHi()`，该方法打印 `Hello, <name>`。使用 `bind()` 确保在 `setTimeout` 中 `this` 始终指向 `person` 对象。
- **提示**：使用 `setTimeout` 和 `bind()`。
- **预期输出**：`Hello, Alice!`（在 1 秒后）

### 17. **练习：使用 `apply()` 与 `Math` 方法**

- **问题**：创建一个函数 `findMin()`，它接受任意多个数字参数，返回这些数字中的最小值。使用 `apply()` 方法调用 `Math.min()`。
- **提示**：使用 `apply()` 方法。
- **预期输出**：`1`（假设传入的是 `10, 20, 30, 1, 5`）

### 18. **练习：`call()` 与数组**

- **问题**：创建一个函数 `printArgs()`，它接受任意数量的参数，并打印它们。使用 `call()` 调用 `printArgs()`，并将数组作为参数传递。
- **提示**：使用 `call()` 方法。
- **预期输出**：`[1, 2, 3, 4]`

### 19. **练习：使用 `call()` 动态改变 `this`**

- **问题**：写一个函数 `printFullName()`，它打印全名。在一个对象 `person` 上调用该方法，使用 `call()` 动态改变 `this`，将其指向另一个对象。
- **提示**：使用 `call()` 方法。
- **预期输出**：`Full name: Bob Smith`

### 20. **练习：使用 `bind()` 和事件绑定**

- **问题**：创建一个对象 `button`，它有一个方法 `click()`，该方法打印 `Button clicked!`。使用 `bind()` 为一个 HTML 按钮的点击事件绑定 `click()` 方法。
- **提示**：使用 `bind()` 来绑定事件处理函数。
- **预期输出**：点击按钮时，输出 `Button clicked!`

---

这些练习题涵盖了 `call()`、`apply()`