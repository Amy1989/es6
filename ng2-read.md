## Angular2的依赖 ##

Angular 2依赖于这四个库：
- 
- es6-shim (为了旧浏览器)
- angular2-polyfills
- SystemJS
- RxJS

**ES6 Shim**
	
ES Shim 为旧版的Javascript引擎提供了ECMAScript 6的行为，该Shim对于较新新版本的Safari,Chrome等并不严格需要，但是对于旧版本的IE是需要的。

**Angular 2 Polyfill**

像ES6 Shim, angular2-polyfills提供跨浏览器的一些基本的标准化。

angular2-polyfills包含的代码专门用于zone,promise和reflection


**SystemJS**

SystemJS是一个模块加载器。它帮助我们创建模块和解决模块之间依赖，模块加载在浏览器端的JavaScript是出奇的复杂，SystemJS使得过程变得更加容易。(类似于webpack)

**RxJS**

RxJS是一个库用于在Javascript中进行反应式编程，一般来说,RxJS给了我们使用Observables的工具，用于发出的数据流。Angular 在许多地方使用了Observables，如在处理异步代码(例如: HTTP请求)





