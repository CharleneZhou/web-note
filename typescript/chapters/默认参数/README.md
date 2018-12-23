# parameter 默认参数

> ES5\ES3 默认参数的写法

```
{
  function f(x, y, z) {
    if (y === undefined) {
      y = 7;
    }
    if (z === undefined) {
      z = 42
    }
    return x + y + z
  }
  console.log(f(1, 3));//46
} 
```

> ES6 默认参数

```
{
  
  function f(x, y = 7, z = 42) {
    return x + y + z
  }
  console.log(f(1, 3));//46
} 
{
  function checkParameter() {
    throw new Error('can\'t be empty')
  }
  function f(x = checkParameter(), y = 7, z = 42) {
    return x + y + z
  }
  console.log(f(1));//50
  try {
    f()
  } catch (e) {
    console.log(e);// 抛出异常 'can't be empty'
  } finally {}
} 
```

> ES3,ES5 可变参数

```
{
  function f() {
    var a = Array.prototype.slice.call(arguments);
    var sum = 0;
    a.forEach(function(item) {
      sum += item * 1;
    })
    return sum
  }
  console.log(f(1, 2, 3, 6));//12
} 
```

* 分析 ：
  这个地方的借助arguments 一个伪数组，获取参数列表

> ES6 可变参数

```
{
  function f(...a) {
    var sum = 0;
    a.forEach(item => {
      sum += item * 1
    });
    return sum
  }
  console.log(f(1, 2, 3, 6));//12
} 
```

* 分析：
  通过扩展运算符（...就是ES6语法中的扩展运算符）接收参数列表，并且这个参数是不固定的。

> ES5 合并数组

```
{
  var params = ['hello', true, 7];
  var other = [1, 2].concat(params);
  console.log(other);//[1,2, 'hello', true, 7]
} 
```

> ES6 利用扩展运算符合并数组

```
{
  var params = ['hello', true, 7];
  var other = [
    1, 2, ...params
  ];
  console.log(other);//[1,2, 'hello', true, 7]
}
```
