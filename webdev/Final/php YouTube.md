
# php YouTube

## Write HTML

```php
echo("Hello world");
//or echo "Hello world";
print("Hello world");
```

*difference between echo and print:*
 echo has no return value while print has a return value of 1 so it can be used in expressions.

**print a header for my site**

```php
echo "<h1>My site</h1>"
```

## variables

```php
$characterName = "Sirui";  
$characterAge = 35;  
echo "There once was a man named $characterName <br>";  
echo "He was $characterAge years old <br>";  
echo "He really liked the name $characterName <br>";  
echo "But didn't like being $characterAge <br>";
```

## Data Types

```php
$phrase = "To be or not to be";  
$age = 21;  
$gpa = 3.9;  
$isMale = false;
```

## Working With Strings

```php
$phrase = "New York University <br>";  
echo $phrase;  
echo strtolower($phrase);  
echo strtoupper($phrase);  
echo strlen($phrase) . "<br>";  
echo $phrase[0] . "<br>";  
// the first character in this string  
$phrase[0] = "B";  
echo $phrase;  
// Bew York University  
echo str_replace("University", "Academy", $phrase);  
// Bew York Academy  
echo substr($phrase, 0, 2);  
// Be
```

## Working With Numbers

```php
echo 40.999 . "<br>";  
echo 5 + 9 . "<br>";  
echo 5 / 9 . "<br>";  
echo 5 * 9 . "<br>";  
echo 10 % 3 . "<br>";  
  
$num = 10;  
echo $num . "<br>";  
// 10  
echo ++$num . "<br>";  
// 11  
echo $num++ . "<br>";  
// 11  
$num += 25;  
// 37  
echo $num . "<br>";  
echo abs(-100) . "<br>";  
// 100  
// pow( , ); sqrt(); max( , ); min( , ); round( ) : round according to common rounding rules  
// ceil( ), floor( )
```

## Getting User Input

```php
<form action="test.php" method="get">  
 Name: <input type="text" name="username"><br>  
 Age: <input type="text" name="age"><br>  
 <input type="submit">  
</form>  
<br>  
Your name is <?php echo @$_GET['username'] ?>  
<br>  
Your age is <?php echo @$_GET['age'] ?>
```

## Building a basic calculator

```php
<form action="test.php" method="get">
 First num <input type="number" name="num1">
 <br>
 Second num <input type="number" name="num2">
 <br>
 <input type="submit">
</form>

<?php
 echo "result: " . @$_GET["num1"] + @$_GET["num2"];
?>
```

**method = "get":**
<http://localhost:63344/learnPhp/test.php?num1=1&num2=1>

## Building a Mad Libs game

```php
<form action="test.php" method="get">  
 Color: <input type="text" name="color"> <br>  
 Plural Noun: <input type="text" name="noun"> <br>  
 Celebrity: <input type="text" name="celebrity"> <br>  
 <input type="submit">  
</form>  
  
<?php  
 $color = @$_GET["color"];  
 $pluralNoun = @$_GET["noun"];  
 $celebrity = @$_GET["celebrity"];  
 echo "Roses are $color <br>";  
 echo "$pluralNoun are blue <br>";  
 echo "I love $celebrity <br>";  
?>
```

## POST vs. GET

**get**

```php
<form action="test.php" method="get">  
 password: <input type="password" name="password"> <br>  
 <input type="submit">  
</form>  
  
<?php  
 $password = @$_GET["password"];  
 echo $password;  
?>
```

<http://localhost:63344/learnPhp/test.php?password=9805>

**post**

```php
<form action="test.php" method="post">  
 password: <input type="password" name="password"> <br>  
 <input type="submit">  
</form>  
  
<?php  
 $password = @$_POST["password"];  
    echo $password;  
?>
```

<http://localhost:63344/learnPhp/test.php>

## Arrays

```php
$friends = array("one", 1, false, "two", "three");  
echo $friends[0] . "<br>";  
// one  
$friends[1] = "Sirui";  
echo $friends[1] . "<br>";  
$friends[10] = "fine";  
  
echo count($friends);  
// 6
```

