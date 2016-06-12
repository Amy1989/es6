## Set ##

类似于数组，但是成员的值都是唯一的，没有重复的值

```js
let s = new Set()
s.add("hello").add("goodbye").add("hello")
s.size===2
s.has("hello")===true
s   //Set{'hello', 'goodbye '}
for(let key of s.values())// insertion orderconsole.log(key)


for (let item of set.entries()) {
  console.log(item);
}
// ["red", "red"]// ["green", "green"]// ["blue", "blue"]

```

## Map ##

它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键

```js
let m=new Map();
m.set("hello", 42); // Map { 'hello' => 42, 12 => 34 }

m.set(s, 34);
m.get(s)===34;
m.size===2;
for(let[ key, val ] of m.entries())console.log(key+" = "+val);


```

```js
var map = new Map();

var k1 = ['a'];
var k2 = ['a'];

map
.set(k1, 111)
.set(k2, 222);

map.get(k1) // 111map.get(k2) // 222
```

由上可知，Map的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键。这就解决了同名属性碰撞（clash）的问题，我们扩展别人的库的时候，如果使用对象作为键名，就不用担心自己的属性与原作者的属性同名。

如果Map的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map将其视为一个键，包括0和-0。另外，虽然NaN不严格相等于自身，但Map将其视为同一个键。
