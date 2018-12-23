# 箭头函数：arrow-function

> ES3,ES5

```
{
  var evens = [1, 2, 3, 4, 5];
  var odds = evens.map(function(v) {
    return v + 1
  });
  console.log(evens, odds);//[1,2,3,4,5],[2，3，4，5，6]
};
```

> ES6

```
{
  let evens = [1, 2, 3, 4, 5];
  let odds = evens.map(v => v + 1);
  console.log(evens, odds);//[1,2,3,4,5],[2，3，4，5，6]
} {
```

> ES3,ES5

```
  var factory = function() {
    this.a = 'a';
    this.b = 'b';
    this.c = {
      a: 'a+',
      b: function() {
        return this.a
      }
    }
  }

  console.log(new factory().c.b());//a+
};

```

* 分析： 
  this的指向是谁调用了这个函数，this指向谁；this的指向会根据函数调用而改变


> ES6 

```

{
  var factory = function() {
    this.a = 'a';
    this.b = 'b';
    this.c = {
      a: 'a+',
      b: () => {
        return this.a
      }
    }
  }
  console.log(new factory().c.b());//a
}
```

* 分析： 
  箭头函数的指向是定义时，这个函数的指向，不会因为谁调用了他而改变this的指向