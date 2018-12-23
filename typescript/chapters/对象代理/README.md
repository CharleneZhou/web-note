# proxy 代理 : 达到保护原始数据的效果。通过代理，数据只可读，不可写

> ES3,ES5 数据保护

```
var Person = function() {
  var data = {
    name: 'es3',
    sex: 'male',
    age: 15
  }
  this.get = function(key) {
    return data[key]
  }
  this.set = function(key, value) {
    if (key !== 'sex') {
      data[key] = value
    }
  }
}

// 声明一个实例
var person = new Person();
// 读取
console.table({name: person.get('name'), sex: person.get('sex'), age: person.get('age')});
// 修改
person.set('name', 'es3-cname');
console.table({name: person.get('name'), sex: person.get('sex'), age: person.get('age')});//此时修改了姓名
person.set('sex', 'female');
console.table({name: person.get('name'), sex: person.get('sex'), age: person.get('age')});//此时修改了性别无用；es3可以生效，但是在es5中要无效，想要达到效果，可以参考下面案例
```

* 分析：

  * Person声明实例后，可以通过对应的get读取，set修改Person内部数据

  * es3中，想要保护数据，通过api的方式，用闭包达到效果；ES5中通过Object.defineProperty只读的属性保护数据

> ES5

```
{
  var Person = {
    name: 'es5',
    age: 15
  };

  Object.defineProperty(Person, 'sex', {
    writable: false,
    value: 'male'
  });

  console.table({name: Person.name, age: Person.age, sex: Person.sex});//查看数据无误
  Person.name = 'es5-cname';
  console.table({name: Person.name, age: Person.age, sex: Person.sex});//修改名字，成功；因为保护的数据只设置了sex；
  try {
    Person.sex = 'female';
    console.table({name: Person.name, age: Person.age, sex: Person.sex});//修改sex属性，结果报错。因为sex数据为Object.defineProperty保护起来的
  } catch (e) {
    console.log(e);
  }
} 
```

* 分析：
  需要保护的数据，可以通过Object.defineProperty设置需要被保护的参数key值，设置读写状态

> ES6

```
{
  let Person = {
    name: 'es6',
    sex: 'male',
    age: 15
  };

  let person = new Proxy(Person, {//ES6原生提供的方法；person暴露给用户的操作对象
    get(target, key) {//get读操作；target代理的数据，这指Person；
      return target[key]
    },
    set(target,key,value){//set写操作
      if(key!=='sex'){
        target[key]=value;
      }
    }
  });

  console.table({
    name:person.name,
    sex:person.sex,
    age:person.age
  });//读取无误

  try {
    person.sex='female';
  } catch (e) {
    console.log(e);//报错：不允许操作
  } finally {

  }

}
```

