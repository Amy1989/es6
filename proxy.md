## proxy ##

Proxy 对象用来为基础操作（例如：属性查找、赋值、枚举、方法调用等）定义用户自定义行为

> var p = new Proxy(target, handler);

target
被代理虚拟化的对象，这个对象常常用作代理的存储后端。关于对象不可拓展性和不可修改属性的不变量会被代理拦截。

代理和目标对象的关系：
 代理的行为很简单：将代理的所有内部方法转发至目标。简单来说，如果调用proxy.[[Enumerate]]() ，
 就会返回target.[[Enumerate]]()， 

 如果代理的目标是一个DOM元素，相应的代理就不是
 target: div#item-1
 p: Object {}

```js
var handler = {
    get: function(target, name){
        return name in target?
            target[name] :
            37;
    }
};

var p = new Proxy({}, handler);
p.a = 1;
p.b = undefined;

console.log(p.a, p.b); // 1, undefined
console.log('c' in p, p.c); // false, 37
```

**句柄对象的方法可以覆写任意代理的内部方法。**
```js
var target = {};
var handler = {
set: function (target, key, value, receiver) {
throw new Error("请不要为这个对象设置属性。");
}
};
var proxy = new Proxy(target, handler);
> proxy.name = "angelina";
Error: 请不要为这个对象设置属性。
```

```js
function Tree() {
return new Proxy({}, handler);
}
var handler = {
get: function (target, key, receiver) {
if (!(key in target)) {
target[key] = Tree(); // 自动创建一个子树
}
return Reflect.get(target, key, receiver);
}
};

> var tree = Tree();
> tree
{ }
> tree.branch1.branch2.twig = "green";
> tree
{ branch1: { branch2: { twig: "green" } } }
> tree.branch1.branch3.twig = "yellow";
{ branch1: { branch2: { twig: "green" },
branch3: { twig: "yellow" }}}

```

Reflect 对象提供了若干个能对任意对象进行某种特定的可拦截操作（interceptable operation）的方法。

Reflect.get()
获取对象身上某个属性的值，类似于 target[name]。
