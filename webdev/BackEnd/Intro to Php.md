---
created: 28-03-2022
e: ⭐
tags: CS/javascript
---

# Intro to Php

## Php basics

- `var_dump($value)`: displays structured information about one or more expressions that includes its type and value
- `intval($value)`: the `intval()` function returns the integer value of a variable.
- `floatval($value)`: the `floatval()` function returns the float value of a variable.
- `array()`: create arrays, syntax (`array(value1, value2, value3` or `array(key=>value1, key2=>value2, key3=> value3`)
- `$my_array[] = value`: same as `array_push($my_array, value)`
- `array_splice(array, start, length)`: remove `length` elements starting at position `start`

```php
<?php  
// variables!  
$myInt = 5;  
$myFloat = 5.9;  
$myString = "hello world";  
$myBool = true;  

print $myBool;  
// 1 for true  
// 0 for false  
var_dump($myBool);  
// bool(true)  
  
print $myInt . $myString;  
// . for concatenation  
  
print '$myString is what I am doing right now';  
// standard delimiter, $myString will be print out directly
print "$myString is what I am doing right now";  
// will print "hello world"
  
// converting between types  
$a = (int) $myFloat;  
print $a;  
// 5  
$a = intval( $myFloat );  
// same as (int) $myFloat  
  
$sum = 10 + 10 + "10";  
// + only for mathematical operation print $sum;  
// 30 (with implicit datatype conversion);
 
if ($myInt > 0) {  
    print "hi";  
    } 
else if (){  } 
else {  }  
  
for ($i = 0; $i < 100; $i++){  
  print $i . "<br>\n";  
}  
  
$myArray = array(100, 200, 300, 400);  
// must use the array function
print var_dump($myArray) . '<br>';  
  
array_push( $myArray, 999, 1, 3);  
// add 999, 1, 3 at the end of the array  
var_dump($myArray);  
$myArray[] = 989;  
// append 999 at the end of the array  
  
array_splice($myArray, 2, 1);  
// remove 1 element starting at position 2  
?>
```

## Php CGI (GET and POST)

stands for *GCI: common gateway interface*

```html
<h1>PHP CGI</h1>
<!--    <form action="php_cgi.php" method="get">-->
<!--        Name: <input type="text" name="name">-->
<!--        <input type="submit">-->
<!--    </form>-->
<form action="php_cgi.php" method="post">
 Name (post): <input type="text" name="name">
 Favorite Color (post): <input type="text" name="color">
 <input type="submit">
</form>
```

### target file

```php
<?php  
// access the incoming variables through the GET stream  
  
// http://localhost:63343/BackEnd/php_cgi.php?name=Sirui  
//$name = $_GET['name'];  
$name = $_POST['name'];  
$color = $_POST['color'];  
  
if ($name){  
 print "hello " . $name . "<br>";  
 print "Your favorite color is $color";  
} else {  
 print "??????";  
}
```

## Php header

```php
<!DOCTYPE html>  
<html lang="en">  
<head>  
 <meta charset="UTF-8">  
 <title>PHP Headers</title>  
 <style>  
  <?php  
   if (@$_GET['favcolor']){  
    print "body { background-color: " . $_GET['favcolor'] . "; }";  
     }  
   ?>  
  </style>  
 </head>  
 <body>  
  <h1>PHP Headers</h1>  
  <?php  
   if (@$_GET['error']){  
    //            @ is error suppression operator  
    print"<strong>Please fill out the form!</strong>";  
   }  
  ?>  
  <form action="phpProcess.php" method="post">  
   Color: <input type="text" name="color">  
   <input type="submit">  
  </form>  
 </body>  
</html>
```

```php
<?php  
// grab the color variable from the POST variable stream  
$color = $_POST['color'];  

if ($color){  
 //    print "thanks!";  
 header('Location: php_header.php?favcolor='.$color);  
} else {  
 // if empty, direct user back to the input page  
 header('Location: php_header.php?error=empty');  
 // ? send data back  
 exit();  
}
```

## syntax

**=> vs. -> vs. ::**

**=>**
The double arrow operator is used as an access mechanism for arrays

```php
$myArray = array(
 0=>'Big',
 1=>'Small',
 2=>'Up',
 3=>'Down'
);
```

**->**
The object operator is used in object scope to access methods and properties of an object (*instance*)

```php
$obj = new MyObject();
$obj->thisProperty = 'Fred';
```

**::**
The Scope Resolution Operator allows access to static, constant, and overridden properties or methods of a class
[[php YouTube#^2c4479]]
