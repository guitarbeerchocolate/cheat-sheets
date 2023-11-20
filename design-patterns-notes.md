# Design Patterns Cheat Sheet

## Creational Design Patterns

### Singleton Pattern

- Ensures a class has only one instance.
- Provides a global point of access to that instance.

Here's an example of the Singleton Pattern implemented in PHP:

```
<?php

class Singleton {
    // Private static variable to hold the single instance of the class
    private static $instance;

    // Private constructor to prevent direct instantiation
    private function __construct() {
        // Initialization code, if any
    }

    // Public static method to get the single instance of the class
    public static function getInstance() {
        if (self::$instance === null) {
            self::$instance = new self();
        }
        return self::$instance;
    }

    // Public method of the singleton class
    public function doSomething() {
        return "Doing something...";
    }
}

// Usage
$singleton1 = Singleton::getInstance();
$singleton2 = Singleton::getInstance();

// Check if both instances are the same
if ($singleton1 === $singleton2) {
    echo "Singleton pattern works! Both instances are the same.\n";
}

// Call a method on the singleton instance
echo $singleton1->doSomething() . "\n";
```

### Factory Method Pattern

- Defines an interface for creating an object but lets subclasses alter the type of objects that will be created.
- Clients code against an abstract type (interface or abstract class).

Here's an example of the Factory Method Pattern implemented in PHP:

```
<?php

// Abstract Product
interface Product {
    public function getName();
}

// Concrete Products
class ConcreteProductA implements Product {
    public function getName() {
        return "Product A";
    }
}

class ConcreteProductB implements Product {
    public function getName() {
        return "Product B";
    }
}

// Abstract Factory
interface Factory {
    public function createProduct();
}

// Concrete Factories
class ConcreteFactoryA implements Factory {
    public function createProduct() {
        return new ConcreteProductA();
    }
}

class ConcreteFactoryB implements Factory {
    public function createProduct() {
        return new ConcreteProductB();
    }
}

// Usage
$factoryA = new ConcreteFactoryA();
$productA = $factoryA->createProduct();
echo $productA->getName() . "\n"; // Output: "Product A"

$factoryB = new ConcreteFactoryB();
$productB = $factoryB->createProduct();
echo $productB->getName() . "\n"; // Output: "Product B"

```

### Abstract Factory Pattern

- Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
- Typically involves multiple Factory Methods.

Here's an example of the Abstract Factory Pattern implemented in PHP:

```
<?php

// Abstract Product Interfaces
interface Chair {
    public function sitOn();
}

interface Table {
    public function putOn();
}

// Concrete Products
class ModernChair implements Chair {
    public function sitOn() {
        return "Sitting on a modern chair.";
    }
}

class ModernTable implements Table {
    public function putOn() {
        return "Putting something on a modern table.";
    }
}

class VictorianChair implements Chair {
    public function sitOn() {
        return "Sitting on a Victorian chair.";
    }
}

class VictorianTable implements Table {
    public function putOn() {
        return "Putting something on a Victorian table.";
    }
}

// Abstract Factory Interface
interface FurnitureFactory {
    public function createChair();
    public function createTable();
}

// Concrete Factories
class ModernFurnitureFactory implements FurnitureFactory {
    public function createChair() {
        return new ModernChair();
    }

    public function createTable() {
        return new ModernTable();
    }
}

class VictorianFurnitureFactory implements FurnitureFactory {
    public function createChair() {
        return new VictorianChair();
    }

    public function createTable() {
        return new VictorianTable();
    }
}

// Client Code
function createAndUseFurniture(FurnitureFactory $factory) {
    $chair = $factory->createChair();
    $table = $factory->createTable();

    echo $chair->sitOn() . "\n";
    echo $table->putOn() . "\n";
}

// Usage
$modernFactory = new ModernFurnitureFactory();
echo "Using Modern Furniture:\n";
createAndUseFurniture($modernFactory);

$victorianFactory = new VictorianFurnitureFactory();
echo "\nUsing Victorian Furniture:\n";
createAndUseFurniture($victorianFactory);
```

### Builder Pattern

- Separates the construction of a complex object from its representation.
- Allows the same construction process to create different representations.

Here's an example of the Builder Pattern implemented in PHP:

