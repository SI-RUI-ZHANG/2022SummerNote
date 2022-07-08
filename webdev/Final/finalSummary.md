# webdev final summary

## Introduction to server-side web development

`ssh`: stands for Secure Shell, is a network communication protocol that enables two computer to communicate.

access through secure shell:

```bash
ssh -l sz3047 i6.cims.nyu.edu
# access i6 server
# password: <2Xr5!qb
```

<img src="images/8d46a2b707193d0e3de396228b8fe9d4e5a4baa208e2551a84520e14d90c4b33.png" width="660px" style="display: block; margin: auto">

- useful commands:
  - `ls`: list all the files and directories
  - `ls -l`: give more info about the files and directories
  - `pwd`: list current working directory
  - `cd`: go to directory; if you are missing, type `cd` with empty argument will teleport you back to your home directory
  - `cd ..`: go up a folder
  - `nano hello.html` : create a file hello.html, you can use `vim` instead

### Accessibility

<img src="images/700362cde639d7a668c4fd0551c461e55c3bb5ab91410d61b2d78934541300a3.png" width="650px" style="display: block; margin: auto">

```bash
  rw-   r--  r--
# Owner Group World
# rwx   rwx   rwx
# r = read
# w = write
# x = execute
```

### Accessibility code

| value | code | meaning |
| ----- | ---- | ------- |
| 0     | 000  | `---`   |
| 1     | 001  | `--x`   |
| 2     | 010  | `-w-`   |
| 3     | 011  | `-wx`   |
| 4     | 100  | `r--`   |
| 5     | 101  | `r-x`   |
| 6     | 110  | `rw-`   |
| 7     | 111  | `rwx`   |

### change accessibility

`chmod`: change modification
`chmod 'value' filename`: change file with name 'filename' accessibility to 'value-meaning'

example:

```bash
chmod 700 index.html 
# change index.html to rwx --- ---
```

## PHP Fundamentals

### PHP basics

- `count()`: return number of elements in a array
- `var_dump($value)`: displays structured information about one or more expressions that includes its type and value
- `intval($value)`: returns the integer value
- `floatval($value)`: returns the float value
- `strval($value)`:  returns the float value
- `array()`: create arrays
  - `array(value1, value2, value3`
  - `array(key=>value1, key2=>value2, key3=> value3)`
- `$my_array[] = value`
  - same as `array_push($my_array, value)`
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

### PHP CGI

#### rul structure

consider the following url: `http://localhost:63342/webdevFinal/PHP%20Fundamentals/php_cgi.php`
to: `http://localhost:63342/webdevFinal/PHP%20Fundamentals/php_cgi.php?name=picachu`
`?`: followed by `name=value` pairs sent url, can be accessed by `$_GET['name']`

#### GET stream

_php_cgi.php_:

```php
<?php
    // access the incoming variables through the GET stream
    $name = $_GET['name'];
    print $name;
?>
```

#### POST stream

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

_target file_: php_cgi.php

```php
<?php  
// access the incoming variables through the GET stream  
// `http://localhost:63342/webdevFinal/PHP%20Fundamentals/php_cgi.php?name=picachu`
//$name = $_GET['name'];  
$name = $_POST['name'];  
$color = $_POST['color'];  
  
if ($name){  
 print "hello " . $name . "<br>";  
 print "Your favorite color is $color";  
} else {  
 print "please fill in your name";
}
```

### Php header

- `header("location: $url")`: send a raw HTTP header; change url to `$url`

_php\_header.php_: ask user provide `favcolor`

```php+HTML
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
    // @ is error suppression operator  
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

_phpProcess.php_: process data sent by user

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

### syntax

**=> vs. -> vs. ::**

**=>**
The double arrow operator is used as an access mechanism for arrays

```php
$myArray = array(
 0=>'Big', 1=>'Small',
 2=>'Up', 3=>'Down'
);
```

**->**
The object operator is used in object scope to access methods and properties of an object (_instance_)

```php
$obj = new MyObject();
$obj->thisProperty = 'Fred';
```

**::**
The Scope Resolution Operator allows access to static, constant, and overridden properties or methods of a class

## File I/O

