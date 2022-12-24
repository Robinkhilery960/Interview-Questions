# Javascript Interview Questions

## 1. What is JSON ?

JSON is a format that is used to represent and exchange data , that too text-based data .JSON follows JS object literal syntax. Even though it closely resembles JavaScript object literal syntax, it can be used independently from JavaScript, and many programming environments feature the ability to read (parse) and generate JSON

JSON exists as a string — useful when you want to transmit data across a network. It needs to be converted to a native JavaScript object when you want to access the data. This is not a big issue — JavaScript provides a global JSON object that has methods available for converting between the two.

A JSON string can be stored in its own file, which is basically just a text file with an extension of `.json`

NOTES:

1. JSON is purely a string with a specified data format—it contains only properties, no methods.
2. JSON requires double quotes to be used around strings and property names. Single quotes are not valid other than surrounding the entire JSON string.
3. JSON can actually take the form of any data type that is valid for inclusion inside JSON, not just arrays or objects. So for example, a single string or number would be valid JSON.
4. Unlike in JavaScript code in which object properties may be unquoted, in JSON only quoted strings may be used as properties.
5. parse(): Accepts a JSON string as a parameter, and returns the corresponding JavaScript object.
6. stringify(): Accepts an object as a parameter, and returns the equivalent JSON string.

### Cross Questions

    1. what is difference between JSON and Object?

## 2. What is a prototype chain ?

**Prototypes** are the mechanisms by which JavaScript objects inherits features from one another

Prototype chaining is used to build new types of objects based on existing ones. It is similar to inheritance in a class based language.

Every object in JavaScript has a built-in property, which is called its **prototype**. The prototype is itself an object, so the prototype will have its own prototype, making what's called a **prototype chain**. The chain ends when we reach a prototype that has `null` for its own prototype.

### Cross Questions:

    1. How you can set Prototype of an object?
    2. What is difference between prototypes ad inheritance ?

## 3. What is the difference between Call, Apply and Bind ?

Normally when we call a function then the value of this , that is passed to function is the object on which we have accessed the function , but if you want to pass your own this you can do that using `call`,`apply` and `bind` methods