```
<?php

// Product
class Computer {
    private $cpu;
    private $ram;
    private $storage;
    private $graphicsCard;

    public function setCPU($cpu) {
        $this->cpu = $cpu;
    }

    public function setRAM($ram) {
        $this->ram = $ram;
    }

    public function setStorage($storage) {
        $this->storage = $storage;
    }

    public function setGraphicsCard($graphicsCard) {
        $this->graphicsCard = $graphicsCard;
    }

    public function showSpecs() {
        $specs = "CPU: {$this->cpu}\nRAM: {$this->ram}GB\nStorage: {$this->storage}GB\nGraphics Card: {$this->graphicsCard}";
        echo $specs . "\n";
    }
}

// Builder Interface
interface ComputerBuilder {
    public function buildCPU();
    public function buildRAM();
    public function buildStorage();
    public function buildGraphicsCard();
    public function getComputer();
}

// Concrete Builder
class GamingComputerBuilder implements ComputerBuilder {
    private $computer;

    public function __construct() {
        $this->computer = new Computer();
    }

    public function buildCPU() {
        $this->computer->setCPU("Intel Core i9");
    }

    public function buildRAM() {
        $this->computer->setRAM(32);
    }

    public function buildStorage() {
        $this->computer->setStorage(1000);
    }

    public function buildGraphicsCard() {
        $this->computer->setGraphicsCard("NVIDIA GeForce RTX 3080");
    }

    public function getComputer() {
        return $this->computer;
    }
}

// Director
class ComputerDirector {
    public function build(ComputerBuilder $builder) {
        $builder->buildCPU();
        $builder->buildRAM();
        $builder->buildStorage();
        $builder->buildGraphicsCard();
    }
}

// Client Code
$gamingBuilder = new GamingComputerBuilder();
$director = new ComputerDirector();
$director->build($gamingBuilder);
$gamingComputer = $gamingBuilder->getComputer();

echo "Gaming Computer Specs:\n";
$gamingComputer->showSpecs();
```

### Prototype Pattern

- Creates new objects by copying an existing object, known as the prototype.
- Useful when the cost of creating an object is more expensive.

Here's an example of the Prototype Pattern implemented in PHP:

```
<?php

// Prototype Interface
interface Prototype {
    public function clone();
}

// Concrete Prototype
class Sheep implements Prototype {
    private $name;
    private $age;
    private $color;

    public function __construct($name, $age, $color) {
        $this->name = $name;
        $this->age = $age;
        $this->color = $color;
    }

    public function getName() {
        return $this->name;
    }

    public function getAge() {
        return $this->age;
    }

    public function getColor() {
        return $this->color;
    }

    public function clone() {
        // Clone the object by creating a new instance with the same properties
        return new self($this->name, $this->age, $this->color);
    }
}

// Client Code
$originalSheep = new Sheep("Dolly", 2, "White");

// Clone the original sheep
$clonedSheep = $originalSheep->clone();

// Modify the cloned sheep
$clonedSheep->setName("Molly");
$clonedSheep->setAge(3);
$clonedSheep->setColor("Black");

echo "Original Sheep: {$originalSheep->getName()}, {$originalSheep->getAge()} years old, {$originalSheep->getColor()}\n";
echo "Cloned Sheep: {$clonedSheep->getName()}, {$clonedSheep->getAge()} years old, {$clonedSheep->getColor()}\n";
```

## Structural Design Patterns

### Adapter Pattern

- Allows objects with incompatible interfaces to work together.
- Wraps one interface around another to make it compatible.

Here's an example of the Adapter Pattern implemented in PHP:

```
<?php

// Target Interface
interface MediaPlayer {
    public function play($audioType, $fileName);
}

// Adaptee Class
class Mp3Player {
    public function playMp3($fileName) {
        echo "Playing MP3 file: $fileName\n";
    }
}

// Adapter Class
class MediaAdapter implements MediaPlayer {
    private $mp3Player;

    public function __construct() {
        $this->mp3Player = new Mp3Player();
    }

    public function play($audioType, $fileName) {
        if ($audioType == "mp3") {
            $this->mp3Player->playMp3($fileName);
        } else {
            echo "Invalid media type: $audioType\n";
        }
    }
}

// Client Code
$mediaPlayer = new MediaAdapter();

$mediaPlayer->play("mp3", "song.mp3");
$mediaPlayer->play("mp4", "movie.mp4");
```

