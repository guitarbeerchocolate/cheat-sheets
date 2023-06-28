# PHP Notes

## Strict types

To use strict types begin your code with:

`<?php declare(strict_types=1);`

## Comments (VSCodium)

For single-line comment use Ctrl+/:

`//`

For block comments Ctrl+Shift+a:

`/*  */`

For phpDoc block comments, just start typing:

`/**`

and it should auto complete.

## Constants

    define("GREETING", "Welcome to W3Schools.com!");
    echo GREETING;

## Operators

Raise $x to the power of $y
`$x \*\* $y`

### Ternary

The value of $x is expr2 if expr1 = TRUE.

The value of $x is expr3 if expr1 = FALSE.

`$x = expr1 ? expr2 : expr3`

## Null coalescing

The value of $x is expr1 if expr1 exists, and is not NULL.

If expr1 does not exist, or is NULL, the value of $x is expr2.

`$x = expr1 ?? expr2`

## Break & Continue

The `break` statement can also be used to jump out of a loop or `switch` statement.

The `continue` statement breaks one iteration (in the loop), if a specified condition occurs, and continues with the next iteration in the loop.

## Callback functions

There are 3 styles of callback function. First is the standard use within `array_map`.

    function myCallback($item) {
    return strlen($item);
    }

    $strings = ["apple", "orange", "banana", "coconut"];
    $lengths = array_map("myCallback", $strings);
    print_r($lengths);

Second is to decalre the function within `array_map`.

    $strings = ["apple", "orange", "banana", "coconut"];
    $lengths = array_map(
        function($item)
        {
            return strlen($item);
        }, $strings);
    print_r($lengths);

Third is not to use array_map at all.

    function exclaim($str) {
        return $str . "! ";
    }

    function ask($str) {
        return $str . "? ";
    }

    function printFormatted($str, $format) {
        echo $format($str);
    }

    printFormatted("Hello world", "exclaim");
    printFormatted("Hello world", "ask");

## OOP

### Constants

    class Goodbye {
    const LEAVING_MESSAGE = "Thank you for visiting W3Schools.com!";
    }

    echo Goodbye::LEAVING_MESSAGE;

### Abstract classes and methods

These are when the parent class has a named method, but need its child class(es) to fill out the tasks. E.g.

    abstract class Car {
        public $name;
        public function __construct($name) {
            $this->name = $name;
        }
        abstract public function intro() : string;
    }

    class Audi extends Car {
        public function intro() : string {
            return "Choose German quality! I'm an $this->name!";
        }
    }

    class Volvo extends Car {
        public function intro() : string {
            return "Proud to be Swedish! I'm a $this->name!";
        }
    }

    $audi = new audi("Audi");
    echo $audi->intro();

    $volvo = new volvo("Volvo");
    echo $volvo->intro();

### Interfaces

Similar to abstract classes except:

Interfaces cannot have properties.

All interface methods must be public.

All methods in an interface are abstract (no code).

Classes can implement an interface while inheriting from another class at the same time.

    interface Animal {
        public function makeSound();
    }

    class Cat implements Animal {
        public function makeSound() {
            echo "Meow";
        }
    }

    $animal = new Cat();
    $animal->makeSound();

### Multiple inheritance using `traits`

    trait message1 {
        public function msg1() {
            echo "OOP is fun! ";
        }
    }

    trait message2 {
        public function msg2() {
            echo "OOP reduces code duplication!";
        }
    }

    class Welcome {
        use message1, message2;
    }

    $obj = new Welcome();
    $obj->msg1();
    $obj->msg2();

### Static methods

Static methods can be called directly - without creating an instance of the class first.

    class greeting {
        public static function welcome() {
            echo "Hello World!";
        }
    }

    greeting::welcome();

A static method can be accessed from a method in the same class using the `self` keyword

    class greeting {
        public static function welcome() {
            echo "Hello World!";
        }

        public function __construct() {
            self::welcome();
        }
    }

    new greeting();

### Static Properties

Static properties can be called directly - without creating an instance of a class.

    class pi {
        public static $value = 3.14159;
    }

    echo pi::$value;

A static property can be accessed from a method in the same class using the `self` keyword.

    class pi {
        public static $value=3.14159;
        public function staticValue() {
            return self::$value;
        }
    }

    $pi = new pi();
    echo $pi->staticValue();

To call a static property from a child class, use the `parent` keyword.

    class pi {
        public static $value=3.14159;
    }

    class x extends pi {
        public function xStatic() {
            return parent::$value;
        }
    }

    echo x::$value;
    $x = new x();
    echo $x->xStatic();