Normally, when calling a function, the value of [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
 inside the function is the object that the function was accessed on. With these functions
, you can assign an arbitrary value as `this`
 when calling an existing function, **without first attaching the function to the object as a property**. This allows you to use methods of one object as generic utility functions.

### Call:

```javascript
let person1 = {
  name: " david",
  age: "22",
};
let person2 = {
  name: " Herry",
  age: "23",
};
let showDetail = function (city, car) {
  console.log(
    `${this.name} is ${this.age} years old and he lives in ${city} and drives ${car}`
  );
};

showDetail.call(person2, "noida", "BMW");
showDetail.call(person1, "delhi", "mercedez");
```

### Apply:

```javascript
let person1 = {
  name: " david",
  age: "22",
};
let person2 = {
  name: " Herry",
  age: "23",
};
let showDetail = function (city, car) {
  console.log(
    `${this.name} is ${this.age} years old and he lives in ${city} and drives ${car}`
  );
};
showDetail.apply(person2, ["noida", "BMW"]);
showDetail.apply(person1, ["delhi", "mercedez"]);
```

### Bind:

```javascript
let person1 = {
  name: " david",
  age: "22",
};
let person2 = {
  name: " Herry",
  age: "23",
};
let showDetail = function (city, car) {
  console.log(
    `${this.name} is ${this.age} years old and he lives in ${city} and drives ${car}`
  );
};

let bindshowDetail = showDetail.bind(person2, "noida", "BMW");
console.log(bindshowDetail);
bindshowDetail();
```

**Note:** Call and apply can be interchangeable . Both execute function immediately . Where binds create a new function for you which later on can be invoked whenever you want that.

### Cross Questions

    1. What is this? How does it work?

## 4. Ways to create a Object ?

There are many ways to create objects in javascript as below

1.  **Object constructor:**

    You can create an object using Object Constructor

    ```javascript
    var object = new Object();
    ```

    ### Cross Questions:

        1.  What is a  Constructor ?
        2. What is an Object Constructor

2.  **Object's create method:**

    The create method of Object creates a new object by passing the prototype object as a parameter

    parameters - can be null or any other object

    ```javascript
    var object = Object.create(null);
    ```

3.  **Object literal syntax:**

    The object literal syntax (or object initializer), is a comma-separated set of name-value pairs wrapped in curly braces.

    ```javascript
    var object = {
      name: "Robin",
      age: 23,
    };
    ```

    Object literal property values can be of any data type, including array, function, and nested object.`

    **Note:** This is an easiest way to create an object

4.  **Function constructor:**

    Create any function and apply the new operator to create object instances, using function as a Constructor

    ```javascript
    function Person(name) {
      this.name = name;
      this.age = 21;
    }
    var object = new Person("Sudheer");
    ```

    ### Cross Questions:

        1. What is difference of creating an object from class and creating an object front the function Constructor
        2. Is all the function in JavaScript can be called as Constructor function ?
        3. what is difference between creating an Object from  object literals and creating an object from  function  Constructor
        4. what is this new keyword and what does it do ?

5.  **Function constructor with prototype:**

    This is similar to function constructor but it uses prototype for their properties and methods,

    ```javascript
    function Person() {}
    Person.prototype.name = "Robin";
    var object = new Person();
    ```

    This is equivalent to an instance created with an object create method with a function prototype and then call that function with an instance and parameters as arguments.

    ```javascript
    function func() {}

    new func(x, y, z);
    ```

    **(OR)**

    ```javascript
     // Create a new instance using function prototype.
    var newInstance = Object.create(func.prototype)

    // Call the function
    var result = func.call(newInstance, x, y, z),

    // If the result is a non-null object then use it otherwise just use the new instance.
    console.log(result && typeof result === 'object' ? result : newInstance);
    ```

6.  **ES6 Class syntax:**

    ES6 introduces class feature to create the objects

    ```javascript
    class Person {
      constructor(name) {
        this.name = name;
      }
    }

    var object = new Person("Sudheer");
    ```

## 5. What is the purpose of the array slice method?

Slice methods return you new Array from a given array based upon the start point and end point it gave you a `shallow copy` of given array

```javascript
const arr = [1, 2, [3], 4, 5];
const newArr = arr.slice(0, 3);
console.log(arr);
console.log(newArr);
newArr[2][0] = 15;
console.log(arr);
console.log(newArr);
```

Some methods do not mutate the existing array that the method was called on, but instead return a new array. They do so by first accessing [this.constructor[Symbol.species]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/@@species) to determine the constructor to use for the new array. The newly constructed array is then populated with elements. The copy always happens *[shallowly](https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy)* — the method never copies anything beyond the initially created array. Elements of the original array(s) are copied into the new array as follows:

- Objects: the object reference is copied into the new array. Both the original and new array refer to the same object. That is, if a referenced object is modified, the changes are visible to both the new and original arrays.
- Primitive types such as strings, numbers and booleans (not `String`,  `Number` and `Boolean`  objects): their values are copied into the new array.

Other methods mutate the array that the method was called on, in which case their return value differs depending on the method: sometimes a reference to the same array, sometimes the length of the new array.

## 6. What is the purpose of the array splice method?

The **splice()** method is used either adds/removes items to/from an array, and then returns the removed item. The first argument specifies the array position for insertion or deletion whereas the optional second argument indicates the number of elements to be deleted. Each additional argument is added to the array.

Some of the examples of this method are,

```javascript
let arrayIntegersOriginal1 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal2 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal3 = [1, 2, 3, 4, 5];

let arrayIntegers1 = arrayIntegersOriginal1.splice(0, 2); // returns [1, 2]; original array: [3, 4, 5]
let arrayIntegers2 = arrayIntegersOriginal2.splice(3); // returns [4, 5]; original array: [1, 2, 3]
let arrayIntegers3 = arrayIntegersOriginal3.splice(3, 1, "a", "b", "c"); //returns [4]; original array: [1, 2, 3, "a", "b", "c", 5]
```

The `splice()` method is a [mutating method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#copying_methods_and_mutating_methods). It may change the content of `this`. If the specified number of elements to insert differs from the number of elements being removed, the array's `length` will be changed as well. At the same time, it uses [@@species](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/@@species) to create a new array instance to be returned.

If the deleted portion is [sparse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections#sparse_arrays), the array returned by `splice()` is sparse as well, with those corresponding indices being empty slots.

The `splice()` method is [generic](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#generic_array_methods). It only expects the `this` value to have a `length` property and integer-keyed properties. Although strings are also array-like, this method is not suitable to be applied on them, as strings are immutable.

---

| Slice                                        | Splice                                          |
| -------------------------------------------- | ----------------------------------------------- |
| Doesn't modify the original array(immutable) | Modifies the original array(mutable)            |
| Returns the subset of original array         | Returns the deleted elements as array           |
| Used to pick the elements from array         | Used to insert or delete elements to/from array |

## 7. Objects vs Maps

Object is similar to Map—both let you set keys to values, retrieve those values, delete keys, and detect whether something is stored at a key.

However, there are important differences that make Map preferable in some cases:

1. The keys of an Object are Strings and Symbols, whereas they can be any value for a Map, including functions, objects, and any primitive.
2. The keys in Map are ordered while keys added to Object are not. Thus, when iterating over it, a Map object returns keys in order of insertion.
3. You can get the size of a Map easily with the size property, while the number of properties in an Object must be determined manually.
4. A Map is an iterable and can thus be directly iterated, whereas iterating over an Object requires obtaining its keys in some fashion and iterating over them.
5. An Object has a prototype, so there are default keys in the map that could collide with your keys if you're not careful.
6. A Map may perform better in scenarios involving frequent addition and removal of key pairs.

## 8. == Vs ===

The **equality (`==`)**
 operator checks whether its two operands are equal, returning a Boolean result. Unlike the [strict equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Strict_equality)
 operator, it attempts to convert and compare operands that are of different types.

The equality operators (`==` and `!=`) provide the IsLooselyEqual semantic. This can be roughly summarized as follows:

1. If the operands have the same type, they are compared as follows:
   - Object: return `true` only if both operands reference the same object.
   - String: return `true` only if both operands have the same characters in the same order.
   - Number: return `true` only if both operands have the same value. `+0` and `0` are treated as the same value. If either operand is `NaN`, return `false`; so, `NaN` is never equal to `NaN`.
   - Boolean: return `true` only if operands are both `true` or both `false`.
2. If one of the operands is `null` or `undefined`, the other must also be `null` or `undefined` to return `true`. Otherwise return `false`.
3. If one of the operands is an object and the other is a primitive, [convert the object to a primitive](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#primitive_coercion).
4. At this step, both operands are converted to primitives (one of String, Number, Boolean, Symbol, and BigInt). The rest of the conversion is done case-by-case.
   - If they are of the same type, compare them using step 1.
   - If one of the operands is a Symbol but the other is not, return `false`.
   - If one of the operands is a Boolean but the other is not, [convert the boolean to a number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number#number_coercion): `true` is converted to 1, and `false` is converted to 0. Then compare the two operands loosely again.
   - Number to String: [convert the string to a number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number#number_coercion). Conversion failure results in `NaN`, which will guarantee the equality to be `false`.

The **strict equality (`===`)**
 operator checks whether its two operands are equal, returning a Boolean result. Unlike the [equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Equality)
 operator, the strict equality operator always considers operands of different types to be different.

The strict equality operators (`===` and `!==`) provide the [IsStrictlyEqual](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness#strict_equality_using) semantic.

- If the operands are of different types, return `false`.
- If both operands are objects, return `true` only if they refer to the same object.
- If both operands are `null` or both operands are `undefined`, return `true`.
- Otherwise, compare the two operand's values:
  - Numbers must have the same numeric values. `+0` and `0` are considered to be the same value.
  - Strings must have the same characters in the same order.
  - Booleans must be both `true` or both `false`.

Some of the example which covers the above cases,

```javascript
0 == false   // true
0 === false  // false
1 == "1"     // true
1 === "1"    // false
null == undefined // true
null === undefined // false
'0' == false // true
'0' === false // false
[]==[] or []===[] //false, refer different objects in memory
{}=={} or {}==={} //false, refer different objects in memory
```

### Cross Questions:

    1. What is type coercion?
    2. How type coercion is happening in equality operator?

### More to read:

1. [Type Coercion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#type_coercion)

## 9. What are arrow function and where to not use them ?

An arrow function is a shorter syntax for a function expression and does not have its own this so don't use arrow function as object methods, Event handlers, Prototype methods. Arrow function don't have argument object so also not use them for functions that use the arguments object.
Arrow functions also does not have new.target keyword so also don't use them as Constructor functions

### Object methods:

```javascript
const counter = {
  count: 0,
  next: () => this.count + 1,
  current: () => this.count,
};
console.log(counter.next()); // NaN
```

The counter object has two methods: current() and next(). The current() method returns the current counter value and the next() method returns the next counter value.
The reason is that when you use the arrow function inside the object, it inherits the this value from the enclosing lexical scope which is the global scope in this example.

The this.count inside the next() method is equivalent to the window.count (in the web browser).

The window.count is undefined by default because the window object doesn’t have the count property. The next() method adds one to undefined that results in NaN.

### Constructor :

Whenever you uses any function as a Constructor function then prototype property of that Constructor is set as prototype of created object and this prototype property contains the Constructor , but in case of arrow function this is missing so you cant use arrow function as Constructor and also arrow function does not have new.target so it will never know that it is called with new keyword or not.

```javascript
const Car = (make, model, year) => {
  this.make = make;
  this.model = model;
  this.year = year;
};
Car.prototype;
// undefined
```

### Prototype methods:

```javascript
function Counter() {
  this.count = 0;
}

Counter.prototype.next = () => {
  return this.count + 1;
};

const count = new Counter();
count.next();
console.log(count); // {count:0}
```

he `this` value in next() method reference the global object. Since you want the this value inside the methods to reference the Counter object, you need to use the regular functions instead:

### Functions that use the arguments object:

```javascript
const sum = (a, b) => {
  console.log(argument);
};
sum(1, 2); // ReferenceError: argument is not defined
```

Arrow functions don’t have the arguments object. Therefore, if you have a function that uses arguments object, you cannot use the arrow function.

### Event handlers:

Suppose that you have the following input text field and you want to show a greeting message when users type their usernames. The following shows the <div> element that will display the greeting message.
Once users type their usernames, you capture the current value of the input and update it to the <div> element.

HTML:

```html
<input
  type="text"
  name="username"
  id="username"
  placeholder="Enter a username"
/>
<div id="greeting"></div>
```

JS:

```javascript
const greeting = document.querySelector("#greeting");
const username = document.querySelector("#username");
username.addEventListener("keyup", () => {
  greeting.textContent = "Hello " + this.value;
});
```

However, when you execute the code, you will get the following message regardless of whatever you type:

```text
Hello undefined
```

Code language: JavaScript (javascript)
It means that the this.value in the event handler always returns undefined.

As mentioned earlier, the arrow function doesn’t have its own this value. It uses the this value of the enclosing lexical scope. In the above example, the this in arrow function references the global object.

In the web browser, the global object is window. The window object doesn’t have the value property. Therefore, the JavaScript engine adds the value property to the window object and sets its values to undefined.

## 10. What is closure?

A closure is the combination of a function and the lexical environment within which that function was declared.
In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

```javascript
const outer = function () {
  const fruit = "mango";
  function inner() {
    console.log(fruit);
  }
  return inner;
};

const result = outer();
result();
```

In this case, result is a reference to the instance of the function inner that is created when outer run. The instance of inner maintains a reference to its lexical environment, within which the variable name exists.
This environment consists of any local variables that were in-scope at the time the closure was created

## 11. What does Lexical scope means?

Lexical scope means the scope in which a item is created . In other words area where your item definition lies is called lexical scope of that item .Any item is accessible to the code which is in its lexical scope .

```javascript
// Define a function:
function showLastName() {
  const lastName = "Khilery";
  return lastName;
}

// Define another function:
function displayFullName() {
  const fullName = "Robin " + lastName;
  return fullName;
}

// Invoke displayFullName():
console.log(displayFullName());

// The invocation above will return:
//Uncaught ReferenceError: lastName is not defined
```

Notice that the invocation of displayFullName() in the snippet above returned an Uncaught ReferenceError. The error returned because only code within an item's lexical scope can access the item.

Therefore, neither the displayFullName() function nor its internal code can access the lastName variable because lastName got defined in a different scope.

In other words, lastName’s lexical scope is different from that of displayFullName()

## 12. What is First- Class-Function?

A programming language is said to have First-class functions when functions in that language are treated like any other variable. For example, in such a language, a function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable.

```javascript
    // assigning function to variable
   const greet=function(){
    console.log("Hola")
   }
   // passing function as parameter
   const sayHola=(greet){
   console.log(greet())
   }
   // returning a function
    const sayHola=( ){
     return function(){
    console.log("Hola")
   }
   }
```

## 13. First Order vs Higher Order functions

### First-order:

First-order function is a function that doesn’t accept another function as an argument and doesn’t return a function as its return value.

```javascript
const greet = function () {
  console.log("Hola");
};
```

### Higer order:

Higher-order function is a function that accepts another function as an argument or returns a function as a return value or both

```javascript
// passing function as parameter
  const sayHola=(greet){
  console.log(greet())
  }
  // returning a function
   const sayHola=( ){
    return function(){
   console.log("Hola")
  }
  }
```

## 14. What is curring in JavaScript ?

Currying refers to the process of transforming a function with multiple number of arguments into the same function with less number of arguments

```javascript
const unCurryFunction = (a, b, c) => {
  return a + b + c;
};
console.log(unCurryFunction(1, 2, 3));

const curryFunction = (a) => (b) => (c) => a + b + c;
console.log(curryFunction(1)(2)(3));
```

## 15. Pure Function

A function must pass two tests to be considered pure:

1. Same inputs always return same outputs
2. No side-effect
   ```text
   1. Mutating your input
   2. console.log
   3. HTTP calls (AJAX/fetch)
   4. Changing the filesystem (fs)
   5. Querying the DOM
   ```

```javascript
// pure function
const add = (x, y) => x + y;
add(2, 4); // 6

// impure function
 let y=5;
 add(x)=>{
    y=y+1;
    return x+y
 }
```

## 16. let, var and const

### Scope:

Scope refers to the part of a program where we can access a variable

### var :

Variables declared with var keyword are either function scoped or global scope depending upon where they are declared.Initialization of variables is optional.
Variables declared using var are created before any code is executed in a process known as hoisting. Their initial value is undefined.
re-declaration, reassigning is possible in same scope

```javascript
console.log(name); // undefined
var name = "robin";
console.log(name); // robin
var name = "sunil";
console.log(name); // sunil
var x = 10;
function add() {
  var x = 12;
  var y = 10;
  console.log(x + y); // 22
}
add();
{
  var y = 20;
}
console.log(y); // 20 not a block scope
```

### let :

Variable declared with this keyword are block scope and initializing it to a value is optional.
Variable declared with let can only be accessed after its declaration is reached because of Temporal Dead Zone.
Redeclaring the same variable within the same function or block scope raises a SyntaxError while reassigning can be done

```javascript
var a = 1;
var b = 2;

if (a === 1) {
  var a = 11; // the scope is global
  let b = 22; // the scope is inside the if-block

  console.log(a); // 11
  console.log(b); // 22
}

console.log(a); // 11
console.log(b); // 2

let x = 1;

{
  var x = 2; // SyntaxError for re-declaration
}
```

### const:

Variable declared with this keyword are block scope and they cannot be redeclare and reassigned and initializer for a constant is required. However, if a constant is an object or array its properties or items can be updated or removed.

```javascript
// define MY_FAV as a constant and give it the value 7
const MY_FAV = 7;

// this will throw an error - Uncaught TypeError: Assignment to constant variable.
MY_FAV = 20;

// MY_FAV is 7
console.log("my favorite number is: " + MY_FAV);

// trying to redeclare a constant throws an error
// Uncaught SyntaxError: Identifier 'MY_FAV' has already been declared
const MY_FAV = 20;

// the name MY_FAV is reserved for constant above, so this will fail too
var MY_FAV = 20;

// this throws an error too
let MY_FAV = 20;

// Attempting to overwrite the object throws an error "Assignment to constant variable".
const MY_OBJECT = { key: "value" };
MY_OBJECT = { OTHER_KEY: "value" };

// Works fine
MY_OBJECT.key = "otherValue";

//. Assigning a new array to the variable throws an error "Assignment to constant variable
const MY_ARRAY = [];
MY_ARRAY = ["B"];

// Works fine
MY_ARRAY.push("A"); // ["A"]
```

## 17. What is Hoisting ?

Javascript hoisting refer to the process where declaration of functions, variables or classes move to the top of their scope before execution of the code.. Remember that JavaScript only hoists declarations, not initialization

### Variable Hoisting:

Variables declaration are hoisted to top of their scope.Undeclared variables do not exist until code assigning them is executed.Therefore, assigning a value to an undeclared variable implicitly creates it as a global variable when the assignment is executed. This means that, all undeclared variables are global variables.

```javascript
console.log(typeof variable); // undefined
console.log(variable); // Reference error - when try to access an undeclared  variable

console.log(hoist); // Output: undefined

var hoist = "The variable has been hoisted.";

function hoist() {
  console.log(message);
  var message = "Hoisting is all the rage!";
}

hoist(); // Output: undefined

// let keyword
console.log(hoist); // Output: ReferenceError: hoist is not defined ...
let hoist = "The variable has been hoisted.";

// const keyword
console.log(hoist); // Output: ReferenceError: hoist is not defined
const hoist = "The variable has been hoisted.";
```

### Function Hoisting:

### Function declaration:

The function declaration defines a function with the specified parameters.A function created with a function declaration is a Function object and has all the properties, methods and behavior of Function objects.Function declarations in JavaScript are hoisted to the top of the enclosing function or global scope. You can use the function before you declared it:

```javascript
hoisted(); // Logs "foo"
function hoisted() {
  console.log("foo");
}
```

### Function expression:

The function keyword can be used to define a function inside an expression.A function created with a function expression is a Function object and has all the properties, methods and behavior of Function objects.
Function expressions in JavaScript are not hoisted, unlike function declarations. You can't use function expressions before you create them:

```javascript
console.log(notHoisted); // undefined
// Even though the variable name is hoisted,
// the definition isn't. so it's undefined.
notHoisted(); // TypeError: notHoisted is not a function

var notHoisted = function () {
  console.log("bar");
};
```

## 18. What is Temporal Dead Zone

TDZ describe a state for let and const , where they are in scope but they cannot be accessed before they are declared .

```javascript
{
  // This is the temporal dead zone for the age variable!
  // This is the temporal dead zone for the age variable!
  let age = 25; // Whew, we got there! No more TDZ
  console.log(age);
}
```

### What's the difference between declaring and initializing?

Declaring a variable means we reserve the name in memory at the current scope. That is labelled 1 in the comments.

Initializing a variable is setting the value of the variable. That is labelled 2 in the comments.

```javascript
function scopeExample() {

    let age; // 1
    age = 20; // 2
    let hands = 2; // 3

```

### Why TDZ Happens ?

When variables get hoisted, var gets undefined initialized to its value by default in the process of hoisting. let and const also get hoisted, but don't get set to undefined when they get hoisted.
The only difference between const and let is that when they are hoisted, their values don't get defaulted to undefined.

Just to prove let and const also hoist, here's an example:

```javascript
{
  // Both the below variables will be hoisted to the top of their scope!
  console.log(typeof nonsenseThatDoesntExist); // Prints undefined
  console.log(typeof name); // Throws an error, cannot access 'name' before initialization

  let name = "Kealan";
}
```

The above snippet is proof that let is clearly hoisted above where it was declared, as the engine alerts us to the fact. It knows name exists (it's declared), but we can't access it before it is initialized.

## 19. Functions

A function is a set of statements that take inputs, do some specific computation, and produce output.In JavaScript, functions are first-class objects, because they can have properties and methods just like any other object. What distinguishes them from other objects is that functions can be called. In brief, they are Function objects.For constructor function default return value is `this` keyword and for other function it is undefined.
Arguments may be passed by value (in the case of primitive values) or by reference (in the case of objects).The this keyword does not refer to the currently executing function, so you must refer to Function objects by name, even within the function body.
Functions created with the Function constructor do not create closures to their creation contexts; they always are created in the global scope. When running them, they will only be able to access their own local variables and global ones, not the ones from the scope in which the Function constructor was created.

## 20. Getters and Setters:

### Getters:

Sometime you want to reflect over the status of internal variable without explicitly calling a method that can be accomplished with help of Getter.The get syntax binds an object property to a function that will be called when that property is looked up.

```javascript
const obj = {
  log: ["a", "b", "c"],
  get latest() {
    return this.log[this.log.length - 1];
  },
};

console.log(obj.latest);
// expected output: "c"
```

Note the following when working with the get syntax:

1. It can have an identifier which is either a number or a string;
2. It must have exactly zero parameters
3. It must not appear in an object literal with another get e.g. the following is forbidden

```javascript
    {
      get x() { }, get x() { }
    }
```

4. It must not appear with a data entry for the same property e.g. the following is forbidden

```javascript
    {
      x: /* … */, get x() { /* … */ }
    }
```

### Setters

The set syntax binds an object property to a function to be called when there is an attempt to set that property.

```javascript
const language = {
  set current(name) {
    this.log.push(name);
  },
  log: [],
};
language.current = "EN";
console.log(language.log); // ['EN']
language.current = "FA";
console.log(language.log); // ['EN', 'FA']
```

Note the following when working with the set syntax:

1. It can have an identifier which is either a number or a string;
2. It must have exactly one parameter

## 21 destructuring

The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

```javascript
let a, b, rest;
[a, b] = [10, 20];

console.log(a);
// expected output: 10

console.log(b);
// expected output: 20

[a, b, ...rest] = [10, 20, 30, 40, 50];

console.log(rest);
// expected output: Array [30,40,50]
```

You can end a destructuring pattern with a rest property ...rest. This pattern will store all remaining properties of the object or array into a new object or array.

## 22. rest and spread operator

When you don't know that how many arguments are supplied to your function then you can use rest parameter there to accept those arguments.
A function definition's last parameter can be prefixed with ... which will cause all remaining (user supplied) parameters to be placed within an Array object.

```javascript
function myFun(a, b, ...manyMoreArgs) {
  console.log("a", a);
  console.log("b", b);
  console.log("manyMoreArgs", manyMoreArgs);
}

myFun("one", "two", "three", "four", "five", "six");

// Console Output:
// a, one
// b, two
// manyMoreArgs, ["three", "four", "five", "six"]
```

A function definition can only have one rest parameter, and the rest parameter must be the last parameter in the function definition.

```javascript
function wrong1(...one, ...wrong) {}
function wrong2(...wrong, arg2, arg3) {}
```

### spread syntax:

The spread operator is just 3 dots ...
It can be used on iterables like an array or a string.
It expands an iterable to its individual elements
It can provide a function call with an array (or any other iterable) where 0 or more arguments were expected.
There are three distinct places that accept the spread syntax:

1. Function arguments list:`(myFunction(a, ...iterableObj, b))`
2. Array literals:`([1, ...iterableObj, '4', 'five', 6])`
3. Object literals: `({ ...obj, key: 'value' })`

`Only` iterable objects, like Array, can be spread in array and function parameters. Many objects are not iterable, including all plain objects that lack a Symbol.iterator method:

```javascript
const obj = { key1: "value1" };
const array = [...obj]; // TypeError: obj is not iterable
```

On the other hand, spreading in object literals enumerates the own properties of the object. For typical arrays, all indices are enumerable own properties, so arrays can be spread into objects.

```javascript
const array = [1, 2, 3];
const obj = { ...array }; // { 0: 1, 1: 2, 2: 3 }
```

### SeeAlso:

[Spread Syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#try_it)

## 23. rest parameter vs argument object

### rest parameter:

1. The arguments object is not a real array, while rest parameters are Array instances, meaning methods like sort(), map(), forEach() or pop() can be applied on it directly.
2. The rest parameter bundles all the extra parameters into a single array, but does not contain any named argument defined before the ...restParam. The arguments object contains all of the parameters — including the parameters in the ...restParam array — bundled into one array-like object

## 24. new keyword

New keyword let you define a new instance of a user defined object type or in-built object type that has a constructor function.

```javascript
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}

const car1 = new Car("Eagle", "Talon TSi", 1993);

console.log(car1.make);
// expected output: "Eagle"
```

When a function is called with the new keyword, the function will be used as a constructor. new will do the following things:

1. Creates a blank, plain JavaScript object. For convenience, let's call it newInstance.
2. Points newInstance's [[Prototype]] to the constructor function's prototype property, if the prototype is an Object. Otherwise, newInstance stays as a plain object with Object.prototype as its [[Prototype]].

```text
Note:Properties/objects added to the constructor function's prototype property are therefore accessible to all instances created from the constructor function.
```

3. Executes the constructor function with the given arguments, binding newInstance as the this context (i.e. all references to this in the constructor function now refer to newInstance).
4. If the constructor function returns a non-primitive, this return value becomes the result of the whole new expression. Otherwise, if the constructor function doesn't return anything or returns a primitive, newInstance is returned instead. (Normally constructors don't return a value, but they can choose to do so to override the normal object creation process.)

Classes can only be instantiated with the new operator — attempting to call a class without new will throw a TypeError.

A function can know whether it is invoked with new by checking new.target. new.target is only undefined when the function is invoked without new.

## 25. What is IIFE(Immediately Invoked Function Expression)

IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined. The signature of it would be as below,

```javascript
(function () {
  // logic here
})();
```

The primary reason to use an IIFE is to obtain data privacy because any variables declared within the IIFE cannot be accessed by the outside world. i.e, If you try to access variables with IIFE then it throws an error as below,

```javascript
(function () {
  var message = "IIFE";
  console.log(message);
})();
console.log(message); //Error: message is not defined
```

## 26. How do you decode or encode a URL in JavaScript

For encoding and decoding purpose we mainly uses UTF-8 format.UTF-8 means `Unicode Transformation Format - 8 bits`.It is an formate in which each code point will be assigned memory and these codepoints are specific to each character for some character UTF-8 uses 1 byte ,for some 2 or 3 or for some also 4. We uses mainly UTF-8 because it decreases your file size as much as it can.

`encodeURI()` function is used to encode an URL. This function requires a URL string as a parameter and return that encoded string.

`decodeURI() `function is used to decode an URL. This function requires an encoded URL string as parameter and return that decoded string.

```text
Note: If you want to encode characters such as / ? : @ & = + $ # then you need to use encodeURIComponent().
```

```javascript
let uri = "employeeDetails?name=john&occupation=manager";
let encoded_uri = encodeURI(uri);
let decoded_uri = decodeURI(encoded_uri);
```

## 27. What is memoization

In programming, memoization is an optimization technique that makes applications more efficient and hence faster. It does this by storing computation results in cache, and retrieving that same information from the cache the next time it's needed instead of computing it again.

```javascript
// without memoization
//we're executing fib(0), fib(1), fib(2) and fib(3) multiple times
const fib = (n) => {
  if (n <= 1) return 1;
  return fib(n - 1) + fib(n - 2);
};
fib(5); // 120

// with memoization
//we're not executing fib(0), fib(1), fib(2) and fib(3) multiple times we stores them first time as we calculated them
const fib = (n, memo) => {
  memo = memo || {};
  if (memo[n]) return memo[n];
  if (n <= 1) return 1;
  return (memo[n] = fib(n - 1, memo) + fib(n - 2, memo));
};
fib(5); // 120
```

## 28.Classes:

Classes are a template for creating objects.Class declarations and Class expressions both are hoisted but they they are not initialized so you cannot access them before defining them .The body of a class is executed in strict mode.The constructor method is a special method for creating and initializing an object created with a class. There can only be one special method with the name "constructor" in a class.The static keyword defines a static method or property for a class. Static members (properties and methods) are called without instantiating their class and cannot be called through a class instance.
classes are under the hoods actually function with the same prototype as the constructor have .

### Classes are nothing but syntactic sugar:

### Modern classes:

```javascript
class Animal {
  constructor(name, weight) {
    this.name = name;
    this.weight = weight;
  }

  eat() {
    return `${this.name} is eating!`;
  }

  sleep() {
    return `${this.name} is going to sleep!`;
  }

  wakeUp() {
    return `${this.name} is waking up!`;
  }
}

// Classes under the hoods are actually function
console.log(typeof Animal); //function

class Gorilla extends Animal {
  constructor(name, weight) {
    super(name, weight);
  }

  climbTrees() {
    return `${this.name} is climbing trees!`;
  }

  poundChest() {
    return `${this.name} is pounding its chest!`;
  }

  showVigour() {
    return `${super.eat()} ${this.poundChest()}`;
  }

  dailyRoutine() {
    return `${super.wakeUp()} ${this.poundChest()} ${super.eat()} ${super.sleep()}`;
  }
}

function display(content) {
  console.log(content);
}

const gorilla = new Gorilla("George", "160Kg");
display(gorilla.poundChest());
display(gorilla.sleep());
display(gorilla.showVigour());
display(gorilla.dailyRoutine());

// OUTPUT:
// George is pounding its chest!
// George is going to sleep!
// George is eating! George is pounding its chest!
// George is waking up! George is pounding its chest!  George is eating! George is going to sleep!
```

### Traditional Classes:

```javascript
function Animal(name, weight) {
  this.name = name;
  this.weight = weight;
}

Animal.prototype.eat = function () {
  return `${this.name} is eating!`;
};

Animal.prototype.sleep = function () {
  return `${this.name} is going to sleep!`;
};

Animal.prototype.wakeUp = function () {
  return `${this.name} is waking up!`;
};

function Gorilla(name, weight) {
  Animal.call(this, name, weight);
}

Gorilla.prototype = Object.create(Animal.prototype);
Gorilla.prototype.constructor = Gorilla;

Gorilla.prototype.climbTrees = function () {
  return `${this.name} is climbing trees!`;
};

Gorilla.prototype.poundChest = function () {
  return `${this.name} is pounding its chest!`;
};

Gorilla.prototype.showVigour = function () {
  return `${Animal.prototype.eat.call(this)} ${this.poundChest()}`;
};

Gorilla.prototype.dailyRoutine = function () {
  return `${Animal.prototype.wakeUp.call(
    this
  )} ${this.poundChest()} ${Animal.prototype.eat.call(
    this
  )} ${Animal.prototype.sleep.call(this)}`;
};

function display(content) {
  console.log(content);
}

var gorilla = new Gorilla("George", "160Kg");
display(gorilla.poundChest());
display(gorilla.sleep());
display(gorilla.showVigour());
display(gorilla.dailyRoutine());

// OUTPUT:
// George is pounding its chest!
// George is going to sleep!
// George is eating! George is pounding its chest!
// George is waking up! George is pounding its chest! George is eating! George is going to sleep!
```

## 29. Modules

JavaScript modules allow you to break up your code into separate files. This makes it easier to maintain the code-base.JavaScript modules rely on the `import` and `export` statements.
Modules increase Maintainability,Reusability and
Name spacing of your code.

### CommonJS modules and ES modules

### CommonJS:

By default, Node.js treats JavaScript code as CommonJS modules. Because of this, CommonJS modules are characterized by the require() statement for module imports and module.exports for module exports.

```javascript
module.exports.add = function (a, b) {
  return a + b;
};

module.exports.subtract = function (a, b) {
  return a - b;
};
```

We can also import the public functions into another Node.js script using require(), just as we do here:

```javascript
const { add, subtract } = require("./util");

console.log(add(5, 5)); // 10
console.log(subtract(10, 5)); // 5
```

### ES Module:

We can also simply enable ES modules in a Node.js package by changing the file extensions from .js to .mjs.

```javAscript
export function add(a, b) {
        return a + b;
}

export function subtract(a, b) {
        return a - b;
}
```

We can then import both functions using the import statement:

```javascript
// app.mjs

import { add, subtract } from "./util.mjs";

console.log(add(5, 5)); // 10
console.log(subtract(10, 5)); // 5
```

Another way to enable ES modules in your project can be done by adding a "type: module" field inside the nearest package.json file (the same folder as the package you’re making):

### See Also [CommonJS vs ES](https://blog.logrocket.com/commonjs-vs-es-modules-node-js/)

## 30. Cookies:

Cookies are key value pair that are stored on your website by a browser that can be used to better a user's web experience.

```javascript
//set a cookie on the client side
document.cookie = "dark_mode=true";

// set an expiration date on a cookie
document.cookie = "dark_mode=true; expires= 25 Dec 2022 00:00:00 GMT"; // expires 1 week from now

// OR

document.cookie = "dark_mode=true; max-age=604800"; // expires 1 week from now

// update a cookie
document.cookie = "dark_mode=false; max-age=604800"; // expires 1 week from now

// set the path for a cookie
document.cookie = "dark_mode=true; path=/about";

//delete a cookie
document.cookie = "dark_mode=true; expires= 11 Dec 2022 00:00:00 GMT"; // 1 week earlier

//OR

document.cookie = "dark_mode=true; max-age=-60"; // 1 minute earlier
```

### Cookie Limitations:

1. Cookies are quite limited compared to some modern alternatives to storing data in the browser like localStorage or sessionStorage and their small size makes it easy for the browser to send cookies with each request to the server. browsers only allow cookies to work from one domain for security reasons.

2. Man-in-the-middle attacks:[Read Here](https://www.invicti.com/blog/web-security/man-in-the-middle-attack-how-avoid/)
3. Cross Site Scripting: [Read Here](https://portswigger.net/web-security/cross-site-scripting)
4. CSRF attacks:[Read Here](https://portswigger.net/web-security/csrf)

### Read Also:[Click here](https://www.freecodecamp.org/news/everything-you-need-to-know-about-cookies-for-web-development/)

## 31. Web Storage API:

Web Storage provides you two mechanisms sessionStorage and localStorage that maintains a separate storage area for each given origin.
Local storage and session Storage are a properties of window object that are used to access storage object and storage object is used to access current origin's storage area by the defined methods

### local Storage Vs Session Storage:-

sessionStorage:

1. storage area is available for the duration of the page session (as long as the browser is open, including page reloads and restores).
2. Stores data only for a session, meaning that the data is stored until the browser (or tab) is closed.
3. Data is never transferred to the server.
   Storage limit is larger than a cookie (at most 5MB).
   localStorage:
4. It persist even when the browser is closed and reopened.
5. Stores data with no expiration date, and gets cleared only through JavaScript, or clearing the Browser cache / Locally Stored Data.
6. Storage limit is the maximum amongst the two.

```javascript
// local storage
// set item in local storage
localStorage.setItem("name", "robin");
localStorage.setItem("myFriend", "sunil");
// get item from local storage
localStorage.getItem("name");
// remove item from local storage
localStorage.removeItem("name");
// to clear local storage
localStorage.clear();
// store array in local storage
const arr = [1, 2, 3, 4, 5];
// make array a string and store
localStorage.setItem("arr", JSON.stringify(arr));
// get back array and parse back
localStorageOutput = JSON.parse(localStorage.getItem("arr"));

//session storage'
// set item to session storage
sessionStorage.setItem("name", "sunil");
sessionStorage.setItem("myFriend", "robin");
// get item from session storage
sessionStorage.getItem("name");
// remove item from session storage
sessionStorage.removeItem("name");
// clear session storage
sessionStorage.clear();
// store an array in  session storage
const sessionArr = ["a", "b", "c", "d", "e"];
sessionStorage.setItem("arr", JSON.stringify(sessionArr));
console.log(JSON.parse(sessionStorage.getItem("arr")));
```

## 32.IndexDB

An non-rational key value database for client side tp storage significant amounts of structured data, including files/blobs.
Advantages of IndexDB:

1. IndexedDB is asynchronous, meaning it does not stop the user interface from rendering while the data loads.
2. It allows you to categorize your data using object stores.
3. It allows you to store large amounts of data.
4. It supports objects like videos, images, and so on – any object that supports a structured clone algorithm.
5. It supports database transactions and versioning.
6. It has great performance.
7. The database is private to an origin.
8. It is supported on all modern browsers.

```javascript
// a global object that gives to access of database - connect to database with  this open method
const indexDB = window.indexedDB;

let db;
// request object   given to you immediately and opening of database goes async
const requestObject = indexedDB.open("todo");

requestObject.onupgradeneeded = (e) => {
  // called when database already don't exist or database version greater then current version
  db = requestObject.result;
  // creating a object store and providing a unique key in option that will help to find objects
  db.createObjectStore("personalNotes", { keyPath: "title" });
  db.createObjectStore("workNotes", { keyPath: "title" });
};

// this success function will be called every time till provided version >= current version
requestObject.onsuccess = (e) => {
  db = requestObject.result;
  // add note to object store
  addNote();
};

const addNote = () => {
  // create a note
  const note = {
    title: "note1",
    text: "i am first note",
  };
  // open a transaction on a object store and mention mode of transaction
  const tx = db.transaction("personalNotes", "readwrite");
  // get that object store
  const personalNotes = tx.objectStore("personalNotes");
  // made a request to add a new note to object store
  const storeRequest = personalNotes.add(note);

  storeRequest.onsuccess = () => {
    console.log("note added successfully");
  };
};

// retrieve data from index db
// loading takes some time so use settimeout
setTimeout(() => {
  if (db) {
    // open a transaction on a object store and mention mode of transaction
    const tx = db.transaction("personalNotes", "readonly");
    // get that object store
    const personalNotes = tx.objectStore("personalNotes");
    // made a request to get data object store
    const storeRequest = personalNotes.getAll();
    storeRequest.onsuccess = (e) => {
      console.log(e.target.result);
    };
  }
}, 100);
```

## 33. Aynsc Javascript

Asynchronous programming is a form of parallel programming that does not blocks your code flow means your multiple tasks can be done at a time.
To perform asynchronous programming in javascript we specially uses 3 things callbacks ,promises and async-await .

1. callbacks function:A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

### Callback hell

Nesting multiple callbacks within a function is called a callback hell.It makes the code very difficult to understand and maintain.call-back hell and inversion of control - control, of your code is not in your hand you are actually giving your function to an anther function that is not written by you and you are expecting that magically that outer function will call you inner
function after a certain time, but is the guaranteed that it will only call it once or what is guarantee that it will call even once?

```javascript
firstFunction(function () {
  secondFunction(function () {
    thirdFunction(function () {
      // And so on
    });
  });
});
```

### Promise:

Promise is a object that represents the eventual completion or failure of a asynchronous function  
Asynchronous function will start its operation and it will return you a promise object , and through this promise object you can add handlers on eventual state of promise.It will be in one of the 3 possible states: fulfilled, rejected, or pending.

```javascript
// fetch an async operation return a promise object to you
const fetchPromise = fetch(
  "https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json"
);
// initial state of this promise will be pending
console.log(fetchPromise);
// when promise will be resolved this means that your fetch function  do its work successfully without errors then a then method is called on fulfilled state of promise
// response object will be send to this handler
fetchPromise
  .then((response) => {
    console.log(`Received response: ${response.status}`);
  })
  .catch((error) => {
    // error handling
    console.error(`Could not get products: ${error}`);
  });
console.log("Started request…");
/* 
o/p: 
Promise { <state>: "pending" }
Started request…
Received response: 200
 */
```

### Transition from callbacks to promise based

Traditional callback :
In callback they are called when a particular task has given you output either it result or it is an error you callback will be called so the point is callbacks are executed after a certain time of interval with the result value the same cab be achieved through promises how instead of giving these output values to the callback directly what happens if if gave them to promise and when i receive a value from the async function I can use that value by attaching some handlers over it this whole work of tieing outcome to a promise from a callback is done by executer function that is a solo parameter for the Promise constructor.

```javascript
readFile("hello.text", (error, result) => {
  // this code will execute only after file is read and you got either the result or error
});
// this part of code won't wait for you to read file making it as asynchronous function
```

### Creating Promises:

Syntax:

```javascript
new Promise(executor);
```

FLOW:

1.  Whenever your Promise constructor actually create new promise object at that time it also creates two function called resolve and reject functions those are bind to your newly created promise object.
2.  Inside the executer function you actually do your Asynchronous task with the help of callback - yes we uses here callback you cannot avoid callbacks - these callbacks are actually defined inside your executer function so these have access to resolve and reject functions.
3.  As soon as a promise is created with promise constructor this executer function is called `synchronously` with arguments as resolve and reject functions
4.  Eventual completion of the asynchronous function will be communicated with the promise instance by your resolve and reject method.  
    4.a Once you called any of resolve or reject function your promise get resolve after that whatever number of time you want to call thses functions your promise state wont change

        4.b Promise resolve does not mean that its state will be either fulfilled or rejected it can be pending also depends upon what you have send as paramter to resolve function if you have sent a new promise then its state will still remain dependend on state of new promise

5.  Once your promise get settled it will call further handlers attached to it like then and catch and will pass them fullfilled value or rejection reson as input

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("foo");
  }, 300);
});

promise1.then((value) => {
  console.log(value);
  // expected output: "foo"
});

console.log(promise1);
// expected output: [object Promise]
```

### Async-await:

Till now to do async task we were returning promises from the function that will hold our outcome of async task.Now what about instead of returning a promises from as function we make function as async.
Using async keyword we can make our function asynchrounous that will still return our promise but here plus point is that you dont have to use then chaining you can use await keyword that will suspend the code flow in your async function till the time your function is not resolved you can use 0 or more then 0 await in your async function

```javascript
function resolveAfter2Seconds() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("resolved");
    }, 2000);
  });
}

async function asyncCall() {
  console.log("calling");
  const result = await resolveAfter2Seconds();
  console.log(result);
  // expected output: "resolved"
}

asyncCall();
```

## 34. Error

### Exception handling statements:

1. throw statement

```javascript
// syntax
throw Expression;

throw "Error2"; // String type
throw 42; // Number type
throw true; // Boolean type
throw {
  toString() {
    return "I'm an object!";
  },
};
```

2. try..catch block:

you want the try block to succeed—but if it does not, you want control to pass to the catch block. If any statement within the try block (or in a function called from within the try block) throws an exception, control immediately shifts to the catch block. If no exception is thrown in the try block, the catch block is skipped. The finally block executes after the try and catch blocks execute but before the statements following the try...catch statement.

### ErrorTypes:

1.  ReferenceError:
    The ReferenceError object represents an error when a variable that doesn't exist (or hasn't yet been initialized) in the current scope is referenced.