### Bridge Pattern

- Separates an object's abstraction from its implementation.
- Allows both to vary independently.

Here's an example of the Bridge Pattern implemented in PHP:

```
<?php

// Implementor Interface
interface DrawingAPI {
    public function drawCircle($x, $y, $radius);
}

// Concrete Implementor
class DrawingAPI1 implements DrawingAPI {
    public function drawCircle($x, $y, $radius) {
        echo "API1 - Drawing a circle at ($x, $y) with radius $radius\n";
    }
}

class DrawingAPI2 implements DrawingAPI {
    public function drawCircle($x, $y, $radius) {
        echo "API2 - Drawing a circle at ($x, $y) with radius $radius\n";
    }
}

// Abstraction
abstract class Shape {
    protected $drawingAPI;

    public function __construct(DrawingAPI $drawingAPI) {
        $this->drawingAPI = $drawingAPI;
    }

    abstract public function draw();
}

// Refined Abstraction
class Circle extends Shape {
    private $x, $y, $radius;

    public function __construct($x, $y, $radius, DrawingAPI $drawingAPI) {
        parent::__construct($drawingAPI);
        $this->x = $x;
        $this->y = $y;
        $this->radius = $radius;
    }

    public function draw() {
        $this->drawingAPI->drawCircle($this->x, $this->y, $this->radius);
    }
}

// Client Code
$drawingAPI1 = new DrawingAPI1();
$drawingAPI2 = new DrawingAPI2();

$circle1 = new Circle(1, 2, 3, $drawingAPI1);
$circle2 = new Circle(4, 5, 6, $drawingAPI2);

$circle1->draw();
$circle2->draw();
```

### Composite Pattern

- Composes objects into tree structures to represent part-whole hierarchies.
- Clients can treat individual objects and compositions of objects uniformly.

Here's an example of the Composite Pattern implemented in PHP:

```
<?php

// Component Interface
interface Component {
    public function render();
}

// Leaf Component
class Text implements Component {
    private $content;

    public function __construct($content) {
        $this->content = $content;
    }

    public function render() {
        echo $this->content;
    }
}

// Composite Component
class Container implements Component {
    private $children = [];

    public function add(Component $component) {
        $this->children[] = $component;
    }

    public function render() {
        foreach ($this->children as $child) {
            $child->render();
        }
    }
}

// Client Code
$text1 = new Text("Hello, ");
$text2 = new Text("world!");

$container = new Container();
$container->add($text1);
$container->add($text2);

$container->render(); // Output: Hello, world!
```

### Decorator Pattern

- Attaches additional responsibilities to objects dynamically.
- Provides a flexible alternative to subclassing for extending functionality.

Here's an example of the Decorator Pattern implemented in PHP:

```
<?php

// Component Interface
interface Coffee {
    public function cost();
    public function description();
}

// Concrete Component
class Espresso implements Coffee {
    public function cost() {
        return 2.0;
    }

    public function description() {
        return "Espresso";
    }
}

// Decorator
abstract class CoffeeDecorator implements Coffee {
    protected $coffee;

    public function __construct(Coffee $coffee) {
        $this->coffee = $coffee;
    }

    public function cost() {
        return $this->coffee->cost();
    }

    public function description() {
        return $this->coffee->description();
    }
}

// Concrete Decorators
class MilkDecorator extends CoffeeDecorator {
    public function cost() {
        return $this->coffee->cost() + 1.0;
    }

    public function description() {
        return $this->coffee->description() . ", Milk";
    }
}

class SugarDecorator extends CoffeeDecorator {
    public function cost() {
        return $this->coffee->cost() + 0.5;
    }

    public function description() {
        return $this->coffee->description() . ", Sugar";
    }
}

// Client Code
$espresso = new Espresso();
$espressoWithMilk = new MilkDecorator($espresso);
$espressoWithMilkAndSugar = new SugarDecorator($espressoWithMilk);

echo "Cost: $" . $espressoWithMilkAndSugar->cost() . "\n";
echo "Description: " . $espressoWithMilkAndSugar->description() . "\n";

```

### Facade Pattern

