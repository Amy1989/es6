## 概述 ##

ES6诞生以前，异步编程的方法，大概有下面四种。

- 回调函数
- 事件监听
- 发布/订阅
- Promise 对象


Promise 对象用于异步(asynchronous ) 计算.。一个Promise对象代表着一个还未完成，但预期将来会完成的操作。

Promise 对象是一个返回值的代理，这个返回值在promise对象创建时未必已知。它允许你为异步操作的成功或失败指定处理方法。 这使得异步方法可以像同步方法那样返回值：异步方法会返回一个包含了原返回值的 promise 对象来替代原返回值。


Promise对象有以下几种状态:

- pending: 初始状态, 既不是 fulfilled 也不是 rejected.
- fulfilled: 成功的操作.
- rejected: 失败的操作.

![GitHub](https://github.com/AmyDayday/es6/blob/master/promises.png "GitHub,Social Coding")


> 基本用法

```js
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('Resolved.');
},function(){
	//失败
});

console.log('Hi!');

// Promise
// Hi!
// Resolved


```
> Promise.prototype.catch()

```js
var p1 = new Promise(function(resolve, reject) {
  resolve("成功");
});

p1.then(function(value) {
  console.log(value); // "成功!"
  throw "哦，不!";
}).catch(function(e) {
  console.log(e); // "哦，不!"
});
```

> 链式操作

```js
getArticleList().then(function(articles){
    return getArticle(articles[0].id);
}).then(function(article){
    return getAuthor(article.authorId);
}).then(function(author){
    alert(author.email);
});

//箭头函数
getArticleList()
.then(articles => getArticle(articles[0].id))
.then(article => getAuthor(article.authorId))
.then(author => {
    alert(author.email);
});


function getAuthor(id){
    return new Promise(function(resolve, reject){
        $.ajax("http://beta.json-generator.com/api/json/get/E105pDLh",{
            author: id
        }).done(function(result){
            resolve(result);
        })
    });
}

function getArticle(id){
    return new Promise(function(resolve, reject){
        $.ajax("http://beta.json-generator.com/api/json/get/EkI02vUn",{
            id: id
        }).done(function(result){
            resolve(result);
        })
    });
}

function getArticleList(){
    return new Promise(function(resolve, reject){
       $.ajax(
        "http://beta.json-generator.com/api/json/get/Ey8JqwIh")
        .done(function(result){
            resolve(result);
        }); 
    });
}
```



Promise新建后立即执行，所以首先输出的是“Promise”。然后，then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以“Resolved”最后输出。

>Promise.all()

`promise.all` 方法用于将多个Promise实例，包装成一个新的Promise实例。
    
        var p = Promise.all([p1, p2, p3]).then(function (posts) {
	      // ...
	    }).catch(function(reason){
	      // ...
	    });
	
只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。

```js
Promise.all([
    fetchPromised("http://backend/foo.txt", 500),
    fetchPromised("http://backend/bar.txt", 500),
    fetchPromised("http://backend/baz.txt", 500)
]).then((data) => {
    let [ foo, bar, baz ] = data
    console.log(`success: foo=${foo} bar=${bar} baz=${baz}`)
}, (err) => {
    console.log(`error: ${err}`)
})

es5

function fetchAll (request, onData, onError) {
    var result = [], results = 0;
    for (var i = 0; i < request.length; i++) {
        result[i] = null;
        (function (i) {
            fetchAsync(request[i].url, request[i].timeout, function (data) {
                result[i] = data;
                if (++results === request.length)
                    onData(result);
            }, onError);
        })(i);
    }
}
fetchAll([
    { url: "http://backend/foo.txt", timeout: 500 },
    { url: "http://backend/bar.txt", timeout: 500 },
    { url: "http://backend/baz.txt", timeout: 500 }
], function (data) {
    var foo = data[0], bar = data[1], baz = data[2];
    console.log("success: foo=" + foo + " bar=" + bar + " baz=" + baz);
}, function (err) {
    console.log("error: " + err);
});

	
```


和Generator结合使用，像同步的方式编写异步的代码

```js
function* run(){
  var articles = yield getArticleList();
  var article = yield getArticle(articles[0].id);
  var author = yield getAuthor(article.authorId);
  alert(author.email);  
}

var gen = run();
gen.next().value.then(function(r1){
  gen.next(r1).value.then(function(r2){
      gen.next(r2).value.then(function(r3){
        gen.next(r3);
        console.log("done");
      })
  })
});

```
es7
async/await


```js
async function run(){
  var articles = await getArticleList();
  var article = await getArticle(articles[0].id);
  var author = await getAuthor(article.authorId);
  alert(author.email);  
}

run();
```

用promise实现$.ajax
```js
var core = {

    // Method that performs the ajax request
    ajax : function (method, url, args) {

      // Creating a promise
      var promise = new Promise( function (resolve, reject) {

        // Instantiates the XMLHttpRequest
        var client = new XMLHttpRequest();
        var uri = url;

        if (args && (method === 'POST' || method === 'PUT')) {
          uri += '?';
          var argcount = 0;
          for (var key in args) {
            if (args.hasOwnProperty(key)) {
              if (argcount++) {
                uri += '&';
              }
              uri += encodeURIComponent(key) + '=' + encodeURIComponent(args[key]);
            }
          }
        }

        client.open(method, uri);
        client.send();

        client.onload = function () {
          if (this.status >= 200 && this.status < 300) {
            // Performs the function "resolve" when this.status is equal to 2xx
            resolve(this.response);
          } else {
            // Performs the function "reject" when this.status is different than 2xx
            reject(this.statusText);
          }
        };
        client.onerror = function () {
          reject(this.statusText);
        };
      });

      // Return the promise
      return promise;
    }
  };

  // Adapter pattern
  return {
    'get' : function(args) {
      return core.ajax('GET', url, args);
    },
    'post' : function(args) {
      return core.ajax('POST', url, args);
    },
    'put' : function(args) {
      return core.ajax('PUT', url, args);
    },
    'delete' : function(args) {
      return core.ajax('DELETE', url, args);
    }
  };
};
```

> 缺点

Promise也有一些缺点。首先，无法取消Promise，一旦新建它就会立即执行，无法中途取消。其次，如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。第三，当处于Pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。








