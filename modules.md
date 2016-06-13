## Module ##

Module解决模块化问题

ES6模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS和AMD模块，都只能在运行时确定这些东西。比如，CommonJS模块就是对象，输入时必须查找对象属性。

```js

// CommonJS模块
let { stat, exists, readFile } = require('fs');

// 等同于
let _fs = require('fs');
let stat = _fs.stat, exists = _fs.exists, readfile = _fs.readfile;

其他引入方式
import name from "module-name"
import * as name from "module-name"
import { member } from "module-name"
import { member as alias } from "module-name"
import { member1 , member2 } from "module-name"
import { member1 , member2 as alias2 , [...] } from "module-name"
import defaultMember, { member [ , [...] ] } from "module-name"
import defaultMember, * as alias from "module-name"
import defaultMember from "module-name"
import "module-name"

```

ES6模块不是对象，而是通过export命令显式指定输出的代码，输入时也采用静态命令的形式。

```js
// ES6模块

import { stat, exists, readFile } from 'fs';
```
上面代码的实质是从fs模块加载3个方法，其他方法不加载。这种加载称为“编译时加载”，即ES6可以在编译时就完成模块加载，效率要比CommonJS模块的加载方式高。当然，这也导致了没法引用ES6模块本身，因为它不是对象。

> export命令

一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量。

```js
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;


另一种写法
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export {firstName, lastName, year};
```


```js
// 报错
export 1;

// 报错
var m = 1;
export m;

// 写法一
export var m = 1;

// 写法二
var m = 1;
export {m};

// 写法三
var n = 1;
export {n as m};

// 报错
function f() {}
export f;

// 正确
export function f() {};

// 正确
function f() {}
export {f};


```


>import命令

注意，import命令具有提升效果，会提升到整个模块的头部，首先执行。
	
	foo();
	
	import { foo } from 'my_module'; //不会报错

> 
> 模块的整体加载


```js
export function area(radius) {
  return Math.PI * radius * radius;
}

export function circumference(radius) {
  return 2 * Math.PI * radius;
}

import { area, circumference } from './circle';

console.log('圆面积：' + area(4));
console.log('圆周长：' + circumference(14));

import * as circle from './circle';

console.log('圆面积：' + circle.area(4));
console.log('圆周长：' + circle.circumference(14));

```

> 
> export default命令


```js
// 输出
export default function crc32() {
  // ...
}
// 输入
import crc32 from 'crc32';

// 输出
export function crc32() {
  // ...
};
// 输入
import {crc32} from 'crc32';
```

第一组是使用export default时，对应的import语句不需要使用大括号；第二组是不使用export default时，对应的import语句需要使用大括号。
export default就是输出一个叫做default的变量或方法，然后系统允许你为它取任意名字


正是因为export default命令其实只是输出一个叫做default的变量，所以它后面不能跟变量声明语句。


```js
// 正确
export var a = 1;

// 正确
var a = 1;
export default a;

// 错误
export default var a = 1;
```

> 
> ES6模块加载的实质

ES6模块加载的机制，与CommonJS模块完全不同。CommonJS模块输出的是一个值的拷贝，而ES6模块输出的是值的引用。

```js
commonjs

var counter = 3;
function incCounter() {
  counter++;
}
module.exports = {
  counter: counter,
  incCounter: incCounter,
};

// main.js
var mod = require('./lib');

console.log(mod.counter);  // 3
mod.incCounter();
console.log(mod.counter); // 3

es6
// lib.js
export let counter = 3;
export function incCounter() {
  counter++;
}

// main.js
import { counter, incCounter } from './lib';
console.log(counter); // 3
incCounter();
console.log(counter); // 4
```
