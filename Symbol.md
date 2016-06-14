## Symbol ##

ES6引入了一种新的原始数据类型Symbol，表示独一无二的值。它是JavaScript语言的第七种数据类型，前六种是：Undefined、Null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

    Symbol("foo") !== Symbol("foo")
    
    const foo=Symbol()
    const bar=Symbol()
    typeof foo==="symbol"
    typeof bar==="symbol"
    
    let obj = {}
    obj[foo]="foo"
    obj[bar]="bar"
    
    obj // {}
    JSON.stringify(obj)// {}
    Object.keys(obj)// []
    Object.getOwnPropertyNames(obj)// []
    Object.getOwnPropertySymbols(obj)// [ foo, bar ]
	Reflect.ownKeys(obj);
    
    const bar = Symbol.for("app.bar")
    Symbol.keyFor(bar)==="app.bar"  [true]



注意，Symbol函数前不能使用new命令，否则会报错。这是因为生成的Symbol是一个原始类型的值，不是对象。也就是说，由于Symbol值不是对象，所以不能添加属性。基本上，它是一种类似于字符串的数据类型。



注意，Symbol值作为对象属性名时，不能用点运算符。 因为点运算符后面总是字符串

```js
var mySymbol = Symbol();
var a = {};

a.mySymbol = 'Hello!';
a[mySymbol] // undefined
a['mySymbol'] // "Hello!"

```

在对象的内部，使用Symbol值定义属性时，Symbol值必须放在方括号之中。

```js
let s = Symbol();

let obj = {
  [s]: function (arg) { ... }
};

obj[s](123)
```
如果s不放在方括号中，该属性的键名就是字符串s，而不是s所代表的那个Symbol值
Symbol值作为属性名时，该属性还是公开属性，不是私有属性
> 
> Symbol.for()


Symbol.for方法可以做到这一点。它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的Symbol值。如果有，就返回这个Symbol值，否则就新建并返回一个以该字符串为名称的Symbol值

    
    var s1 = Symbol.for('foo');
    var s2 = Symbol.for('foo');
    
    s1 === s2 // true

Symbol.for 这种方式会访问symbol注册表，其中存储了已经存在的一系列symbol。这
种方式与通过Symbol() 定义的独立symbol不同，symbol注册表中的symbol是共享的。如果你连续
三十次调用Symbol.for("cat") ，每次都会返回相同的symbol。注册表非常有用，在多个web页面或
同一个web页面的多个模块中经常需要共享一个symbol




    
