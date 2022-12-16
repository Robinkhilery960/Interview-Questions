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
    
    ````javascript
    var object = new Object();
    ````
    
    ### Cross Questions:
        1.  What is a  Constructer ?
        2. What is an Object Constructer 
    
2. **Object's create method:**
    
    The create method of Object creates a new object by passing the prototype object as a parameter
    
    parameters - can be null or any other object 
    ````javascript 
    var object = Object.create(null); 
    ````
    
3. **Object literal syntax:**
    
    The object literal syntax (or object initializer), is a comma-separated set of name-value pairs wrapped in curly braces.
    ````javascript 
    var object = {
         name: "Robin",
         age: 23
    };
    ````
    
    Object literal property values can be of any data type, including array, function, and nested object.`
    
    **Note:** This is an easiest way to create an object
    
4. **Function constructor:**
    
    Create any function and apply the new operator to create object instances, using function as a constructer
    ````javascript 
    function Person(name) {
      this.name = name;
      this.age = 21;
    }
    var object = new Person("Sudheer");
    ````
    
    ### Cross Questions:
        1. What is difference of creating an object from class and creating an object front the function constructer 
        2. Is all the function in JavaScript can be called as constructer function ? 
        3. what is difference between creating an Object from  object literals and creating an object from  function  constructer 
        4. what is this new keyword and what does it do ?
   
5. **Function constructor with prototype:**
    
    This is similar to function constructor but it uses prototype for their properties and methods,
    
    ````javascript
    function Person() {}
    Person.prototype.name = "Robin";
    var object = new Person();
    ````
    
    This is equivalent to an instance created with an object create method with a function prototype and then call that function with an instance and parameters as arguments.
    
     ````javascript
     function func() {};
    
    new func(x, y, z);
     ````
    
    **(OR)**
    
    ````javascript
     // Create a new instance using function prototype.
    var newInstance = Object.create(func.prototype)
    
    // Call the function
    var result = func.call(newInstance, x, y, z),
    
    // If the result is a non-null object then use it otherwise just use the new instance.
    console.log(result && typeof result === 'object' ? result : newInstance); 
    ````
6. **ES6 Class syntax:**
    
    ES6 introduces class feature to create the objects
    
    ````javascript 
    class Person {
      constructor(name) {
        this.name = name;
      }
    }
    
    var object = new Person("Sudheer");
    ````
    
 ## 5. What is the purpose of the array slice method?
 Slice methods return you new Array from a given array  based upon the start point and end point  it  gave you a `shallow copy` of given array
 ````javascript
 const arr=[1, 2, [3], 4, 5]
const newArr=arr.slice(0,3)
console.log(arr)
console.log(newArr)
newArr[2][0]=15
console.log(arr)
console.log(newArr)
 ````

 Some methods do not mutate the existing array that the method was called on, but instead return a new array. They do so by first accessing [this.constructor[Symbol.species]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/@@species) to determine the constructor to use for the new array. The newly constructed array is then populated with elements. The copy always happens *[shallowly](https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy)* — the method never copies anything beyond the initially created array. Elements of the original array(s) are copied into the new array as follows:

- Objects: the object reference is copied into the new array. Both the original and new array refer to the same object. That is, if a referenced object is modified, the changes are visible to both the new and original arrays.
- Primitive types such as strings, numbers and booleans (not `String`,  `Number` and `Boolean`  objects): their values are copied into the new array.

Other methods mutate the array that the method was called on, in which case their return value differs depending on the method: sometimes a reference to the same array, sometimes the length of the new array.

## 6. What is the purpose of the array splice method?
The **splice()** method is used either adds/removes items to/from an array, and then returns the removed item. The first argument specifies the array position for insertion or deletion whereas the optional second argument indicates the number of elements to be deleted. Each additional argument is added to the array.

Some of the examples of this method are,
````javascript
let arrayIntegersOriginal1 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal2 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal3 = [1, 2, 3, 4, 5];

let arrayIntegers1 = arrayIntegersOriginal1.splice(0, 2); // returns [1, 2]; original array: [3, 4, 5]
let arrayIntegers2 = arrayIntegersOriginal2.splice(3); // returns [4, 5]; original array: [1, 2, 3]
let arrayIntegers3 = arrayIntegersOriginal3.splice(3, 1, "a", "b", "c"); //returns [4]; original array: [1, 2, 3, "a", "b", "c", 5]
````

The `splice()` method is a [mutating method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#copying_methods_and_mutating_methods). It may change the content of `this`. If the specified number of elements to insert differs from the number of elements being removed, the array's `length` will be changed as well. At the same time, it uses [@@species](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/@@species) to create a new array instance to be returned.

If the deleted portion is [sparse](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections#sparse_arrays), the array returned by `splice()` is sparse as well, with those corresponding indices being empty slots.

The `splice()` method is [generic](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#generic_array_methods). It only expects the `this` value to have a `length` property and integer-keyed properties. Although strings are also array-like, this method is not suitable to be applied on them, as strings are immutable.
***

| Slice | Splice |
| --- | ---|
| Doesn't modify the original array(immutable) | Modifies the original array(mutable) |
| Returns the subset of original array | Returns the deleted elements as array |
| Used to pick the elements from array | Used to insert or delete elements to/from array |

## 7. Objects vs  Maps
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

````javascript
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
````
###  Cross Questions:
    1. What is type coercion?
    2. How type coercion is happening in equality operator?

### More to read:
1. [Type Coercion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#type_coercion) 

## 9. What are arrow function and where to not use them ?
An arrow function is a shorter syntax for a function expression and does not have its own this, arguments, super, or new.target
 

## 10. What is closure? 
A closure is the combination of a function and the lexical environment within which that function was declared.
 In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

````javascript
const outer =function(){
    const fruit="mango"
    function inner(){
        console.log(fruit)
    }
    return inner
}

const result=outer() 
result()
````
 In this case, result is a reference to the instance of the function inner that is created when outer   run. The instance of inner maintains a reference to its lexical environment, within which the variable name exists.
 This environment consists of any local variables that were in-scope at the time the closure was created

## 11. What does Lexical scope means?
Lexical scope means the scope in which a item is created . In other words area where your item defination lies is called lexical sope of that item .Any item is accessible to the code which is in its lexical scope .

````javascript
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
````
Notice that the invocation of displayFullName() in the snippet above returned an Uncaught ReferenceError. The error returned because only code within an item's lexical scope can access the item.

Therefore, neither the displayFullName() function nor its internal code can access the lastName variable because lastName got defined in a different scope.

In other words, lastName’s lexical scope is different from that of displayFullName()