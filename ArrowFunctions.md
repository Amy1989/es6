## 箭头函数 ##


```js
odds  = evens.map(v => v + 1)
pairs = evens.map(v => ({ even: v, odd: v + 1 }))
nums  = evens.map((v, i) => v + i)

es5
odds  = evens.map(function (v) { return v + 1; });
pairs = evens.map(function (v) { return { even: v, odd: v + 1 }; });
nums  = evens.map(function (v, i) { return v + i; });

```

使用注意点箭头函数有几个使用注意点。
-（1）函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
-（2）不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
-（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。
-（4）不可以使用yield命令，因此箭头函数不能用作Generator函数。
 -(5) 箭头函数对上下文的绑定是强制性的，无法通过 apply 或 call 方法改变其上下文

```js
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

var id = 21;

foo.call({ id: 42 });
// id: 42

```
箭头函数会绑定上下文的特性，故不能随意在顶层作用域使用箭头函数，以防出错：

```js
// 假设当前运行环境为浏览器，故顶层作上下文为 `window`
let obj = {
  msg: 'pong',

  ping: () => {
    return this.msg // Warning!
  }
}

obj.ping() //=> undefined
let msg = 'bang!'
obj.ping() //=> bang!

//等价代码
let obj = {
  // ...
  ping: (function() {
    return this.msg // Warning!
  }).bind(this)
}
```

## 与解构赋值默认值结合使用 ##


```js
function fetch(url, { body = '', method = 'GET', headers = {} }) { 
console.log(method); 
} 
fetch('http://example.com', {}) // "GET" fetch('http://example.com') // 报错
```

```js
function fetch(url, { method = 'GET' } = {}) { 
console.log(method); 
} 
fetch('http://example.com') // "GET"
```

## 扩展运算符 ##

```js
// ES5的合并数组arr1.concat(arr2, arr3);
// [ 'a', 'b', 'c', 'd', 'e' ]

// ES6的合并数组
[...arr1, ...arr2, ...arr3]
// [ 'a', 'b', 'c', 'd', 'e' ]

const [first, ...rest] = [1, 2, 3, 4, 5];
first // 1
rest  // [2, 3, 4, 5]

const [first, ...rest] = ["foo"];
first  // "foo"
rest   //[]

var d = new Date(...dateFields); 
```
