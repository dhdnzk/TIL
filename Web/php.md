### php

#### syntax

```php
<? php 

//code here

?>
```

- echo 
```php
<?php 

echo "hello, world!";

?>
```

- string
```php
<?php 

echo "hello, " . "world!";  // 다른 언어에서 스트링 처리할때의 더하기랑 같은뜻 

?>
```

- variables
```php
<?php

$name = "NekoToken";

$age = 100;

?>
```

- if
```php
<? php

if($var > 10) {

    echo "var > 10!";

}
elseif($var == 10) {

    echo "var == 10!";

}
else {

    echo "var < 10!";

}

?>
```

- switch
```php
<? php

switch($var) {
    case 0:
        //...

    case 1:
        //...

    case 2:
        //...

    case 3:
        //...

    default:
        //...

?>
```
```php
<?php

switch($var):

    case 0:
        //...

    case 1:
        //...

    case 2:
        //...

    default:
        //...

endswitch;

?>
```

- array
```php
<? php

$ary = array("aaa", "bbb", "CCC");

&ary[0] //"aaa"

$ary{0} //"aaa"

unset($ary[0]);

unset($ary);

?>
```

```php
<? php

// => 키워드(key => value);
$ary = array("aaa" => 3, "bb" => 2, "ccccc" => 5);

?>
```

```php
<? php

$ ary = array(array(0, 1, 2),
        array(0, 1, 2),
        array(0, 1, 2));

echo $ary[0][0];

?>
```

- for 
```php
<? php

for($i = 0; i < 10; i ++) {

    //code here!

}

?>
```

- foreach
```php
<?php

forEach ($langs as $lang) {

    echo "<li>$lang</li>";

}

$numbers = array(1, 2, 3);

foreach($numbers as $item) {
    echo $item;
}

?>
```

- while
```php
<? php

while(condition) {

}

?>
```
```php
<? php

while(condition):

endwhile;

?>
```

- do-while
```php
do {

    echo $i;

} while ($i > 0);

```

#### function

- stringFunction
```php
<? php

$length = strlen("abcdefg");

print $length;

?>
```
```php
<? php

$partial = substr("abcde", 0, 3);

print $partial;         //"abc"

$upperStr = strtoupper($partial)    //"ABC"

$lowerStr = strtolower($upperStr);   //"abc"

?>
```
```php
<? php

strpos("emily", "e");   // 0

strpos("emily", "i");   // 2

strpos("emily", "ily"); // 2

strpos("emily", "zxc"); // false

?>
```

- mathFunction
```php
<?php

// Round pi down from 3.1416...
$round = round(M_PI);

print $round;  // prints 3

// This time, round pi to 4 places
$round_decimal = round(M_PI, 4);

print $round_decimal; // prints 3.1416

?>
```
```php
<? php

// prints a number between 0 and 32767
print rand();

// prints a number between 1 and 10
print rand(1,10);

?>
```

- arrayFunction
```php
<?php

$fav_bands = array();

array_push($fav_bands, "Maroon 5");

array_push($fav_bands, "Bruno Mars");

array_push($fav_bands, "Nickelback");

array_push($fav_bands, "Katy Perry");

array_push($fav_bands, "Macklemore");

print count($fav_bands);    // 5

?>
```

```php
<? php

$array = array(5, 3, 7, 1);

sort($array);

print join(", ", $array);
// prints "1, 3, 5, 7"

$array = array(5, 3, 7 ,1);

rsort($array);

print join(":", $array);
// prints "7:5:3:1"

?>
```
```php
join(glue, array)
```

- function definition
```php
<? php

function name($var1, $var2) {

  statement;

  return someValue;

}
?>
```

### object

```php
function __construct() {

}
```

```php
<? php
class Person {

    public $isAlive = true;
    public $firstname;
    public $lastname;
    public $age;

    public function __construct($firstname, $lastname, $age) {
        $this->firstname = $firstname;
        $this->lastname = $lastname;
        $this->age = $age;
    }

    // Creating a method (function tied to an object)
    public function greet() {

        return "Hello, my name is " . $this->firstname . " " . $this->lastname . ". Nice to meet you! :-)";

    }

}
?>
```

```php
<?php

class Person {

    public $age;
    public $sex;

    public function __construct() {

        $this->age = 10;
        $this->sex = "male";

    }

}

// 클래스 안의 멤버변수에 접근할때에는 $className->memberVariable 의 형태로 접근
// or Class::memberVariable을 붙여서 범위지정을 해줌

?>
```

```php
<? php
class AA extends A {

    final public function(){

        // 오버라이딩 안됨!

    }

}
?>
```
```php
<? php

// const keyword 상수에는 $안붙임
const aaa;

//static keyword
static $aaa;

?>
```

### php html

```php
<?php

$_SESSION[key] = value
value = $_SESSION[key]

?>
```
```php
<?php

$_GET[key] = value
value = $_GET[key]

?>
```
```php
<?php

$_POST[key] = value
value = $_POST[key]

?>
```

### php database
```php
<?php

$pdo = new PDO(dns, username, password, option);

?>
```

