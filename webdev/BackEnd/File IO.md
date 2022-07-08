
# File IO

## fileIOConfig.php

```php
<?php  
// store it in a file for later use  
$path = '/Users/zhangsirui/PhpstormProjects/test/data';  
// set up the filename of the destination file to store the 
//username  
$filename = $path . '/username.txt';
```

## fileIO.php

```php
<!DOCTYPE html>  
<html lang="en">  
<head>  
<meta charset="UTF-8">  
<title>Title</title>  
</head>  
<body>  
    <h1>PHP File I/O</h1>  
    <form method="post" action="saveform.php">  
        Name: <input type="text" name="username">  
        <input type="submit">  
    </form>  
</body>  
</html>
```

## saveForm.php

```php
<?php  
// bring all variables and code from config.php  
include ('fileIOConfig.php');  
/**  
 * @var $filename  
 */  
// grad the incoming username  
$username = $_POST['username'];  
// put the data into the file  
file_put_contents($filename, $username."\n", FILE_APPEND);  
// tell the user we are done!  
print "all done!";
```

## getData.php

```php
<?php  
// open the username.txt file and grab all the data  
include ('fileIOConfig.php');  
/**  
 * @var $filename  
 */  
// open the usernames.txt file and grab all the data  
$allData = trim(file_get_contents($filename));  
// cut apart all the usernames  
$allName = explode("\n", $allData);  
print "<ul>";  
for ($i = 0; $i < sizeof($allName); $i++ ){  
 print "<li>" . $allName[$i] . "</li>\n";  
}  
print "</ul>";  
  
// show the data to the user
```

# php Cookies

## cookies.php

```html
<!DOCTYPE html>  
<html lang="en">  
<head>  
<meta charset="UTF-8">  
<title>Title</title>  
</head>  
<body>  
   <form method="post" action="doSomthing.php">  
    	<input type="submit">  
   </form>  
</body>  
</html>
```

## doSomething.php

```php
<?php  
// extract POST variables  
// $x = $_POST['foobar'];  
// $y = $_GET['foobar'];  

// reading a cookie with php  
$name = $_COOKIE['name'];  
  
// set a cookie with php  
setcookie('power', 'electricity');  
  
// delete a cookie  
// setcookie('power', '');  
// set expire time of cookiesetcookie('power', '', time()-3600);  
// the cookie should expire ??? time ago  
  
print "hello world<br>";
```

## tester.php

```php
<?php  
// get the name of our pokemon  
@$name = $_COOKIE['name'];  
  
if ($name) {  
 print $name;  
} else {  
 print "???";  
}
```