2.  SyntaxError:The SyntaxError object represents an error when trying to interpret syntactically invalid code.
3.  TypeError:
    A TypeError may be thrown when:

4.  an operand or argument passed to a function is
    2.incompatible with the type expected by that operator or function; or
5.  when attempting to modify a value that cannot be changed; or
6.  when attempting to use a value in an inappropriate way.
7.  RangeError:
    A RangeError is thrown when trying to pass a value as an argument to a function that does not allow a range that includes the value.

This can be encountered when:

1. passing a value that is not one of the allowed string values to String.prototype.normalize(), or
2. when attempting to create an array of an illegal length with the Array constructor, or
3. when passing bad values to the numeric methods Number.prototype.toExponential(), Number.prototype.toFixed() or Number.prototype.toPrecision().

5.InternalError:

Creates an instance representing an error that occurs when an internal error in the JavaScript engine is thrown. E.g. "too much recursion"

## 35. String

1. String.prototype.at() and String.prototype.charAt() Returns the character (exactly one UTF-16 code unit) at the specified index
2. String.prototype.charCodeAt():Returns a number that is the UTF-16 code unit value at the given index
3. String.prototype.concat():
   The concat() method concatenates the string arguments to the calling string and returns a new string.

```javascript
const str1 = "Hello";
const str2 = "World";

console.log(str1.concat(" ", str2));
// expected output: "Hello World"

console.log(str2.concat(", ", str1));
// expected output: "World, Hello"
```

