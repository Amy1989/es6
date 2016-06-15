	对象字面量方式 新的
    obj = {
    foo (a, b) {
    …
    },
    bar (x, y) {
    …
    },
    *quux (x, y) {
    …
    }
    }
	
	es5
	obj = {
    foo: function (a, b) {
        …
    },
    bar: function (x, y) {
        …
    },
    //  quux: no equivalent in ES5
    …
	};


常用二

	    let obj = {
    	foo: "bar",
    	[ "baz" + quux() ]: 42
    	}
		var obj = {
		    foo: "bar"
		};
		obj[ "baz" + quux() ] = 42;


## Object ##
Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

Object.is() 
ES6提出“Same-value equality”（同值相等）算法，用来解决这个问题。Object.is就是部署这个算法的新方法。它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。

## 属性的遍历 ##
ES6一共有5种方法可以遍历对象的属性。

（1）for...in

for...in循环遍历对象自身的和继承的可枚举属性（不含Symbol属性）。

（2）Object.keys(obj)

Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含Symbol属性）。

（3）Object.getOwnPropertyNames(obj)

Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含Symbol属性，但是包括不可枚举属性）。

（4）Object.getOwnPropertySymbols(obj)

Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有Symbol属性。

（5）Reflect.ownKeys(obj)

Reflect.ownKeys返回一个数组，包含对象自身的所有属性，不管是属性名是Symbol或字符串，也不管是否可枚举。
ES5有三个操作会忽略enumerable为false的属性。

以上的5种方法遍历对象的属性，都遵守同样的属性遍历的次序规则。
- 
- 首先遍历所有属性名为数值的属性，按照数字排序。
- 其次遍历所有属性名为字符串的属性，按照生成时间排序。
- 最后遍历所有属性名为Symbol值的属性，按照生成时间排序。



for...in循环：只遍历对象自身的和继承的可枚举的属性
Object.keys()：返回对象自身的所有可枚举的属性的键名
JSON.stringify()：只串行化对象自身的可枚举的属性

> object 支持 __proto__ 注入

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

##Aarray##

Array.from()
Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）。

Array.of()
Array.of方法用于将一组值，转换为数组。

数组实例的find()和findIndex()
数组实例的find方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。如果没有符合条件的成员，则返回undefined。


