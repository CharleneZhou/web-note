# 面向对象编程

# SOLID 原则

常见的使用OOP（面向对象编程语言）会犯的错误。总结了五个每个oop开发者需要遵守的准则

* <strong>单一职责原则(SRP)</strong>: 表明软件组件（函数，类，模块）必须专注于单一的任务（只有单一的职责）
* <strong>开/闭原则(OCP)</strong>: 表明软件设计时必须时刻考虑到（代码）可能的发展（具有扩展性），但是程序的发展必须最少地修改已有的代码（对已有的修改封闭）
* <strong>里氏替换原则(LRP)</strong>: 表明只要继承的是同一个接口，程序里任意一个类都可以被其他的类替换。在替换完成后，不需要其他额外的工作程序就能像原来一样运行
* <strong>接口隔离原则(ISP)</strong>: 表明我们应该将那些非常大的接口（大而全的接口）拆分成一些小的更具体的接口（特定客户端接口），这样客户端就只需关心他们需要用到的接口
* <strong>依赖反转原则(DIP)</strong>: 表明一个方法应该遵从依赖于抽象（接口）而不是一个实例（类）的概念

# 类

```
class Person {
  public name: string;
  public surname: string;
  public email: string;
  constructor(name: string, surname:string, email: string) {
    this.name = name;
    this.surname = surname;

    //单一职责原则
    if(this.validateEmail(email)) {
      this.email = email;
    }else{
      throw new Error("Invalid email!");
    }
  }
  validateEmail(){
    var re = /\S+@\S+\.S+/;
    return re.test(this.email)
  }
  greet(){
    alert("Hi");
  }
}
var me: Person = new Person("Remo", "Jansen","remo.jansen@wolksoftware.com")

```

当一个类不遵循SRP，知道了太多的事情（拥有太多属性）或做了太多事情（拥有太多方法），我们称这种对象为God对象。
这的 Person 类就是一个God对象，因此我们增加一个和 person 类的行为并无关联的 validateEmail 方法

```

class Email{
  public email: string;
  constructor( email: string){
    if(this.validateEmail(email)) {
      this.email = email;
    }else{
      throw new Error("Invalid email!");
    }
  }
}

validateEmail(){
  var re = /\S+@\S+\.S+/;
  return re.test(this.email)
}

class Person {
  public name: string;
  public surname: string;
  public email: Email;
  constructor(name: string, surname:string, email: Email) {
    this.email: email;
    this.name = name;
    this.surname = surname;
  }
  greet(){
    alert("Hi");
  }
}
```


# 关联、聚合和组合

# 继承

# 混合

# 范类型

# 接口

* 接口可以扩展其他接口或者类
* 接口可以定义数据和行为而不只是行为


# 命名空间

# 外部模块

# 异步模块定义

# CommonJS 模块

# ES6 模块

# Browserify 和通用模块定义

# 循环依赖
