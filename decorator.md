## 修饰器 ##

修饰器（Decorator）(也可叫装饰器) 是一个函数，用来修改类的行为。这是ES7的一个提案，目前Babel转码器已经支持。

修饰器对类的行为的改变，是代码编译时发生的，而不是在运行时。这意味着，修饰器能在编译阶段运行代码


```js
function testable(target) {
  target.isTestable = true;
}

@testable
class MyTestableClass {}

console.log(MyTestableClass.isTestable) // true

```

testable函数的参数`target`，就是会被修饰的类。

如果觉得一个参数不够用，可以在修饰器外面再封装一层函数。

```js
function testable(isTestable) {
  return function(target) {
    target.isTestable = isTestable;
  }
}

@testable(true)
class MyTestableClass {}
MyTestableClass.isTestable // true

@testable(false)
class MyClass {}
MyClass.isTestable // false



import { Component } from '@angular/core';
@Component({
  selector: 'my-app',

  template: `
    <h1>{{title}}</h1>
    <router-outlet></router-outlet>
  `,
  styleUrls: ['app/app.component.css'],
  providers: [
    ROUTER_PROVIDERS,
    HeroService,
  ]
})

export class AppComponent {
 
```


修饰器只能用于类和类的方法，不能用于函数，因为存在函数提升。

```js
var counter = 0;

var add = function () {
  counter++;
};

@add
function foo() {
}


var counter;
var add;

@add
function foo() {
}

counter = 0;

add = function () {
  counter++;
};


```
上面的代码，意图是执行后counter等于1，但是实际上结果是counter等于0。因为函数提升，使得实际执行的代码是下面这样。


