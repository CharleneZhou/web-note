> ES5 中作用域

``` 
const callbacks = []
for (var i = 0; i <= 2; i++) {
    callbacks[i] = function() {
        return i * 2
    }
}

console.table([
    callbacks[0](),//6
    callbacks[1](),//6
    callbacks[2](),//6
])
```
* 分析：
var 变量提升了，相当于var = 0 是全局的作用域；
函数表达式内容return中的i是变量的引用，不是对变量值的引用；
保留一个源情况，函数体内是一个表达式，而不是一个值；
表达式用到了i变量，此时i中是一个闭包，i的值是3时候去执行

> ES6 块作用域

```
const callbacks2 = []
for (let j = 0; j <= 2; j++) {
    callbacks2[j] = function() {
        return j * 2
    }
}

console.table([
    callbacks2[0](),//0
    callbacks2[1](),//2
    callbacks2[2](),//4
])
```

* 分析：
用let申明的变量是块作用域；
此时的闭包取决于块作用域，这个块作用域for循环这个花括号；
块作用域会把当前这个值保存下来，供后面闭包使用


> 分割函数执行 ES5中 
```
(function() {
    const foo = function() {
        return 1
    }
    console.log("foo()===1", foo() === 1)
    ;((function() {
        const foo = function() {
            return 2
        }
        console.log("foo()===2", foo() === 2)
    })())
})()
```

> ES6 分割函数执行
```
{
    function foo() {
        return 1
    }

    console.log("foo()===1", foo() === 1)
    {
        function foo() {
            return 2
        }

        console.log("foo()===2", foo() === 2)
    }
    console.log("foo()===1", foo() === 1)
}
```
* 分析：