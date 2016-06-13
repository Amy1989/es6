> 转换TypeScript代码为ES5代码的transpiler是由TypeScript核心团队编写，然而，转换ES6代码到ES5代码有2个主要的transpilers：Google开发的traceur
> 和JavaScript社区创建的babel,我们不打算在这本书中使用直接，但他们都是伟大的项目值得我们了解。
> 
> npm install -g  typeScript
##基础类型##

 ```js
let isDone: boolean = false;	
let decLiteral: number = 6;
let name: string = "bob";
数组
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];

数组中的类型可以不一样

// Declare a tuple type
let x: [string, number];
// Initialize it
x = ['hello', 10]; // OK
// Initialize it incorrectly
x = [10, 'hello']; // Error

```js
> 
> 枚举 

使用枚举我们可以定义一些有名字的数字常量

    enum Color {Red, Green, Blue};
    var c: Color = Color.Green;



> Any

有时我们在写程序的时候不确定一个变量是什么类型。比如是来自动态内容或是第三方库之类的。此时我们可以用:any说明符，让这个变量跳过编译时类型检查。

> Void

它代表没有任何数据类型。常用来说明没有返回值的函数的返回类型。

```js
function warnUser(): void {
    alert("This is my warning message");
}
```
##接口##

```js
interface LabelledValue {
  label: string;
  width?: number;
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```

LabelledValue接口就好比一个名字，用来描述上面例子里的要求。 它代表了有一个label属性且类型为string的对象。 需要注意的是，我们在这里并不能像在其它语言里一样，说传给printLabel的对象实现了这个接口。我们只会去关注值的外形。 只要传入的对象满足上面提到的必要条件，那么它就是被允许的。

可选属性的好处之一是可以对可能存在的属性进行预定义，好处之二是可以捕获引用了不存在的属性时的错误。 比如，我们故意将printLabel里的width属性名拼错，就会得到一个错误提示


## **类** ##

```js
class Person{
    first_name:string;
    last_name: string;
    age:number;
    greet(){
        console.log("Hello",this.first_name) 
    }
    ageInYears(years: number): number {
        return this.age + years;
    }
}
// instantiate a new Person instance
var p = new Person();
// set initial age
p.age=6;
//how old will he be in 12 years?
p.ageInYears(12);

```

**构造函数**

构造函数是在创建类的新实例时执行的特殊方法。通常，在这里构造函数是为新对象执行初始设置的地方。

构造函数的方法名必须被命名为constructor。他们可以有参数，但他们不能返回任何值。

一个类也可以没有明确定义的构造函数：
    
    class Vehicle {}
    var v = new Vehicle();

同等于
	class Vehicle {
	    constructor(){}
	}
	var v = new Vehicle();


> 在TypeScript 每一个类只能有一个constructor


```js
class Person {
  first_name: string;
  last_name: string;
  age: number;
  constructor(first_name: string, last_name: string, age: number) {
    this.first_name = first_name;
    this.last_name = last_name;
    this.age = age;
  }
  greet() {
    console.log("Hello", this.first_name);
  }
  ageInYears(years: number): number {
        return this.age + years;
  }
}
```

属性和方法默认是公有的，可以用public修饰

当成员被标记成private时，它就不能在声明它的类的外部访问

```js
class Animal {
    private name: string;
    constructor(theName: string) { this.name = theName; }
}

new Animal("Cat").name; // Error: 'name' is private;
```









