* [在线体验使用](http://www.typescriptlang.org/play/)

# 设计目标

1. 微软公司 防止并排查一些运行是错误的最佳方式
2. 与JavaScript非常高的兼容性
3. 为大型项目提供一个构建机制
4. 对于发型版本的代码，没有运行时开销
5. 遵循当前以及未来出现的ECMAScript规范
6. 成为跨平台的开发工具

# 语言特性

> 全局安装 

```
sudo npm install -g typescript
```

# 类型

## 基本类型

| 类型  |  描述 |
|------| ------|
|boolean  | true false <br/>```var isDone:boolean=false```|
|number   |和JavaScript一样所有数字都是浮点数<br/>```var height:number=6```|
|string   |和JavaScript一样，表示文本<br/>```var name:string="Charlene"```|
|array    |数组类型 两种表现形式，<br/>第一种```var list:number[]=[1,2,3]```<br/>第二种```var list:Array<numver>=[1,2,3]```|
|enum     |为了给数字集更友好的命名；默认从0开始，可以手动更改这种默认行为；<br/>```enum Color {Red, Green, Blue};``` <br/>```var c:Color = Color.Green;```|
|any     | 可以表示任意的JavaScript类型值 <br/>```var notSure:any=4```<br/>```notSure = 'maybe a string instead```<br/>```notSure = false```|
|void    | any的对立面，即是所有类型都不存在的时候<br/>```function warnUser():void{alert("this is my warning message")}```|

* <font color="red" fontSize='24' fontWeight=700>注意</font>： 
  * 在typeScript中，我们不能把null或undefined当作类型使用；因为这两个不是typescript的基本类型
  * 在typescript中，申明变量var 、 let、const
    * 使用var声明的变量保存在最近的函数作用域中（如果不再任何函数中则在全局作用域中）
    * 使用let声明的变量保存在最近的比函数作用域小的快作用域中（如果不再任何块中则在全局作用域中）
    * const关键字会创建位置作用域中的常量，可以是全局作用域也可以是块作用域

## 联合类型

```
var path:string[] | string
path = '/temp/log.xml';
path = ['/temp/log.xml','/temp/error.xml'];
path = 1;//错误;因为没有声明number是它的类型
```

## 类型守护

使用typeof 或者instanceof运算符对类型进行验证
```
var x: any = {/*...*/};
if( typeof x === 'string') {
  console.log(x.splice(3, 1));//错误，‘string‘上不存在‘splice’方法
}
//x依然是any类型
x.foo();//合法
```

## 类型别名

使用type关键字声明别名

类型别名实质上与原来的类型一样，他仅仅是一个替代的名字

类型别名可以让代码的可读性更高，但是他也会导致一些问题

## 环境声明

```
customConsole.log("A log entry");//错误 cannot find name 'customConsole'

```
当访问DOM或BOM对象时，这些对象已经在typescript中被声明。可以使用declare操作符创建一个环境
```
interface ICustomConsole {
  log(arg: string) : void;
}
declare var customConsole: ICustomConsole

customConsole.log('A log entry');//成功
```

* <font color="red" fontSize='24' fontWeight=700>注意</font>： 
  * TypeScript默认包含一个名为lib.d.ts的文件，它提供了像DOM这种JavaScript内置库的接口声明
  * 使用.d.ts[]结尾的声明文件，是用来提高typescript对第三方库和像node.js或浏览器这种运行时环境的兼容性的

## 算数运算符 、比较运算符 、逻辑运算符 、 赋值运算符

和JavaScript一样 

# 流程控制语句

## 单一选择结构（if） 、 双选择结构（if...else） 、 三元操作符（ ? : ）、多选择结构（switch）、语句在顶部进行判断的循环（while)、语句在底部进行判断的循环(do...while)、迭代对象的属性(for...in)、计数控制器循环(for)

和JavaScript一样

# 函数

不仅可以给函数的参数加上类型，还可以给函数的返回值指定类型，返回值的类型正确与否，并且他们都不是必需的

```
var greet = (name: string):string => {
  if(name){
    return "Hi" + name;
  }else{
    return "Hi! my name is" + this.fullname
  }
}
```

```
function greet(name:string): string{
  if(name){
    return "Hi" + name;
  }else{
    return "Hi! my name is" 
  }
}

```
<font color=red fontSize=24 fontWieght=700>注意</font>
当处于类的内部时，使用箭头函数语法将会改变this操作符的工作机制

# 类

```
class Character{
  fullname: string;
  constructor(firstname: string, lastname: string){
    this.fullname = firstname+' '+lastname;
  }
  greet(name:string){
    if(name){
      return `hi! ${name}!my name is${this.fullname}`
    }else{
      return `hi! my name is${this.fullname}`;
    }
  }
}

var spark = new Character('Jacob','Keyes');
var msg = spark.greet();
alert(msg);//hi!my name is Jacob Keyes;
var msg1 = spark.greet('Dr.Halsey');
alert(msg1);//hi!Dr.Halsey!my name is Jacob Keyes;

```

this 操作符表明了这是一个成员访问操作

使用new操作符构造了Character类的一个实例，这回调用类的构造函数（constructor），按照定义对实例进行初始化

# 命名空间

命名空间，又称内部模块，被用于组织一些具有某些内在联系的特性和对象。命名空间能够使代码结构更清晰，可以使用<font color=red>namespace</font>和<font color=red>export</font>关键字
```
namespace Grometry{
  interface VectorInterface{ /*...*/ }//次接口在声明前，没有使用export，所以在命名空间外部，我们访问不到他

  export Vector2dInterface{ /*...*/ }

  export Vector3dInterface{ /*...*/ }

  export class Vecrot2d implements VectorInterface, Vector2dInterface{/*...*/}

  export class Vecrot3d implements VectorInterface, Vector3dInterface{/*...*/}
}

var Vector2dInterface: Geometry.Vector2dInterface = new Grometry.Vector2d();
var Vector3dInterface: Geometry.Vector3dInterface = new Grometry.Vector3d();

```
# 综合运用
