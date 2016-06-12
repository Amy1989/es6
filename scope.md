## 块级作用域 ##

    for(let i=0; i<5; i++){}
    console.log(i) // 报错
es5

	(function(){
	for(var i=0; i<5; i++){}
	})
	console.log(i) // 报错