- Provides a simplified, high-level interface to a complex subsystem.
- Shields clients from the complexity of the subsystem.

Here's an example of the Facade Pattern implemented in PHP:

```
<?php

// Subsystem 1
class CPU {
    public function freeze() {
        echo "CPU: Freezing...\n";
    }

    public function jump($position) {
        echo "CPU: Jumping to memory position $position\n";
    }

    public function execute() {
        echo "CPU: Executing...\n";
    }
}

// Subsystem 2
class Memory {
    public function load($position, $data) {
        echo "Memory: Loading data into memory position $position: $data\n";
    }
}

// Subsystem 3
class HardDrive {
    public function read($sector, $size) {
        echo "HardDrive: Reading data from sector $sector, size: $size\n";
    }
}

// Facade
class ComputerFacade {
    private $cpu;
    private $memory;
    private $hardDrive;

    public function __construct() {
        $this->cpu = new CPU();
        $this->memory = new Memory();
        $this->hardDrive = new HardDrive();
    }

    public function start() {
        echo "ComputerFacade: Starting the computer...\n";
        $this->cpu->freeze();
        $this->memory->load(0, "BOOT");
        $this->cpu->jump(0);
        $this->cpu->execute();
        $this->memory->load(1, "OS");
        $this->cpu->jump(1);
        $this->cpu->execute();
        echo "ComputerFacade: Computer started successfully!\n";
    }
}

// Client Code
$computer = new ComputerFacade();
$computer->start();
```

### Proxy Pattern

- Provides a surrogate or placeholder for another object to control access to it.
- Types include Virtual, Remote, and Protection Proxies.

Here's an example of the Proxy Pattern implemented in PHP:

```
<?php

// Subject Interface
interface Image {
    public function display();
}

// Real Subject
class RealImage implements Image {
    private $filename;

    public function __construct($filename) {
        $this->filename = $filename;
        $this->loadImage();
    }

    private function loadImage() {
        echo "Loading image from file: {$this->filename}\n";
    }

    public function display() {
        echo "Displaying image: {$this->filename}\n";
    }
}

// Proxy
class ImageProxy implements Image {
    private $realImage;
    private $filename;

    public function __construct($filename) {
        $this->filename = $filename;
    }

    public function display() {
        if ($this->realImage === null) {
            $this->realImage = new RealImage($this->filename);
        }
        $this->realImage->display();
    }
}

// Client Code
$image = new ImageProxy("example.jpg");

// The image is loaded and displayed only when necessary
$image->display();
$image->display();

```

## Behavioral Design Patterns

### Observer Pattern

- Defines a one-to-many dependency between objects.
- When one object changes state, all its dependents (observers) are notified and updated automatically.

Here's an example of the Observer Pattern implemented in PHP:

```
<?php

// Subject (Observable)
class WeatherStation implements SplSubject {
    private $observers = [];

    public function attach(SplObserver $observer) {
        $this->observers[] = $observer;
    }

    public function detach(SplObserver $observer) {
        $index = array_search($observer, $this->observers);
        if ($index !== false) {
            unset($this->observers[$index]);
        }
    }

    public function notify() {
        $data = "Sunny day"; // Weather data (for example)
        foreach ($this->observers as $observer) {
            $observer->update($this, $data);
        }
    }
}

// Observer
class WeatherObserver implements SplObserver {
    public function update(SplSubject $subject, $data = null) {
        echo "Received weather data: " . $data . "\n";
    }
}

// Usage
$station = new WeatherStation();
$observer1 = new WeatherObserver();
$observer2 = new WeatherObserver();

$station->attach($observer1);
$station->attach($observer2);

$station->notify();
```

### Strategy Pattern

- Defines a family of algorithms, encapsulates each one, and makes them interchangeable.
- Allows the client to choose the appropriate algorithm at runtime.

Here's an example of the Strategy Pattern implemented in PHP:

