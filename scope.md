## 块级作用域 ##

    for(let i=0; i<5; i++){}
    console.log(i) // 报错
es5

	(function(){
	    for(var i=0; i<5; i++){}
	})
	console.log(i) // 报错

```js
<button>一</button>
<button>二</button>
<button>三</button>
<button>四</button>

<div id="output"></div>

<script>
  var buttons = document.querySelectorAll('button')
  var output = document.querySelector('#output')

  for (var i = 0; i < buttons.length; i++) {
    buttons[i].addEventListener('click', function() {
      output.innerText = buttons[i].innerText //报错，这时的i是4
    })
  }
</script>

//es5
for (var i = 0; i < buttons.length; i++) {
  	(function(i){
  		buttons[i].addEventListener('click', function() {
  		  output.innerText = buttons[i].innerText
  		})
  	}(i))
  }
```


