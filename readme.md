# Javascript Interview Questions

##  1. What is JSON ?

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
  let person1={
    name: " david",
    age:"22"
     
}
let person2={
    name: " Herry",
    age:"23"
     
}
let showDetail=function(city,car){
    console.log( `${this.name} is ${this.age} years old and he lives in ${city} and drives ${car}`)
        }

showDetail.call(person2,'noida',"BMW");
showDetail.call(person1,"delhi","mercedez");
   ```

### Apply:
```javascript
let person1={
    name: " david",
    age:"22" 
}
let person2={
    name: " Herry",
    age:"23" 
}
let showDetail=function(city,car){
    console.log( `${this.name} is ${this.age} years old and he lives in ${city} and drives ${car}`)
        }
showDetail.apply(person2,['noida',"BMW"]);
showDetail.apply(person1,["delhi","mercedez"]);
```

### Bind:
```javascript
 let person1={
    name: " david",
    age:"22"
     
}
let person2={
    name: " Herry",
    age:"23"
     
}
let showDetail=function(city,car){
    console.log( `${this.name} is ${this.age} years old and he lives in ${city} and drives ${car}`)
        } 

let bindshowDetail=showDetail.bind(person2,'noida',"BMW");
console.log(bindshowDetail)
 bindshowDetail(); 
```
**Note:**  Call and apply can be interchangeable . Both execute function  immediately . Where binds create a new function for you which later on can be invoked whenever you want that.

### Cross Questions
    1. What is this? How does it work?

## 4. Ways to create a Object ?
There are many ways to create objects in javascript as below

1. **Object constructor:**
    
     You can create an object using Object Constructer 
    
    `var object = new Object();`
    
    ### Cross Questions:
        1.  
    
2. **Object's create method:**
    
    The create method of Object creates a new object by passing the prototype object as a parameter
    
    parameters - can be null or any other object 
    
    `var object = Object.create(null);`
    
3. **Object literal syntax:**
    
    The object literal syntax (or object initializer), is a comma-separated set of name-value pairs wrapped in curly braces.
    
    `var object = {
         name: "Sudheer",
         age: 34
    };
    
    Object literal property values can be of any data type, including array, function, and nested object.`
    
    **Note:** This is an easiest way to create an object
    
4. **Function constructor:**
    
    Create any function and apply the new operator to create object instances, using function as a constructer
    
    `function Person(name) {
      this.name = name;
      this.age = 21;
    }
    var object = new Person("Sudheer");`
    
    [Cross Questions](https://www.notion.so/Cross-Questions-33a7259b0ac04efba91787df3ead9ba9)
    
5. **Function constructor with prototype:**
    
    This is similar to function constructor but it uses prototype for their properties and methods,
    
    `function Person() {}
    Person.prototype.name = "Sudheer";
    var object = new Person();`
    
    This is equivalent to an instance created with an object create method with a function prototype and then call that function with an instance and parameters as arguments.
    
    `function func() {};
    
    new func(x, y, z);`
    
    **(OR)**
    
    `// Create a new instance using function prototype.
    var newInstance = Object.create(func.prototype)
    
    // Call the function
    var result = func.call(newInstance, x, y, z),
    
    // If the result is a non-null object then use it otherwise just use the new instance.
    console.log(result && typeof result === 'object' ? result : newInstance);`
    
6. **ES6 Class syntax:**
    
    ES6 introduces class feature to create the objects
    
    `class Person {
      constructor(name) {
        this.name = name;
      }
    }
    
    var object = new Person("Sudheer");`
    
7. **Singleton pattern:**
    
    A Singleton is an object which can only be instantiated one time. Repeated calls to its constructor return the same instance and this way one can ensure that they don't accidentally create multiple instances.
    
    `var object = new (function () {
      this.name = "Sudheer";
    })();`