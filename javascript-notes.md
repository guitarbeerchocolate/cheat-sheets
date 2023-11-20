# JavaScript Cheat Sheet (ES6+)

## Variables

var: Declares a variable with function scope.

```
var x = 10;
```

let: Declares a variable with block scope.

```
let y = 20;
```

const: Declares a constant variable with block scope.

```
const z = 30;
```

## Data types

Data Types: JavaScript has dynamic data types, including string, number, boolean, null, undefined, object, and symbol (ES6).

## Conditional Statements

if Statement:

```
if (condition) {
  // code to execute if condition is true
} else {
  // code to execute if condition is false
}
```

switch Statement:

```
switch (value) {
  case 'A':
    // code for case A
    break;
  case 'B':
    // code for case B
    break;
  default:
    // code for other cases
}
```

Loops
for Loop:

```
for (let i = 0; i < 5; i++) {
  // code to repeat
}
```

while Loop:

```
let i = 0;
while (i < 5) {
  // code to repeat
  i++;
}
```

## Functions

Function Declaration:

```
function greet(name) {
  return 'Hello, ' + name + '!';
}
```

Function Expression:

```
const greet = function(name) {
  return 'Hello, ' + name + '!';
};
```

## Arrays

Creating Arrays:

```
const fruits = ['apple', 'banana', 'cherry'];
```

Accessing Elements:

```
const firstFruit = fruits[0];
```

Array Methods:

```
fruits.push('orange'); // Add to end
fruits.pop(); // Remove from end
fruits.shift(); // Remove from start
fruits.unshift('grape'); // Add to start
```

## Objects

Creating Objects:

```
const person = {
  name: 'John',
  age: 30,
};
```

Accessing Properties:

```
const name = person.name;
```

Adding/Modifying Properties:

```
person.email = 'john@example.com';
person.age = 31;
```

## DOM Manipulation

Selecting Elements:

```
const element = document.getElementById('myElement');
```

Modifying Content:

```
element.innerHTML = 'New Content';
```

Adding/Removing Classes:

```
element.classList.add('new-class');
element.classList.remove('old-class');
```

## Event Handling

Adding Event Listeners:

```
element.addEventListener('click', function() {
  // code to execute on click
});
```

## Error Handling

try-catch Statement:

```
try {
  // code that may throw an error
} catch (error) {
  // handle the error
}
```

## Default Function Parameters

Specify default values for function parameters.

```
function greet(name = 'Guest') {
  console.log(`Hello, ${name}!`);
}
```

## Spread Operator

Spread elements of an iterable (e.g., array or object) into another.

```
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];
```

## Proper Class Declarations

Create classes with constructors, methods, and inheritance.

```
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, I'm ${this.name} (${this.age} years old).`);
  }
}

class Student extends Person {
  constructor(name, age, grade) {
    super(name, age);
    this.grade = grade;
  }

  study() {
    console.log(`${this.name} is studying.`);
  }
}
```

## Arrow Functions

Create concise anonymous functions.

```
const add = (a, b) => a + b;
```

## Implicit return for single expressions.

```
const double = x => x * 2;
```

## Promises

Handle asynchronous operations with Promises.

```
const fetchData = () => {
  return new Promise((resolve, reject) => {
    // Asynchronous operation
    if (success) {
      resolve(data);
    } else {
      reject(error);
    }
  });
};

fetchData()
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

## Fetch API

Fetch data from a server using the fetch API.

```
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

## Async and Await

Simplify asynchronous code using async and await.

```
async function fetchAndDisplayData() {
  try {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

fetchAndDisplayData();
```