## Using Checkboxes

```php
<form action="test.php" method="post">  
 Apples: <input type="checkbox" name="fruits[]" value="apples"><br>  
 Oranges: <input type="checkbox" name="fruits[]" value="oranges"><br>  
 Pears: <input type="checkbox" name="fruits[]" value="pears"><br>  
 <input type="submit">  
</form>  
  
<?php  
 $fruits = $_POST["fruits"];  
 echo $fruits[0];  
?>
```

## Associative Arrays

```php
<form action="test.php" method="post">  
 <input type="text" name="student">  
 <input type="submit">  
</form>  

<?php  
 $grades = array("Jim"=>"A+", "Pam"=>"B-", "Sirui"=>"A+++");  
echo @$grades[@$_POST["student"]];  
?>
```

## Function

```php
function sayHi($name, $age){  
 echo "Good Morning: $name <br>";  
    echo "You are $age<br>";  
}  
sayHi("Sirui", "21");  
sayHi("Dave", "20");
```

## Return Value

```php
function cube($num): float|int {  
 return $num * $num * $num;  
}  
$result = cube(4);  
echo $result;
```

## if

```php
$isMale = true;  
$isTall = false;  
// && and  
// || or  
if ($isMale && $isTall){  
 echo "You are a tall male";  
} else if ( $isMale && !$isTall ){  
 echo "You are a male";  
} else {  
 echo "Yor are not a male";  
}
```

## if compare

```php
//        echo max(3, 6);  
 function getMax($num1, $num2) : float|int {  
 return $num1>$num2 ? $num1: $num2;  
//            if ($num1 > $num2){  
//                return $num1;  
//            }else {  
//                return $num2;  
//            }  
 }  
 echo getMax(10, 9);
```

## calculator

```php
<form action="test.php" method="post">  
 First Num:<input type="number" name="num1"><br>  
 OP: <input type="text" name="op"><br>  
 Second Num: <input type="number" name="num2"><br>  
 <input type="submit">  
</form>  
<?php  
 $num1 = @$_POST['num1'];  
    $num2 = @$_POST['num2'];  
    $op = @$_POST['op'];  
  
    if($op == "+"){  
 echo $num1 + $num2;  
    } else if ($op == "-"){  
 echo $num1 - $num2;  
    } else if ($op == "*"){  
 echo $num1 * $num2;  
    } else if ($op == "/"){  
 echo $num1 / $num2;  
    } else {  
 echo "Invalid operator";  
    }  
?>
```

## switch

```php
<form action="test.php" method="post">  
 What is your grade?<br>  
 <input type="text" name="grade">  
 <input type="submit">  
</form>  
<?php  
 $grade = @$_POST['grade'];  
    switch($grade){  
 case "A":  
 echo "You did amazing";  
            break;  
        case "B":  
 echo "You did pretty good";  
            break;  
        case "C":  
 echo "You did poorly";  
            break;  
        case "F":  
 echo "You FAIL!";  
            break;  
        default:  
 echo "Invalid grade";  
            break;  
    }  
?>
```

## while

```php
$index = 1;  
while ($index <= 10){  
 echo "$index <br>";  
    $index++;  
}  
do {  
 echo "$index <br>";  
    $index--;  
} while ($index > 0)
```

## for loop

```php
for ($i = 0; $i < 5; $i++){  
 echo "$i <br>";  
}  
$numbers = array(1,2,3,4,5,6,7,8,9);  
for ($i = 0; $i < count($numbers); $i++){  
 echo $numbers[$i] . "<br>";  
}
```

### for each

In order to be able to directly modify array elements within the loop precede `$value` with `&`.

```php
<?php
$arr = array(1,2,3,4);
foreach($arr as &value){
   $value = $value * 2;
}

$associative_arr = array("one"=>1, "two"=>2, "three"=>3);
foreach($associative_arr as $key=>$value){
   print $value;
}
?>
```

## Including HTML

component: **header.html**

