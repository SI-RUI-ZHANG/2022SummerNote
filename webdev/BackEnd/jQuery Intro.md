---
created: 15-04-2022
tags: CS, jQuery
---

# jQuery Intro

## jQuery basic syntax

### Include in jQuery

```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js"
 integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4="
 crossorigin="anonymous">
</script>
```

### edit css

```js
 $('#foo').css('background-color','red')
```

### select all

```js
let allP = document.querySelectorAll('p')
for (let paragraph of allP){
 paragraph.style.backgroundColor = 'grey'
}
```

is equivalent to

```js
$('p').css('background-color', 'blue')
```

### set/get attribute

```js
$('img').attr('src', 'head2.png')
let temp = $('img').attr('src')
```

### change inner value

```js
$('#foo').html('<h1>Hello world!</h1>')
```

### document.ready

go when document is fully loaded

```js
$(document).ready(function(){ 
 setTimeout(()=>{
  prompt("test")
 }, 1000)
})
```

### edit class

```js
$('p').addClass('pikachu')
let foo = $('#foo')
if (foo.hasClass('pikachu')){
 foo.removeClass('pikachu')
}
```

### event listener

```js
$('#foo').click(function(){
 // event is the vanilla javascript event
 // $(this) is the jQuery $('#foo')
})

$('p').click(function(){
 $(this).css('background-color', 'blue')
})
```

### add state

```js
$('p').hover (
 // when hover
 function (event){
  $(this).css('color','yellow')
 },
 // when leave
 function (event){
  $(this).css('color','white')
 }
)
```

## AJAX

```js
// the long way to do
document.getElementById('click').onclick = function (){
    //step 1. create xmlHttp object
    let xmlHttp = new XMLHttpRequest()
    //step 2. have this object listen for various state changes

    // 1: request not initialized
    // 2: request received
    // 3: processing request
    // 4: request finished and response is ready
    xmlHttp.onreadystatechange = function (){
    console.log(this.readyState)
    if (this.readyState === 4 && this.status === 200){
        console.log("Get data")
        console.log(this.responseText)
        document.getElementById('output').innerText = this.responseText
    }
 }

 //step 3. initiate a request
 xmlHttp.open("GET", "test.txt")

 xmlHttp.send()

}
```

### using jQuery

#### helloWorld.php

```php
<?php
    print "Hello world! From PHP!";
    print rand(1,1000);
?>
```

#### jQuery.php

This file only get data from request

```php
<body>
    <h1>AJAX</h1>
    <button id="click"> click me </button>
    <div id="output"></div>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js" 
        integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4=" 
        crossorigin="anonymous">
    </script>

    <script>
    $(document).ready(function (){
        // reference to our output div
        let output = document.getElementById('output')

        document.getElementById('click').addEventListener('click', ()=>{
            // ask jQuery to make an AJAX request
            $.ajax({
                type: 'GET',
                url: 'helloWorld.php',
                // variables that send to url
                data: {},
                // run when server respond
                success: function (data, status){
                    output.innerHTML += data + "<br>";
                },
                error: function (request, data, status){
                    output.innerHTML += 'Error occurred!' + "<br>"
                }
            })
        })
    })
    </script>
</body>
```

:**send data through request**

#### getData.php

```php
<?php
    $num = @$_GET['num'];
    if ($num) print $num * 10;
    else print "missingData";
?>

```

#### jQuery.php

```html

<h1>AJAX</h1>
Number: <input type="text" id="num">
<button id="click">
    click me
</button>

<div id="output">
</div>


<script src="https://code.jquery.com/jquery-3.6.0.min.js" 
    integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4=" 
    crossorigin="anonymous">
</script>
<script>
    $(document).ready(function (){
        // reference to our output div
        let output = document.getElementById('output')

        document.getElementById('click').addEventListener('click', ()=>{
            // ask jQuery to make an AJAX request
            let numFromUser = document.getElementById('num').value;
            $.ajax({
                type: 'GET',
                url: 'getData.php',
                // variables that send to url
                data: {
                    num: numFromUser
                },

                // run when server respond
                success: function (data, status){
                    if (data === "missingData"){
                        alert("Fill in the form!")
                    } else {
                        output.innerHTML += data + "<br>";
                    }
                },
                error: function (request, data, status){
                    output.innerHTML += 'Error occurred!' + "<br>"
                }
            })
        })
    })
</script>
```