- `file_put_contents($filename, $data, flags=0)`:
  - `$filename`: string; path to the file where to write the data
  - `$data`: mixed type; data to write into file
  - `$flags`: by default clear the file content
    - `$flags = FILE_APPEND`: when pass `FILE_APPEND` to `$flags`, append data to end of the file
- `file_get_content($filename)`: read the contents of a file into a string.
- `trim()`: strip whitespace (or other characters) from the beginning and end of a string
  - `" ";\n;\r;\t;\v;\0`: ordinary space; new line; carriage return; tab; vertical tab; null type
- `explode($separator, $string)`: returns and array of strings, each of which is a substring of `string` formed by splitting it on boundaries formed by the string `separator`

don't forget to use `FILE_APPEND` when appending data to file

### fileIOConfig.php

```php
<?php
$path = getcwd() . "/dataFolder" ;
$filename = $path . "/data.txt";
?>
```

### saveForm.php

```php
<?php  
// bring all variables and code from config.php  
include ('fileIOConfig.php');  
/**  
 * @var string $filename  
 */  
// grad the incoming username  
$username = $_POST['username'];  
// put the data into the file  
file_put_contents($filename, $username."\n", FILE_APPEND);  
// tell the user we are done!  
print "all done!";
```

### getData.php

```php
<?php  
// open the username.txt file and grab all the data  
include ('fileIOConfig.php');  
/**  
 * @var string $filename  
 */  
// open the usernames.txt file and grab all the data  
$allData = trim(file_get_contents($filename));  
// cut apart all the usernames  
$allName = explode("\n", $allData);  
print "<ul>";  
for ($i = 0; $i < sizeof($allName); $i++ ){  
  // show the data to the user
   print "<li>" . $allName[$i] . "</li>\n";  
}  
print "</ul>";  
?>
```

### some extra stuff

`$_SERVER['HTTP_USER_AGENT']`: grab the type of browser the user is using
`$_SERVER['REMOTE_ADDR']`: grab the user's IP address

---

### recall javascript cookies

```javascript
// set cookie
document.cookie = 'pokemon=whatever';
document.write( document.cookie );
// get value from cookie
let split = document.cookie.split("; ");
for (let i = 0; i < split.length; i++>){
  let split3 = split[i].split("=");
  console.log(split2);
}
```

---

## PHP Cookies

`setcookie($name, $value)`: defines a cookie to be sent along with the rest of the HTTP headers
`$_COOKIE['name']`: get cookie value with name `name`

to **destroy** a cookie:

```php
// Set the expiration date to one hour ago
setcookie("name", "", time()-3600);
```

```php
if($_COOKIE["name"]) {
  print "hello $_COOKIE['name']";
}
```

### a practical example: password protection

#### login.php

```php+HTML
<html>
...
<body>
    <h1>Password Protection</h1>
    <?php
        // look for a GET variable to see if there's an error
        if (@$_GET['login'] == 'failed') {
            ?> <div class="error">Login failed!</div> <?php
        }

        if (@$_COOKIE['loggedIn'] == 'yes') {
            ?> <div class="success">Logged in!</div> <?php
        }
    ?>
    <form action="validate.php" method="post">
        Username: <input type="text" name="username"><br>
        Password: <input type="text" name="password"><br>
        <input type="submit">
    </form>
</body>
</html>
```

#### validate.php

```php
<?php
    // grab the username, password
    $username = $_POST['username'];
    $password = $_POST['password'];

    // check the username & password
    if ($username == 'a' && $password == 'b') {
        setcookie('loggedIn', 'yes');
        // redirect back to the main page
        header("Location: login.php");
    } else {
        setcookie('loggedIn', '', time()-3600);
        header("Location: login.php?login=failed");
    }
    exit();
?>

```

## Introduction to relational database

### Basic commands

we use **SQLite** in this class

- `Sqlite3`: enter sqlite command line tool interface
- `.open databaseName.db`: open database with name `databaseName`; if no such file exists, new database file will be created

create table syntax

```sqlite
create table table_name (column_name1 datatype1, column_name2 datatype2, ...);
```

example

```sqlite
create table items 
  (id integer primary key autoincrement, title text, status text);
```

