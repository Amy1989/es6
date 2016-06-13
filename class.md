
## 类声明 ##

```js
class Shape {
    constructor (id, x, y) {
        this.id = id
        this.move(x, y)
    }
    move (x, y) {
        this.x = x
        this.y = y
    }
}

var Shape = function (id, x, y) {
    this.id = id;
    this.move(x, y);
};
Shape.prototype.move = function (x, y) {
    this.x = x;
    this.y = y;
};

```
#####construcor

class 根据 constructor 方法来创建和初始化对象。

一个 class 中只能有一个指定的 ”constructor“ （构造）方法。如果 class 定义的时候包含多个构造方法，程序将会抛出 SyntaxError 错误。

在构造方法中可以使用 super 关键字来调用父类的构造方法。



#####变量提升

类声明和函数声明不同的一点是，函数声明存在变量提升现象，而类声明不会。也就是说，你必须先声明类，然后才能使用它，否则代码会抛出 ReferenceError 异常

      var p = new Polygon(); // ReferenceError `
      class Polygon {}
    
#####静态方法

static 关键字用来定义类的静态方法。 静态方法是指那些不需要对类进行实例化，使用类名就可以直接访问的方法。
静态方法经常用来作为工具函数。
```js
class Point {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }

    static distance(a, b) {
        const dx = a.x - b.x;
        const dy = a.y - b.y;

        return Math.sqrt(dx*dx + dy*dy);
    }
}

const p1 = new Point(5, 5);
const p2 = new Point(10, 10);
p1.distance()//会报错 不会被实例继承， 可以被子类继承
console.log(Point.distance(p1, p2));

es5 
var fn = function(){
}

fn.test = function(){
	console.log(2)
};

```
不能直接地定义静态成员变量，但若必须实现此类需求，可以用static 加上 get 语句和 set 语句实现
    class SyncObject {
      // ...
    
      static get baseUrl() {
    	return 'http://example.com/api/sync'
      }
    }
#####继承

```js

class Shape{
	construcotr(id, x, y){
		this.id = id;
		this.x = x;
		this.y = y;
	}
}
class Circle extends Shape {
    constructor (id, x, y, radius) {
        super(id, x, y) //this必须在super之后写，否则会报错
        this.radius = radius
    }
}

es5

var Rectangle = function (id, x, y, width, height) {
    Shape.call(this, id, x, y);
    this.width  = width;
    this.height = height;
};
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;
var Circle = function (id, x, y, radius) {
    Shape.call(this, id, x, y);
    this.radius = radius;
};
Circle.prototype = Object.create(Shape.prototype);
Circle.prototype.constructor = Circle;

```

#####setter和getter

在Class内部可以使用get和set关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为

```js
class MyClass {
  constructor() {
    // ...
  }
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

console.log(inst.prop)// 'getter

```

ES2015 中对类的定义依然不支持默认属性的语法,而在 TypeScript 中则有良好的实现。
    
    // 理想型
    class Person {
      name: String
      gender = 'man'
      // ...
    }
## 支持 __proto__ 注入 ##

```js
class Foo {
  constructor() {
    this.pingMsg = 'pong'
  }

  ping() {
    console.log(this.pingMsg)
  }
}

let o = {
  __proto__: new Foo()
}

o.ping() //=> pong

//有一个比较特殊的场景会需要用到：想扩展或者覆盖一个类的方法，并生成一个实例，但觉得另外定义一个类就感觉浪费了
let o = {
  __proto__: new Foo(),

  constructor() {
    this.pingMsg = 'alive'
  },

  msg: 'bang',
  yell() {
    console.log(this.msg)
  }
}

o.yell() //=> bang
o.ping() //=> alive

```
- 
- 缺点：
- 
- 不支持私有属性（private）
- 不支持前置属性定义，但可用 get 语句和 set 语句实现
- 不支持多重继承
- 没有类似于协议（Protocl）或接口（Interface）等的概念


## ts ##

当成员被标记成private时，它就不能在声明它的类的外部访问,默认是public
protected修饰符与private修饰符的行为很相似，但有一点不同，protected成员在派生类中仍然可以访问
```js
class Animal {
	public age: number;
    private name: string;
    constructor(theName: string) { this.name = theName; }
}

new Animal("Cat").name; // Error: 'name' is private;

```

