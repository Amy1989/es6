## destructuring 变量的解构赋值 ##

从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）

```js
varlist=[1,2,3];
var[ a, , b ] = list;
[b, a]=[a, b];

```
如果解构不成功，变量的值就等于undefined。
如果等号的右边不是数组（或者严格地说，不是可遍历的结构），那么将会报错

```js
let [x, y] = [1, 2, 3]; //不完全解构
x // 1
y // 2
```

```js
var { op, lhs, rhs } = getASTNode()


es5 
var tmp = getASTNode();
var op  = tmp.op;
var lhs = tmp.lhs;
var rhs = tmp.rhs;


var list = [ 7, 42 ]
var [ a = 1, b = 2, c = 3, d ] = list
a === 7
b === 42
c === 3
d === undefined


```

函数参数传参

```js
function foo(name, {age= 10, sex= 'gril'}){
	console.log(name)
	console.log(age)
}

foo('liming', {age: 20});
```

...rest

```js
function foo(...rest){//(name,...rest)到在后面
	console.log(arguments) //{ '0': 'liming', '1': 18 }
	console.log([].slice.apply(arguments)) 
	console.log([...rest]) //[ 'liming', 18 ]
}

foo('liming', 18);

```