- `.tables`: show list of existing tables
- `.schema table_name`: see the organizational structure of a table with name `table_name`
- `drop table table_name` deleting table with name `table_name`

### working with records

#### Inserting data

syntax

```sqlite
insert into table_name (column_name1, column_name2, ...) values (value1, value2, ...)
```

example

```sqlite
insert into items (title, status) values ('walk the dog', 'in progress');
insert into items (title, status) values ('finish micro assignment', 'completed');
insert into items (title, status) values ('study for web dev final', 'in progress');
```

#### Viewing/Retrieving Data

syntax

```sqlite
select * from table
```

`*`: a "wildcard" that says "retrieve all data"

to limit the columns to retrieve:

```sqlite
select id, title, status, from items
```

##### order by

- `asc`: stands for ascending
- `desc`: stands for descending

```sqlite
select * from items ordered by title asc;
```

#### `where` clause

`where`: extract only those records that fulfill a specific condition

syntax

```sqlite
select * from table_name where column_name1 [=/</>] desired_value1;
select * from table_name where 
    column_name1 [=/</>] desired_value1
    and column_name2 [=/</>] desired_value2;
```

example

```sqlite
select * from items where status = 'in progress';
```

#### Deleting Data

syntax

```sqlite
delete from table_name where conditions;
```

example

```sqlite
delete from items where status = `completed`;
```

#### Updating data

`update ... set ...`: used to modify the existing records in a table

syntax

```sqlite
update table_name set column_name1 = value1, column_name2 = value2... where conditions;
```

example

```sqlite
update items set status = 'completed' where id = 3;
```

## Using SQLite with PHP

### Connect to database

#### config.php

```php
// identify file path of where our databases are stored on the server
$path = '/your/file/path/goes/here';
// connect to our database
$db = new SQLite3($path . "/to_do_list.db");
```

### Running a Query

- connect to database
- construct query using a string
- execute the query using the connection object
- deal with any return values

#### Running an insert query

##### insert.php

```php
<?php
// 1: import database object
include('config.php');
/**
 * @var Sqlite3 $db
 **/

// 2: grab value send from other file
$title = $_POST['title'];
$status = $_POST['status'];

// 2: construct insert query
$sql = "insert into items (title, status) values ('$title', '$status')";
// 3: run the query
$db->query($sql);
?>
```

==Note: to safely add string into database:==

```php
$title = $db->escapeString(addslashes(htmlspecialchars($title)));
$status = $db->escapeString(addslashes(htmlspecialchars($status)));
$sql = "insert into items (title, status) values ('$title', '$status')";
$db->query($sql);
```

#### Running a delete or update query

```php
// 1: import database object
include('config.php');
/**
 * @var Sqlite3 $db
 **/

// 2: construct a delete query
$sql_delete = "delete from items where title = 'feed the cat'";
// 3: run the query
$db->query($sql_delete);


// construct another query
$sql_update = "update items set status = 'completed' where title = 'review for final'";
// run the query
$db->query($sql_update);
```

#### Running a select query

data returned by select query will need some extra code to process

```php
// 1: import database object
include('config.php');
/**
 * @var Sqlite3 $db
 **/

// 2: construct a select query
$sql = "select (id, title, status) from items";
// 3: run the query
$result = $db->query($sql);

// 4: iterate over the results
while ($row = $result->fetchArray()) {
  // extract the relevant info from the query into some variables
  $id = $row["id"];
  $title = $row["title"];
  $status = $row["status"];
}
```

==To return data to an ajax call==

```php
$arr_return = array();
while ($row = $result->fetchArray()) {
  $arr_temp = array();
  // extract the relevant info from the query into some variables
  $arr_temp["id"] =  $row["id"];
  $arr_temp["title"] =  $row["title"];
  $arr_temp["status"] =  $row["status"];
  // append row to array
  $arr_return[] = $arr_temp;
}
// encode data to json format
print json_encode($arr_return);
exit();
```

#### other commands

- `$db->lastInsertRowID()`: obtain the integer id that goes along with the record just inserted
- `$db->changes()`: get a count of how many records were affected by your last query

## Introduction to jQuery

### Bring in the jQuery library

```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js"
  integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4="
  crossorigin="anonymous">
</script>
```

### Basic jQuery syntax

