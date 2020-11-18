## Stack

数据操作遵循后进先出，LIFO。 常用于编译器，计算机存储变量和执行栈，浏览器历史记录后退按钮


### 实现方法：

* push(element(s)): 向栈中添加一个或多个元素
* pop(): 删除栈顶元素，返回被删除的元素
* peek(): 返回栈顶元素，并不修改栈
* isEmpty(): 判空，栈内没有元素返回true，否则返回false
* clear(): 清空，删除栈内所有元素
* size(): 返回栈内包含元素的个数

##### 通过数组模拟stack

```js
class Stack {
    constructor() {
        this.items = [];
    }

    push(element) {
        this.items.push(element);
    }

    pop() {
        return this.items.pop();
    }

    peek() {
        return this.items[this.items.length - 1];
    }

    isEmpty() {
        return this.items.length === 0;
    }

    size() {
        return this.items.length;
    }

    clear() {
        this.items = [];
    }

    toString() {
        return this.items.toString();
    }
}
```


##### 通过对象模拟stack

```js

class Stack {
    constructor() {
        this.items = {};
        this.count = 0;
    }

    push(element) {
        this.items[this.count] = element;
        this.count++;
    }

    pop() {
        if (this.isEmpty()) {
            return undefined;
        }
        this.count--;
        const result = this.items[this.count];
        delete this.items[this.count];
        return result;
    }

    peek() {
        if (this.isEmpty()) {
            return undefined;
        }
        return this.items[this.count - 1];
    }

    size() {
        return this.count;
    }

    isEmpty() {
        return this.count === 0;
    }

    clear() {
        this.items = {};
        this.count = 0;
    }

    toString() {
        if (this.isEmpty()) {
            return '';
        }
        let objString = `${this.items[0]}`;
        for(let i = 1, i < this.count; i++) {
            objString = `${objString}, ${this.items[i]}`;
        }
        return objString;
    }

}

```

### 通过栈解决的问题

* #### 进制转换

```js
function baseConverter(decNumber, base) {
    const remStack = new Stack();
    const digits = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ';
    let num = decNumber;
    let baseString = '';

    if (!(base >= 2 && base <= 36)) return ''; // 因为0-9和a-z加起来总共只有36个

    while(number > 0) {
        remStack.push(number % base);
        number = Math.floor(number / base);
    }

    while(!remStack.isEmpty()) {
        baseString += digits[remStack.pop()];
    }

    return baseString;
}

console.log(baseConverter(31, 32));
```

tips: js原生toString和parseInt都可以用来转换进制, parseInt限制较多，不建议用

```js
(31).toString(32); // "v"
```


* #### 判断符号是否匹配

[LeetCode 20.有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

```js
function isVaild(s) {
    let stack = new Stack();

    for(let k of s) {
        switch(k) {
            case '[': case '{': case '(':
                stack.push(k);
                break;
            case ')':
                if (stack.pop() != '(') return false;
                break;
            case ']':
                if (stack.pop() != '[') return false;
                break;
            case '}':
                if (stack.pop() != '{') return false;
                break;
        }
    }
    return stack.isEmpty();
}
```