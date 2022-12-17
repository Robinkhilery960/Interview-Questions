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
 inside the function is the object that the function was accessed on. With these funtions
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

    You can create an object using Object Constructer

    ```javascript
    var object = new Object();
    ```

    ### Cross Questions:

        1.  What is a  Constructer ?
        2. What is an Object Constructer

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

    Create any function and apply the new operator to create object instances, using function as a constructer

    ```javascript
    function Person(name) {
      this.name = name;
      this.age = 21;
    }
    var object = new Person("Sudheer");
    ```

    ### Cross Questions:

        1. What is difference of creating an object from class and creating an object front the function constructer
        2. Is all the function in JavaScript can be called as constructer function ?
        3. what is difference between creating an Object from  object literals and creating an object from  function  constructer
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

An arrow function is a shorter syntax for a function expression and does not have its own this so don't use arrow function as object methods, Event handlers, Prototype methods. Arrow function dont have argument object so also not use them for functions that use the arguments object.
Arrow functions also does not have new.target keyword so also dont use them as constructer functions

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
Whenever you uses any function as a  constructer function then prototype property of that constructer is set as prototype of created object  and this prototype property contains the constructer , but in case of arrow function this is missing so you cant use arrow function as constructer and also arrow function does not have new.target so it will never know that it is called with new keyword or not. 
````javascript
const Car=(make, model, year)=>{
  this.make = make;
  this.model = model;
  this.year = year;
} 
Car.prototype
// undefined
```` 

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

Lexical scope means the scope in which a item is created . In other words area where your item defination lies is called lexical sope of that item .Any item is accessible to the code which is in its lexical scope .

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
    // assigning function to variavle
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

### var :

Variables declared with var keyword are either function scoped or global scope depending upon where they are declared.Initializtion of variables is optional.
Variables declared using var are created before any code is executed in a process known as hoisting. Their initial value is undefined.
Redeclaration, reassigning is possible in same scope

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
Variable declared with let can only be accessed after its declaration is reached beacuse of Temporal Dead Zone.
Redeclaring the same variable within the same function or block scope raises a SyntaxError while reassiging can be done

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

Variable declared with this keyword are block scope and they cannot be redeclared annd reassigned and initializer for a constant is required. However, if a constant is an object or array its properties or items can be updated or removed.

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

Javascript hoisting refer to the process where declaration of functions, variables or classes move to the top of their scope before execution of the code.. Remember that JavaScript only hoists declarations, not initialisation

### Variable Hoisting:

Variables declaration are hoisted to top of their scope.Undeclared variables do not exist until code assigning them is executed.Therefore, assigning a value to an undeclared variable implicitly creates it as a global variable when the assignment is executed. This means that, all undeclared variables are global variables.

```javascript
console.log(typeof variable); // undefined
console.log(variable); // Refernece error - when try to access an undeclared  variable

console.log(hoist); // Output: undefined

var hoist = "The variable has been hoisted.";

function hoist() {
  console.log(message);
  var message = "Hoisting is all the rage!";
}

hoist(); // Ouput: undefined

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

### What's the difference between declaring and initialising?

Declaring a variable means we reserve the name in memory at the current scope. That is labelled 1 in the comments.

Initialising a variable is setting the value of the variable. That is labelled 2 in the comments.

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

## 19. Funtions

A function is a set of statements that take inputs, do some specific computation, and produce output.In JavaScript, functions are first-class objects, because they can have properties and methods just like any other object. What distinguishes them from other objects is that functions can be called. In brief, they are Function objects.For constructer function default return value is `this` keyword and for other function it is undefined.
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

When you dont know that how many arguments are supplied to your function then you can use rest parameter there to accept those arguments.
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

````javascript
const obj = { key1: 'value1' };
const array = [...obj]; // TypeError: obj is not iterable
````  

On the other hand, spreading in object literals enumerates the own properties of the object. For typical arrays, all indices are enumerable own properties, so arrays can be spread into objects.


````javascript
const array = [1, 2, 3];
const obj = { ...array }; // { 0: 1, 1: 2, 2: 3 }
````
### SeeAlso:
  [Spread Syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#try_it)

## 23. rest parameter vs argument object
### rest parameter:
1. The arguments object is not a real array, while rest parameters are Array instances, meaning methods like sort(), map(), forEach() or pop() can be applied on it directly.
2. The rest parameter bundles all the extra parameters into a single array, but does not contain any named argument defined before the ...restParam. The arguments object contains all of the parameters — including the parameters in the ...restParam array — bundled into one array-like object

## 24. new keyword
New keyword let you define a new instance of a user defined object type or in-built object type that has a constructer function.
````javascript
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}

const car1 = new Car('Eagle', 'Talon TSi', 1993);

console.log(car1.make);
// expected output: "Eagle"
````
When a function is called with the new keyword, the function will be used as a constructor. new will do the following things:
1. Creates a blank, plain JavaScript object. For convenience, let's call it newInstance.
2. Points newInstance's [[Prototype]] to the constructor function's prototype property, if the prototype is an Object. Otherwise, newInstance stays as a plain object with Object.prototype as its [[Prototype]].
````text
Note:Properties/objects added to the constructor function's prototype property are therefore accessible to all instances created from the constructor function.
```` 
3. Executes the constructor function with the given arguments, binding newInstance as the this context (i.e. all references to this in the constructor function now refer to newInstance).
4. If the constructor function returns a non-primitive, this return value becomes the result of the whole new expression. Otherwise, if the constructor function doesn't return anything or returns a primitive, newInstance is returned instead. (Normally constructors don't return a value, but they can choose to do so to override the normal object creation process.)

Classes can only be instantiated with the new operator — attempting to call a class without new will throw a TypeError. 

A function can know whether it is invoked with new by checking new.target. new.target is only undefined when the function is invoked without new.
## 25. What is IIFE(Immediately Invoked Function Expression)
IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined. The signature of it would be as below,

````javascript
(function () {
  // logic here
})();
````
The primary reason to use an IIFE is to obtain data privacy because any variables declared within the IIFE cannot be accessed by the outside world. i.e, If you try to access variables with IIFE then it throws an error as below,

````javascript
(function () {
  var message = "IIFE";
  console.log(message);
})();
console.log(message); //Error: message is not defined
````