```javascript
let foo = $('#foo');

// edit css
foo.css("background-color", "red");

// set/get attribute
foo.attr("src", "star.png");
let image_src = foo.attr("src");

// change inner value
$("#text_box").html("<h1>Hello world!</h1>");

// select all <p> tag and change color
$("p").css("color", "red");

// edit class
if (foo.hasClass("error")) {
  foo.removeClass("error");
} else {
  foo.addClass("error");
}
```

==document.ready== will execute after all resource is loaded

```javascript
$(document).ready(function(){
  // do something
})
```

## AJAX with jQuery

```javascript
$.ajax({
    type: "post",
    url: "target_file.php",
    data: {
      // name value pair goes here
      name: $username,
      age: $user_age,
    },
    success: function (data, status) {
      output.innerHTML += data + "<br>";
    },
    // error will run if the request failed
    error: function (request, data, status) {
      output.innerHTML += "Error occurred<br>"
    }
})
```

## PHP session

A way to store information to be used across multiple pages.
Unlike a cookie, the information stored on the server.

- `session_start()`: start a session
- `$_SESSION`: php global variable, where session variables are set
- `session_unset()`: free all session variables currently registered
- `session_destroy()`: destroy all data registered to a session

> `session_unset()` vs. `session_destroy()`
>
>- `session_unset()`: deletes only the variables from session and session still exists
>- `session_destroy()` destroys all of the data associated with he current session. It doesn't unset any of the global variables associated with this session, or unset the session cookie

### start a session `start_session.php`

```php
<?php
// start the session
session_start();
// set session variables
$_SESSION["favcolor"] = "black";
$_SESSION["favanimal"] = "dog";
?>
```

### get session variable values `retrieve_session_variable.php`

```php
<?php
session_start();
// print session variable stored in session_start.php
print "favorite color is" . $_SESSION["favcolor"] . "<br>";
print "favorite animal is" . $_SESSION["favanimal"] . "<br>";
?>
```

### modify session variables `session_modify.php`

```php
<?php
session_start();
// overwrite session variable
$_SESSION["favcolor"] = "yellow";
?>
```

#### destroy php session

```php
<?php
session_start();

// remove all session variables
session_unset();

// destroy the session
session_destroy();
?>
```

## API

**API**: Application programming interface, is a connection between computers or between computer programs.

>==API== vs. ==REST API==
>==REST== is a type of API. Not all APIs are REST, but all REST services are APIs.
>
>==API== is a very broad term. Generally it's how one piece of code talks to another. In web development API often refers to the way in which we retrieve information from an online service. The API documentation will give you a list of URLs, query parameters and other information on how to make a request from the API, and inform you what sort of response will be given for each query.
>
>==REST== is a set of rules/standards/guidelines for how to build a web API. Since there are many ways to do so, having an agreed upon system of structuring an API saves time in making decisions when building one, and saves time in understanding how to use one.
>==REST== just is a guiding principle how to use URLs and the HTTP protocol to structure an API. It says nothing about return formats, which may just as well be JSON.

### Access a REST API via an AJAX call

```html
<html lang="en">
<head>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"
            integrity="sha256-/xUj+3OJU5yExlq6GSYGSHk7tPXikynS7ogEvDej/m4="
            crossorigin="anonymous">
    </script>
    <style>html{background-color: black}</style>
    <title>api</title>
</head>
<body>
    <script>
        // grab info about our favorite Pokémon form the Poke API
        function createImage(data){
            for (let key in data[ 'sprites' ]) {
                if (data['sprites'][key] && typeof data['sprites'][key] == 'string'){
                    let tempImage = document.createElement('img');
                    tempImage.src = data['sprites'][key];
                    document.querySelector('body').append(tempImage);
                }
            }
        }
        $(document).ready(function(){
            $.ajax({
                url: "https://pokeapi.co/api/v2/pokemon/pikachu",
                success: function (data, status){
                    console.log(data);
                    if (data['sprites']){
                        createImage(data);
                    }
                }
            })
        })
    </script>
</body>
</html>
```

![pikachu](images/4a83e6b2d809095328ad7031174b573645f802eb9009c051da32fd9073f61a10.png)  

## Additional stuff

