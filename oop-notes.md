# Object-Oriented Programming (OOP) Cheat Sheet in PHP

## Basics of OOP

- **Object:** An instance of a class that encapsulates data and behavior.

- **Class:** A blueprint or template for creating objects. It defines properties (attributes) and methods (functions) that objects of that class will have.

## Four Pillars of OOP

1. **Encapsulation:**
   - The bundling of data (attributes) and methods (functions) that operate on the data into a single unit (class).
   - Access to the data is controlled through getter and setter methods.
2. **Inheritance:**

   - The process by which one class (subclass or derived class) inherits properties and behaviors from another class (superclass or base class).
   - Allows for code reuse and creating a hierarchy of classes.

3. **Polymorphism:**

   - The ability of objects of different classes to respond to the same method in a way that is specific to their class.
   - Achieved through method overriding and interfaces/abstract classes (in some languages).

4. **Abstraction:**
   - The process of simplifying complex reality by modeling classes based on essential properties and behaviors.
   - Hides the unnecessary details while exposing the necessary features.

## Classes and Objects

Create an Object:

```
$obj = new ClassName();  // Instantiate an object
```

Class Constructor (Initializer):

```
class MyClass {
    public function __construct($arg1, $arg2) {
        $this->arg1 = $arg1;
        $this->arg2 = $arg2;
    }
}
```

Accessing Class Members:

```
$obj->arg1;  // Access object attributes
$obj->method();  // Call object methods
```

## Inheritance

Single Inheritance:

```
class Subclass extends Superclass {
    // Subclass inherits from Superclass
}
```

# Multiple Inheritance Using Traits

```
// Define Trait 1
trait Trait1 {
    public function methodTrait1() {
        echo "Method from Trait1";
    }
}

// Define Trait 2
trait Trait2 {
    public function methodTrait2() {
        echo "Method from Trait2";
    }
}

// Create a Class Using Multiple Traits
class MyClass {
    use Trait1, Trait2;

    public function myMethod() {
        echo "My Class Method";
    }
}

// Create an Object
$obj = new MyClass();

// Access Methods from Traits and Class
$obj->methodTrait1();  // Calls methodTrait1 from Trait1
$obj->methodTrait2();  // Calls methodTrait2 from Trait2
$obj->myMethod();      // Calls myMethod from MyClass
```

## Polymorphism

Method Overriding:

```
class Superclass {
    public function method() {
        echo "Superclass method";
    }
}

class Subclass extends Superclass {
    public function method() {
        echo "Subclass method";
    }
}

$obj = new Subclass();
$obj->method();  // Calls Subclass method
```

## Abstraction

Abstract Class (in PHP):

```
abstract class AbstractClass {
    abstract public function abstractMethod();
}

class ConcreteClass extends AbstractClass {
    public function abstractMethod() {
        echo "ConcreteClass implements abstractMethod";
    }
}

$obj = new ConcreteClass();
$obj->abstractMethod();  // Calls ConcreteClass implementation
```

## Encapsulation

Private and Protected Members (in some languages):

- Private members: $variable or private $variable
- Protected members: protected $variable
- Getter and Setter Methods (in some languages):

```
class MyClass {
    private $privateVar = 0;

    public function getPrivateVar() {
        return $this->privateVar;
    }

    public function setPrivateVar($value) {
        if ($value >= 0) {
            $this->privateVar = $value;
        }
    }
}
```

## SOLID Principles (Design Principles)

Single Responsibility Principle (SRP):

A class should have only one reason to change.
Open-Closed Principle (OCP):

Software entities (classes, modules, functions) should be open for extension but closed for modification.
Liskov Substitution Principle (LSP):

Subtypes must be substitutable for their base types without altering the correctness of the program.
Interface Segregation Principle (ISP):

A client should not be forced to depend on interfaces it does not use.
Dependency Inversion Principle (DIP):

High-level modules should not depend on low-level modules. Both should depend on abstractions.