```html
<h1>Sirui Zhang's Website</h1>  
<hr>
```

component: **footer.html**

```html
<hr>  
<h3>Thanks for visiting</h3>
```

main file: **test.php**

```php
<?php include "header.html"; ?>  
<p>Hello World</p>  
<?php include "footer.html"; ?>
```

## Including PHP

component: **articleHeader.php**

```php
<h2><?php  
 echo $title;  
?></h2>  
<h4><?php  
 echo $author;  
?></h4>  
word count: <?php  
 echo $wordCount;  
?>
```

component: **usefulTools.php**

```php
<?php  
 $feetInMile = 5280;  
    function sayHi($name){  
 echo "Hello $name";  
    }
```

main file: **test.php**

```php
<?php  
 include "usefulTools.php";  
    /**  
 * @var $feetInMile  
 */  
?>  
  
<?php  
 $title = "My First Post";  
    $author = "Sirui";  
    $wordCount = 900;  
    include "articleHeader.php";  
?>  
 <hr>  
<?php  
 sayHi("Sirui");  
?>  
 <hr>  
<?php  
 echo $feetInMile;  
?>
```

## Classes  & Objects

```php
class Book{  
 var $title;  
    var $author;  
    var $pages;  
}  
  
$book1 = new Book();  
$book1->title = "Harry Potter";  
$book1->author = "JK Rowling";  
$book1->pages = 400;  
  
$book2 = new Book();  
$book2->title = "Lord Of the Rings";  
$book2->author = "Tolkien";  
$book2->pages = 700;  
  
echo $book1->title;  
echo $book2->title;
```

## Constructors

```php
class Book{  
 var string $title;  
 var string $author;  
 var int $pages;  
 
 function __construct($title, $author, $pages){  
  $this->title = $title;  
  $this->author = $author;  
  $this->pages = $pages;  
 }  
}  
  
$book1 = new Book("Harry Potter", "JK Rowling", 400);  
$book1->title = "Hunger Games";
  
echo $book1->title . "<br>";
```

## Object Functions

```php
class Student{  
 var string $name;  
 var string $major;  
 var int $gpa;  
 
 function __construct($name, $major, $gpa){  
  $this->name = $name;  
  $this->major = $major;  
  $this->gpa = $gpa;  
 }  
 
 function hasHonors(): string {  
  return $this->gpa > 3.5 ? "true": "false";  
 }  

}  

$student1 = new Student("Sirui", "Computer Science", 4.0);  
echo $student1->hasHonors();
```

## getters/setters

```php
class Movie{  
 public string $title;  
 private string $rating;  
 private static array $ratings = array("G", "PG", "PG-13", "R", "NR");  
 
 public function __construct(string $title, string $rating) {  
  $this->title = $title;  
  $this->setRating($rating);  
 }  
 
 public function setRating(string $rating){  
  if(in_array($rating, Movie::$ratings))  
   $this->rating = $rating;  
  else  
   $this->rating = "NR";  
 }  
  
 public function getRating(): string {  
  return $this->rating;  
 }  
 
}  

$avengers = new Movie("Avengers", "PG-13");  
$avengers->setRating("dog");  
echo $avengers->getRating();  
// NR
```

^2c4479

## Inheritance

```php
class Chef {  
 function makeChicken(){  
  echo "The chef makes chicken <br>";  
 }  
 
 function makeSalad(){  
  echo "The chef makes salad <br>";  
 }  
 
 function makeSpecialDish(){  
  echo "The chef makes bbq ribs <br>";  
 }  
}  
  
class ItalianChef extends Chef {  
 function makePasta() {  
  echo "The chef makes pasta <br>";  
 }  
 
 function makeSpecialDish() {  
  echo "The chef makes chicken parm";  
 }  
}  
  
$chef = new Chef();  
$chef->makeChicken();  
 
$italianChef = new ItalianChef(); 
$italianChef->makePasta(); 
  
$chef->makeSpecialDish(); 
$italianChef->makeSpecialDish(); 
```