4. String.prototype.includes():
   The includes() method performs a case-sensitive search to determine whether one string may be found within another string, returning true or false as appropriate.

```javascript
const sentence = "The quick brown fox jumps over the lazy dog.";

const word = "fox";

console.log(
  `The word "${word}" ${
    sentence.includes(word) ? "is" : "is not"
  } in the sentence`
);
// expected output: "The word "fox" is in the sentence"
```

5. String.prototype.indexOf():
   The indexOf() method, given one argument: a substring to search for, searches the entire calling string, and returns the index of the first occurrence of the specified substring.
6. String.prototype.lastIndexOf():
   Returns the index within the calling String object of the last occurrence of searchValue, or -1 if not found.

```javascript
const paragraph =
  "The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?";

const searchTerm = "dog";

console.log(
  `The index of the first "${searchTerm}" from the end is ${paragraph.lastIndexOf(
    searchTerm
  )}`
);
// expected output: "The index of the first "dog" from the end is 52"
```

7.String.prototype.match():
The match() method retrieves the result of matching a string against a regular expression.

```javascript
const paragraph = "The quick brown fox jumps over the lazy dog. It barked.";
const regex = /[A-Z]/g;
const found = paragraph.match(regex);

console.log(found);
// expected output: Array ["T", "I"]
```

