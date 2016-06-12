
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







