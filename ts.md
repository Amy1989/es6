> 转换TypeScript代码为ES5代码的transpiler是由TypeScript核心团队编写，然而，转换ES6代码到ES5代码有2个主要的transpilers：Google开发的traceur
> 和JavaScript社区创建的babel,我们不打算在这本书中使用直接，但他们都是伟大的项目值得我们了解。
> 
> npm install -g  typeScript


##基础类型##
> Boolean、Number、Number、Array、Enum、Tuple、Any、Void
 ```js
let isDone: boolean = false;	
let name: string = "bob";

> number
    let decimal: number = 6;
    let hex: number = 0xf00d;
    let binary: number = 0b1010;
    let octal: number = 0o744;

> Array
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];

> Tuple
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

使用枚举我们可以定义一些有名字的数字常量 (星期)

    enum Color {Red, Green, Blue};
    var c: Color = Color.Green;

	enum Color {Red = 1, Green = 2, Blue = 4}; //可以设置索引，默认是从0开始的
	let c: Color = Color.Green;

> Any

有时我们在写程序的时候不确定一个变量是什么类型。比如是来自动态内容或是第三方库之类的。此时我们可以用:any说明符，让这个变量跳过编译时类型检查。

> Void

它代表没有任何数据类型。常用来说明没有返回值的函数的返回类型。

```js
function warnUser(): void {
    alert("This is my warning message");
}
```

> 泛型
   不定义类型，用的时候定义类型

    function fn<T>(args: T) :T{
    	return args;
    }
    
    console.log(fn<string>('123'));


##接口##
接口可以描述js任何一个类型(属性、函数、class、数组等)
通过关键字Interface创建一个接口，同时对接口进行使用。达到规范类型的目的

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


>  TypeScript 接口的函数类型，通过接口来规范函数的参数的统一性，避免参数转换问题

```js
interface Test{
    (label: string, name: string) :boolean;
}

let fn: Test;
fn = function(label, name){
    let result = label.search(name);
    if(result != -1){
        return true;
    }else{
        return false;
    }
}

console.log(fn('liming', 'li'));
```
> 
> 接口数组类型

```js

interface StringArray {
    [index: number]: string;
}

let myArray: StringArray;
myArray = ["Bob", "Fred"];

let myStr: string = myArray[0];

```

> 接口与class

```js
interface ClockInterface {
    currentTime: Date;
    setTime(d: Date);
}

class Clock implements ClockInterface {
    currentTime: Date;
    setTime(d: Date) {
        this.currentTime = d;
    }
    constructor(h: number, m: number) { }
}
```


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
注： 私有属性如果想被外界访问用setter getter

## decorator ##
若要启用实验性的decorator，你必须启用experimentalDecorators编译器选项，在命令行中或在tsconfig.json
```js
{
    "compilerOptions": {
        "target": "ES5",
        "experimentalDecorators": true
    }
}
```