8.String.prototype.replace():
The replace() method returns a new string with one, some, or all matches of a pattern replaced by a replacement.

```javascript
const p =
  "The quick brown fox jumps over the lazy dog. If the dog reacted, was it really lazy?";

console.log(p.replace("dog", "monkey"));
// expected output: "The quick brown fox jumps over the lazy monkey. If the dog reacted, was it really lazy?"

const regex = /Dog/i;
console.log(p.replace(regex, "ferret"));
// expected output: "The quick brown fox jumps over the lazy ferret. If the dog reacted, was it really lazy?"
```

9. String.prototype.slice():
   The slice() method extracts a section of a string and returns it as a new string, without modifying the original string.

```javascript
const str = "The quick brown fox jumps over the lazy dog.";

console.log(str.slice(31));
// expected output: "the lazy dog."

console.log(str.slice(4, 19));
// expected output: "quick brown fox"

console.log(str.slice(-4));
// expected output: "dog."

console.log(str.slice(-9, -5));
// expected output: "lazy"
```

10. String.prototype.split():
    The split() method takes a pattern and divides a String into an ordered list of substrings by searching for the pattern, puts these substrings into an array, and returns the array.

```javascript
const str = "The quick brown fox jumps over the lazy dog.";

const words = str.split(" ");
console.log(words[3]);
// expected output: "fox"

const chars = str.split("");
console.log(chars[8]);
// expected output: "k"

const strCopy = str.split();
console.log(strCopy);
// expected output: Array ["The quick brown fox jumps over the lazy dog."]
```