```
<?php

// Strategy Interface
interface PaymentStrategy {
    public function pay($amount);
}

// Concrete Strategies
class CreditCardPayment implements PaymentStrategy {
    private $cardNumber;
    private $name;

    public function __construct($cardNumber, $name) {
        $this->cardNumber = $cardNumber;
        $this->name = $name;
    }

    public function pay($amount) {
        echo "Paid $amount USD using Credit Card ending in {$this->getLastFourDigits()} ({$this->name})\n";
    }

    private function getLastFourDigits() {
        return substr($this->cardNumber, -4);
    }
}

class PayPalPayment implements PaymentStrategy {
    private $email;

    public function __construct($email) {
        $this->email = $email;
    }

    public function pay($amount) {
        echo "Paid $amount USD using PayPal ({$this->email})\n";
    }
}

// Context
class ShoppingCart {
    private $paymentStrategy;
    private $items = [];

    public function setPaymentStrategy(PaymentStrategy $paymentStrategy) {
        $this->paymentStrategy = $paymentStrategy;
    }

    public function addItem($item) {
        $this->items[] = $item;
    }

    public function checkout($amount) {
        echo "Items in the cart:\n";
        foreach ($this->items as $item) {
            echo "- $item\n";
        }

        $this->paymentStrategy->pay($amount);
    }
}

// Client Code
$cart = new ShoppingCart();

$cart->addItem("Product A");
$cart->addItem("Product B");
$cart->addItem("Product C");

// Pay with a credit card
$creditCardPayment = new CreditCardPayment("1234-5678-9876-5432", "John Doe");
$cart->setPaymentStrategy($creditCardPayment);
$cart->checkout(150.0);

// Pay with PayPal
$paypalPayment = new PayPalPayment("john.doe@example.com");
$cart->setPaymentStrategy($paypalPayment);
$cart->checkout(75.0);
```

### Command Pattern

- Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.

Here's an example of the Command Pattern implemented in PHP:

```
<?php

// Receiver
class Light {
    public function on() {
        echo "Light is on\n";
    }

    public function off() {
        echo "Light is off\n";
    }
}

// Command Interface
interface Command {
    public function execute();
}

// Concrete Commands
class LightOnCommand implements Command {
    private $light;

    public function __construct(Light $light) {
        $this->light = $light;
    }

    public function execute() {
        $this->light->on();
    }
}

class LightOffCommand implements Command {
    private $light;

    public function __construct(Light $light) {
        $this->light = $light;
    }

    public function execute() {
        $this->light->off();
    }
}

// Invoker
class RemoteControl {
    private $command;

    public function setCommand(Command $command) {
        $this->command = $command;
    }

    public function pressButton() {
        $this->command->execute();
    }
}

// Client Code
$light = new Light();
$lightOnCommand = new LightOnCommand($light);
$lightOffCommand = new LightOffCommand($light);

$remoteControl = new RemoteControl();

$remoteControl->setCommand($lightOnCommand);
$remoteControl->pressButton(); // Turns the light on

$remoteControl->setCommand($lightOffCommand);
$remoteControl->pressButton(); // Turns the light off
```

### Chain of Responsibility Pattern

- Passes a request along a chain of handlers.
- Each handler decides either to process the request or to pass it to the next handler in the chain.

Here's an example of the Chain of Responsibility Pattern implemented in PHP:

```
<?php

// Handler Interface
interface Handler {
    public function setSuccessor(Handler $successor);
    public function handleRequest($request);
}

// Concrete Handler
class ConcreteHandler implements Handler {
    private $successor;

    public function setSuccessor(Handler $successor) {
        $this->successor = $successor;
    }

    public function handleRequest($request) {
        if ($this->canHandle($request)) {
            echo "ConcreteHandler: Handling request\n";
        } elseif ($this->successor !== null) {
            echo "ConcreteHandler: Passing request to the next handler\n";
            $this->successor->handleRequest($request);
        } else {
            echo "ConcreteHandler: Cannot handle the request\n";
        }
    }

    private function canHandle($request) {
        // Check if this handler can handle the request
        // In a real-world scenario, you would implement specific criteria
        return true;
    }
}

// Client Code
$handler1 = new ConcreteHandler();
$handler2 = new ConcreteHandler();
$handler3 = new ConcreteHandler();

$handler1->setSuccessor($handler2);
$handler2->setSuccessor($handler3);

// Make a request to the first handler
$request = "Sample Request";
$handler1->handleRequest($request);
```

### State Pattern

- Allows an object to alter its behavior when its internal state changes.
- The object will appear to change its class.

Here's an example of the State Pattern implemented in PHP:

```
<?php

// Context
class Context {
    private $state;

    public function __construct(State $state) {
        $this->transitionTo($state);
    }

    public function transitionTo(State $state) {
        echo "Context: Transitioning to " . get_class($state) . ".\n";
        $this->state = $state;
        $this->state->setContext($this);
    }

    public function request1() {
        $this->state->handle1();
    }

    public function request2() {
        $this->state->handle2();
    }
}

// State Interface
interface State {
    public function setContext(Context $context);
    public function handle1();
    public function handle2();
}

// Concrete States
class ConcreteStateA implements State {
    private $context;

    public function setContext(Context $context) {
        $this->context = $context;
    }

    public function handle1() {
        echo "ConcreteStateA handles request1.\n";
    }

    public function handle2() {
        echo "ConcreteStateA handles request2.\n";
        echo "ConcreteStateA wants to change the state of the context.\n";
        $this->context->transitionTo(new ConcreteStateB());
    }
}

class ConcreteStateB implements State {
    private $context;

    public function setContext(Context $context) {
        $this->context = $context;
    }

    public function handle1() {
        echo "ConcreteStateB handles request1.\n";
        echo "ConcreteStateB wants to change the state of the context.\n";
        $this->context->transitionTo(new ConcreteStateA());
    }

    public function handle2() {
        echo "ConcreteStateB handles request2.\n";
    }
}

// Client Code
$context = new Context(new ConcreteStateA());

$context->request1();
$context->request2();
```

### Template Method Pattern

- Defines the skeleton of an algorithm in the base class but lets subclasses override specific steps.

Here's an example of the Template Method Pattern implemented in PHP:

```
<?php

// Abstract Class with Template Method
abstract class AbstractClass {
    // The template method defines the skeleton of the algorithm
    final public function templateMethod() {
        $this->step1();
        $this->step2();
        $this->step3();
    }

    // Abstract methods to be implemented by concrete subclasses
    abstract protected function step1();
    abstract protected function step2();

    // Concrete method with a default implementation
    protected function step3() {
        echo "AbstractClass: Default implementation of step3\n";
    }
}

// Concrete Subclass 1
class ConcreteClass1 extends AbstractClass {
    protected function step1() {
        echo "ConcreteClass1: Step1\n";
    }

    protected function step2() {
        echo "ConcreteClass1: Step2\n";
    }
}

// Concrete Subclass 2
class ConcreteClass2 extends AbstractClass {
    protected function step1() {
        echo "ConcreteClass2: Step1\n";
    }

    protected function step2() {
        echo "ConcreteClass2: Step2\n";
    }

    protected function step3() {
        echo "ConcreteClass2: Custom implementation of step3\n";
    }
}

// Client Code
$object1 = new ConcreteClass1();
$object1->templateMethod();

$object2 = new ConcreteClass2();
$object2->templateMethod();
```

### Visitor Pattern

- Represents an operation to be performed on the elements of an object structure.
- Allows adding new operations without modifying the object structure itself.

Here's an example of the Visitor Pattern implemented in PHP:

```
<?php

// Visitor Interface
interface Visitor {
    public function visitElementA(ElementA $elementA);
    public function visitElementB(ElementB $elementB);
}

// Element Interface
interface Element {
    public function accept(Visitor $visitor);
}

// Concrete Elements
class ElementA implements Element {
    public function accept(Visitor $visitor) {
        $visitor->visitElementA($this);
    }

    public function operationA() {
        echo "ElementA: Operation A\n";
    }
}

class ElementB implements Element {
    public function accept(Visitor $visitor) {
        $visitor->visitElementB($this);
    }

    public function operationB() {
        echo "ElementB: Operation B\n";
    }
}

// Concrete Visitor
class ConcreteVisitor implements Visitor {
    public function visitElementA(ElementA $elementA) {
        echo "ConcreteVisitor: Visiting ElementA\n";
        $elementA->operationA();
    }

    public function visitElementB(ElementB $elementB) {
        echo "ConcreteVisitor: Visiting ElementB\n";
        $elementB->operationB();
    }
}

// Client Code
$elements = [new ElementA(), new ElementB()];
$visitor = new ConcreteVisitor();

foreach ($elements as $element) {
    $element->accept($visitor);
}
```