### Json

#### Javascript

- `JSON.parse(data)`: parse `data` json string into a javascript Object

#### php

- `json_encode($data)`: encode `$data` into json format

### Hashing

password should be hashed before stored into database

```php
$password = $_POST['password];
$salt = "apple";
$password = md5($password, $salt);
```

You can store  `$salt` in config file

### Linux basic commands

- `ls`: list all the files and directories
- `ls -l`: give more info about the files and directories
- `pwd`: list current working directory
- `cd`: go to directory
  - `cd ..`: go up a folder
  - `cd /`: go to root directory
  - `cd ~` or `cd`: go to home directory
- `nano hello.html` : create a file hello.html, you can use `vim` instead
- `ssh`: stands for Secure Shell, is a network communication protocol that enables two computer to communicate.
  - `ssh -l sz3047 i6.cims.nyu.edu`: login with my account
- `mkdir`: make new directory
- `touch`: create a file

#### `cp`: stands for copy

syntax:

```bash
cp Source Destination
# copy content from Source (filename) to Destination (filename)
# create new or overwrite

cp Source Directory
cp Source-1 Source-2 Source-3 Source-4 ... Directory
# copy Source ... to Directory with the same filename, Directory must exists

cp -R CS/vim .
# copy vim directory under CS directory
# -R for recursive 
```

#### `mv`: stands for move

1. It renames a file or folder
2. It moves a group of files to a different directory

syntax:

```bash
mv Source Destination
# rename Source (filename) to Destination (filename)
# create new or overwrite

mv Source Directory
mv Source1 Source2 Source3 ... Directory
# move file Source (filename) to Destination
# destination must exists
```

#### `rv`: stands for remove

```bash
rm Source
rm Source1 Source2 Source3 ...
```

### The LAMP stack

- linux: the operating system run by most servers
- Apache: the web server software run by most servers
- MySQL: the database software run by most servers
- PHP/Python/..: the programming language run by most servers

#### Apache

The open-source software that is designed to listen for web page requests and respond to them

<div style="font-size: 3em; text-align: center; margin: 1em auto;">🌑 🌒 🌓 🌔 🌕 🌖 🌗 🌘 🌑 </div>

## Contents before midterm

### basic Javascript

#### `typeof()`

returns a string indicating the type of unevaluated operand

returned types:

- `string`
- `number`
  - includes `NaN`
  - float, integer
- `boolean`
- `object`
  - includes `null`
- `function`
- `undefined`
  - datatype of an undefined variable
  - datatype of a variable that has not been assigned a value

#### parse datatype

- `parseInt()`
- `parseFloat()`
- `variable.toString()`

#### array & object

##### array

```javascript
let arr = ["apple", "pear", "peach"];
```

##### object

```javascript
let pokemon = {
    name: "Pikachu",
    age: 6,
    power: ["thunder", "shock"],
    sayHello: function() {
        console.log("hello");
        console.log( this.name );
    }
};
```

#### DOM

##### Attributes

```javascript
let element = document.getElementById('element');
element.href = "...";

element.target = "blank";
element.setAttribute("target", "blank");

element.id = element.getAttribute("id") // true

element.style.color = "green";
element.style["font-size"] = "200%";
```

##### Classes

```javascript
let a = document.getElementById('one');
if (a.classList.contains("foo")) {
    a.classList.remove("foo");
} else {
    a.classList.add("foo");
}
```

##### create new DOM elements

```javascript
let newTag = document.createElement("p");
let body = document.getElementById("body");
newTag.innerHTML = "Hello, world";
body.append(newTag);

// or body.appendChild(newTag);
```

#### Cookies

##### set a cookie

```javascript
document.cookie = "name=Sirui";
// this will create a new cookie, will not overwrite other cookies
```

##### access cookie

`let x = document.cookie;`

- a cookie string delimited by `;`

#### localStorage

##### set value

`window.localStorage.setItem(key, value);`

##### access value

`window.localStorage.getItem(key);`

#### data- attribute

```html
<div id="container" data-columns="3" data-index-number="12314">
```

##### access via javascript

```javascript
const container = document.getElementById("container");
container.dataset.columns; // 3
container.dataset.indexNumber; // 12314
```