11. String.prototype.toUpperCase()
    Returns the calling string value converted to uppercase.

12. String.prototype.trim()
    Trims whitespace from the beginning and end of the string.

## 36. Array

Array object allows you to store multiple values in a single variable.
In JavaScript, arrays aren't primitives but are instead Array objects with the following core characteristics:

1. JavaScript arrays are resizable and can contain a mix of different data types. (When those characteristics are undesirable, use typed arrays instead.)
2. JavaScript arrays are not associative arrays and so, array elements cannot be accessed using arbitrary strings as indexes, but must be accessed using nonnegative integers (or their respective string form) as indexes.
3. JavaScript arrays are zero-indexed: the first element of an array is at index 0, the second is at index 1, and so on — and the last element is at the value of the array's length property minus 1.
4. JavaScript array-copy operations create shallow copies. (All standard built-in copy operations with any JavaScript objects create shallow copies, rather than deep copies).

```javascript
console.log(arr.0); // a syntax error
```

JavaScript syntax requires properties beginning with a digit to be accessed using bracket notation instead of dot notation. It's also possible to quote the array indices (e.g., years['2'] instead of years[2]), although usually not necessary.
The 2 in years[2] is coerced into a string by the JavaScript engine through an implicit toString conversion. As a result, '2' and '02' would refer to two different slots on the years object, and the following example could be true:

```javascript
console.log(years["2"] !== years["02"]);
```

Only years['2'] is an actual array index. years['02'] is an arbitrary string property that will not be visited in array iteration.

```javascript
const fruits = [];
fruits.push("banana", "apple", "peach");
console.log(fruits);
console.log(fruits.length); // 3
fruits[5] = "mango";
console.log(fruits);
console.log(fruits[4]); // 'undefined'
console.log(fruits[5]); // 'mango'
console.log(Object.keys(fruits)); // ['0', '1', '2', '5']
console.log(fruits.length); // 6

// Increasing the length.
fruits.length = 10;
console.log(fruits); // ['banana', 'apple', 'peach', empty x 2, 'mango', empty x 4]
console.log(Object.keys(fruits)); // ['0', '1', '2', '5']
console.log(fruits.length); // 10
console.log(fruits[8]); // undefined

// Decreasing the length property does, however, delete elements.
fruits.length = 2;
console.log(Object.keys(fruits)); // ['0', '1']
console.log(fruits.length); // 2
```

### Array Properties:

1. Array.prototype.length
   Reflects the number of elements in an array.

### Array Methods:

### 1. Array.isArray():

Returns true if the argument is an array, or false otherwise.

### 2. Array.prototype.map():

The map() method creates a new array populated with the results of calling a provided function on every element in the calling array.

```javascript
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map((x) => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

Return value:

A new array with each element being the result of the callback function.
Calling map() on non-array objects:

The map() method reads the length property of this and then accesses each integer index.

```javascript
const arrayLike = {
  length: 3,
  0: 2,
  1: 3,
  2: 4,
};
console.log(Array.prototype.map.call(arrayLike, (x) => x ** 2));
// [ 4, 9, 16 ]
```

### 3. Array.prototype.filter()

The filter() method creates a shallow copy of a portion of a given array, filtered down to just the elements from the given array that pass the test implemented by the provided function.

```javascript
const words = [
  "spray",
  "limit",
  "elite",
  "exuberant",
  "destruction",
  "present",
];

const result = words.filter((word) => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

Return value:

A shallow copy of a portion of the given array, filtered down to just the elements from the given array that pass the test implemented by the provided function. If no elements pass the test, an empty array will be returned.

    USES:
    1. Search in an array  and can return that

### 4. Array.prototype.reduce():

The reduce() method executes a user-supplied "reducer" callback function on each element of the array, in order, passing in the return value from the calculation on the preceding element. The final result of running the reducer across all elements of the array is a single value.

```javascript
// reduce(callbackFn, initialValue)
const array1 = [1, 2, 3, 4];

// 0 + 1 + 2 + 3 + 4
const initialValue = 0;
const sumWithInitial = array1.reduce(
  (accumulator, currentValue) => accumulator + currentValue,
  initialValue
);

console.log(sumWithInitial);
// expected output: 10
```

The reduce() method is an iterative method. It runs a "reducer" callback function over all elements in the array, in ascending-index order, and accumulates them into a single value. Every time, the return value of callbackFn is passed into callbackFn again on next invocation as accumulator. The final value of accumulator (which is the value returned from callbackFn on the final iteration of the array) becomes the return value of reduce().

callbackFn is invoked only for array indexes which have assigned values. It is not invoked for empty slots in sparse arrays.

Unlike other iterative methods, reduce() does not accept a thisArg argument. callbackFn is always called with undefined as this, which gets substituted with globalThis if callbackFn is non-strict.

Edge cases:

If the array only has one element (regardless of position) and no initialValue is provided, or if initialValue is provided but the array is empty, the solo value will be returned without calling callbackFn.

If initialValue is provided and the array is not empty, then the reduce method will always invoke the callback function starting at index 0.

If initialValue is not provided then the reduce method will act differently for arrays with length larger than 1, equal to 1 and 0, as shown in the following example:
Return value:

The value that results from running the "reducer" callback function to completion over the entire array.

USES:

1.Flatten an array - 2D To 1D

```javascript
const flattened = [
  [0, 1],
  [2, 3],
  [4, 5],
].reduce((accumulator, currentValue) => accumulator.concat(currentValue), []);
// flattened is [0, 1, 2, 3, 4, 5]
```

2. Grouping objects by a property
3. remove duplicate in an array
4. Replace .filter().map() with .reduce()

### 5. Array.prototype.forEach()

The forEach() method executes a provided function once for each array element.

```javascript
const array1 = ["a", "b", "c"];

array1.forEach((element) => console.log(element));

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

callbackFn is invoked only for array indexes which have assigned values. It is not invoked for empty slots in sparse arrays.
forEach() does not mutate the array on which it is called, but the function provided as callbackFn can. Note, however, that the length of the array is saved before the first invocation of callbackFn. Therefore:

callbackFn will not visit any elements added beyond the array's initial length when the call to forEach() began.
Changes to already-visited indexes do not cause callbackFn to be invoked on them again.
If an existing, yet-unvisited element of the array is changed by callbackFn, its value passed to the callbackFn will be the value at the time that element gets visited. Deleted elements are not visited.
Return value:
undefined so not chainable.
forEach() expects a synchronous function — it does not wait for promises. Make sure you are aware of the implications while using promises (or async functions) as forEach callbacks.

```javascript
const ratings = [5, 4, 5];
let sum = 0;

const sumFunction = async (a, b) => a + b;

ratings.forEach(async (rating) => {
  sum = await sumFunction(sum, rating);
});

console.log(sum);
// Naively expected output: 14
// Actual output: 0
```

USES:

1. print content of array
2. iterate over array and can also modify array not by itself but by callback function
3. If you wanted to run an callback on each item of array
4. ## for-in and for-of

### for-of:

The for...of statement executes a loop that operates on a sequence of values sourced from an iterable object.

```javascript
const array1 = ["a", "b", "c"];

for (const element of array1) {
  console.log(element);
}

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

When a for...of loop iterates over an iterable, it first calls the iterable's iterator() method, which returns an iterator, and then repeatedly calls the resulting iterator's next() method to produce the sequence of values to be assigned to variable.

A for...of loop exits when the iterator has completed (the iterator's next() method returns an object containing done: true). You may also use control flow statements to change the normal control flow. break exits the loop and goes to the first statement after the loop body, while continue skips the rest of the statements of the current iteration and proceeds to the next iteration.

If the for...of loop exited early (e.g. a break statement is encountered or an error is thrown), the return() method of the iterator is called to perform any cleanup

**NOTE**:You can also interate over object using for of loop all you need to do is to define an iterator method in that object.

### for-in:

The for...in statement iterates over all enumerable string properties of an object (ignoring properties keyed by symbols), including inherited enumerable properties.

```javascript
const object = { a: 1, b: 2, c: 3 };

for (const property in object) {
  console.log(`${property}: ${object[property]}`);
}

// expected output:
// "a: 1"
// "b: 2"
// "c: 3"

}

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

The loop will iterate over all enumerable properties of the object itself and those the object inherits from its prototype chain (properties of nearer prototypes take precedence over those of prototypes further away from the object in its prototype chain).

A for...in loop only iterates over enumerable, non-symbol properties. Objects created from built–in constructors like Array and Object have inherited non–enumerable properties from Array.prototype and Object.prototype, such as Array's indexOf() method or Object's toString() method, which will not be visited in the for...in loop.

The traversal order, as of modern ECMAScript specification, is well-defined and consistent across implementations. Within each component of the prototype chain, all non-negative integer keys (those that can be array indices) will be traversed first in ascending order by value, then other string keys in ascending chronological order of property creation

### Array iteration and for...in:

Array indexes are just enumerable properties with integer names and are otherwise identical to general object properties. The for...in loop will traverse all integer keys before traversing other keys, and in strictly increasing order, making the behavior of for...in close to normal array iteration. However, the for...in loop will return all enumerable properties, including those with non–integer names and those that are inherited. Unlike for...of, for...in uses property enumeration instead of the array's iterator. In sparse arrays, for...of will visit the empty slots, but for...in will not.

It is better to use a for loop with a numeric index, Array.prototype.forEach(), or the for...of loop, because they will return the index as a number instead of a string, and also avoid non-index properties.

## 38. Functional Programming

A programming paradigm is essentially a bunch of rules that you follow when writing code.
If you're coding in a language that follows the imperative/procedural paradigm, you write code that tells how to do something.You can write JavaScript in the Declarative paradigm or the Imperative paradigm. This is what people mean when they say it's a multi-paradigm language.

1. keep ypur data and your functin seperate - pure function
2. tou dont update a variable again and again instaed you delacre a new variale and put that new value in that
3. Function are treated as first class obeject

### WHY YOU DO THAT ?

## 39. Symbols:

Symbol is a built-in object whose constructor returns a symbol primitive — also called a Symbol value or just a Symbol — that's guaranteed to be unique. Symbols are often used to add unique property keys to an object that won't collide with keys any other code might add to the object, and which are hidden from any mechanisms other code will typically use to access the object.

```javascript
//The below code creates three new Symbols. Note that Symbol("foo") does not coerce the string "foo" into a Symbol. It creates a new Symbol each time:
const sym1 = Symbol();
const sym2 = Symbol("foo");
const sym3 = Symbol("foo");

Symbol("foo") === Symbol("foo"); // false

// The following syntax with the new operator will throw a TypeError:
//  It is not a constructor in the traditional sense, because it can only be called as a function, instead of being constructed with new Symbol().
const sym = new Symbol(); // TypeError
```

## 40. Polyfills

A polyfill is a piece of code used to provide modern functionality on older browsers that do not natively support it.

### map polyfill:

```javascript
// 1. Fiest chek does your browser have   map function or not already if not only then write your map function
if (typeof Array.prototype.map !== "function") {
  // here create your map function
}
// 2. Apply some checks on your arguemnts
if (typeof Array.prototype.map !== "function") {
  // dont use arrow function here
  Array.prototype.myMap = function (callback, thisArg) {
    if (typeof callback !== "function") return;
    // apply check for array like object length property
    if (typeof this.length !== "number") return;
    const arr = [];
    //this argument should be object or if not you can change that to object using Object constructer
    if (typeof thisArg === "object") {
      // we will be calling callback function for every entry of array object so let make a loop
      for (let i = 0; i < this.length; i++) {
        // i represent property of array object  so check if  it exist  only then proceed
        if (i in this) {
          const outcome = callback.call(thisArg || this, this[i], i, this);
          arr.push(outcome);
        } else {
          return;
        }
      }
    }
    return arr;
  };
}
// for array
const arr = [1, 2, 3, 4];
const newArr = arr.myMap((value, index, arr) => {
  return value * 10;
});
console.log(newArr); //[ 10, 20, 30, 40 ]
// for array like object
const obj = {
  length: 3,
  0: 2,
  1: 3,
  2: 9,
};
const newObj = Array.prototype.myMap.call(obj, (value, index, obj) => {
  return value * 10;
});
console.log(newObj); //[ 20, 30, 90 ]
```

### filter polyfill: 
```javascript
if (typeof Array.prototype.filter !== "function") {
  Array.prototype.myFilter = function (callback, thisArg) {
    if (typeof callback !== "function") return;
    if (typeof this.length !== "number") return;
    const arr = [];

    if (typeof this === "object") { 
      for (let i = 0; i < this.length; i++) {
        if (i in this) {
          if (callback.call(thisArg || this, this[i], i, this)) {
            arr.push(this[i]);
          }
        } else {
          return;
        }
      }
    }
    return arr;
  };
}

const arr=[1,2,3,4,5]
const newArr=arr.myFilter((value,index,arr)=>{ 
    return value>3
})
console.log(newArr)// [ 4, 5 ]

const obj={
    length:5,
    0:1,
    1:2,
    2:3,
    3:4,
    4:5
}

const newObj=Array.prototype.myFilter.call(obj,(value)=>value>3)
console.log(newObj)//[ 4, 5 ]
```

### reduce polyfill:
````javascript
if(!Array.prototype.reduce){
    Array.prototype.myReduce=function(callback,intialValue){
        if(typeof callback !== "function") return
        //intial value could be undefined if not provided 
         let accumaltor=intialValue 
         for(let i=0;i<this.length;i++){
            // accumaltor can have undeined as well as a value 
            if(i in this && accumaltor!==undefined){
                // i am at zero index and accumaltor have some value so call callback for each index
                accumaltor=callback(accumaltor,this[i],i,this)

            }else{
                // i am at zero index and accumlator is undefined
                accumaltor=this[i]
                continue 
            }
         }
         return accumaltor
    }
}
const array = [15, 16, 17, 18, 19];

function reducer(accumulator, currentValue, index) {
  const returns = accumulator + currentValue;
  console.log(
    `accumulator: ${accumulator}, currentValue: ${currentValue}, index: ${index}, returns: ${returns}`,
  );
  return returns;
}
array.myReduce(reducer);

// accumulator: 15, currentValue: 16, index: 1, returns: 31
// accumulator: 31, currentValue: 17, index: 2, returns: 48
// accumulator: 48, currentValue: 18, index: 3, returns: 66
// accumulator: 66, currentValue: 19, index: 4, returns: 85
````
## 41. FileReader:
The FileReader object lets web applications asynchronously read the contents of files (or raw data buffers) stored on the user's computer 
FileReader can only access the contents of files that the user has explicitly selected, either using an HTML `<input type="file">` element or by drag and drop. It cannot be used to read a file by pathname from the user's file system.
File reader reads a file in three state  and these three sate can be easily accessed by its readyState property if this gave you value as 0 means that reader has been created. None of the read methods called yet.
if it gives you value as 1 means that A read method has been called.
ans lastly if it gives you value 2 means   operation is complete.

## Function

## Objects

## strict mode

## undefined va null

## Dom lifecycle

## same-origin policy

## Javascript Nature

## 41. execution context  
Whenever a browser reading your html code and sees a script tag or any attribute that    contains js code like on onClick method it send that code to the js engine   where first a new environment is created to transform and execute that code. 
In execution context code will be parsed and variables and function declarations will be assigned memory and then code will be transformed into binary so that CPU can understand and execute it.

Js engine create 2 types of execution context :

1. global execution context 
2. function execution context 

Global Execution Context(GEC) : 
For every js file a global execution context is created and inside that global code will be executed that too the code that is written outside of the function .

Function  Execution  Context will be created when that function will be called and there can be more than 1 function execution context but only 1 global execution context 

How execution context are created :
Every execution context is created in 2 phases:
 1. creation phase
 2. execution phase 

1. creation phase is associated with Execution Context Object(ECO) creation .
ECO holds the important data that a code needed while execution that code. 

ECO creation happens in 3 phases:

1. creation of variable object 
2. creation of scope chain 
3. setting up the value of this keyword 

1. creation of the variable object :

A Variable Object(VO) is created in a execution context  and it stores the variable and function declaration  defined with in that execution context. 

For example  if you declare a variable in GEC with var keyword then a property will be created in VO and  a undefined will be assigned to that property.
 For function declaration - a property is also added that refer to that function and this property is stored in memory 
this means that variable and function declaration are made accessible and stored inside the VO .
In FEC no VO is created but an an array like argument object is created that stores all th arguments supplied to that function . 

2. Creation of scope chain : Each FEC defined its scope that is whatever variable and  function it defined  are accessible in its scope 

3. creation phase setting up the value of this 
 

## callstack

## single threaded vs Multi threaded

## Java vs Javascript

## Event loop

## RegExp

## Set
