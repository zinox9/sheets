![Banner](./images/js.png)

#### Table Of Contents

**[JavaScript Reference Sheet](#javascript-reference-sheet)**

- [References](#references)

- [Basics](#basics)

- [Functions](#functions) 

- [Arrays](#arrays) 

- [Objects & Properties](#objects--properties)

- [Document Object Model (DOM)](#document-object-model-dom)

- [ES6+](#es6)

- [Asynchronous JavaScript](#asynchronous-javascript)

---

# JavaScript Reference Sheet

> **Road Map to study JavaScript. Starting All the way from Basics to Advanced with references of useful links !** 

A reference to Advanced JavaScript Concepts : [**JavaScript Behind the Scenes**](./jsBehind.md)

---

## References

- Cheat Sheet :  [Link](https://websitesetup.org/javascript-cheat-sheet/)

- All JavaScript Details : [Javascript.info](https://javascript.info)

- JavaScript Documentation : [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/javascript)

- Books : [Eloquent JS](https://eloquentjavascript.net/) | [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS)

---

## Basics

- **Console logging**

- **Variable & Datatypes** (using var)
  
  - Number -  Floating Point numbers & Integers
  - Strings -  For text 
  - Boolean  - true/false logical data type
  - Undefined - Data type of variable with no value
  - Null - Doesn't Exist 
  - JavaScript is dynamic : data types are automatically assigned
  - Camel Case & Naming Conventions

- **Comments**

- **Mutation** (Changing Data in variable) &  **Coercion** (Data type conversion)

- **Math Operators & Logic Operators**
  
  - `+ , - , * , / , %` 
  - < , > and <= , >= ...
  - Compare letters according to Unicode ('a' < 'b')
  - `typeof` &  (== & ===)
  - Operator Precedence & Multiple Assignments
  - Operators Shorthand

- **Conditionals** : If else, nested If, if else if 

- **Ternary operator**

- **Switch Statement**

- **Boolean Logic** : && , || , !

- **Truthy and Falsy** values
  
  - Falsy  values : undefined , null , 0 , '', NaN
  
  - Truthy values : all others give true on coercion 

- **Loops & Iteration**

- **For Loop** 
  
  - While Loop
  - Continue & Break

- **Error Handling** 
  
  - Throw
  - try , catch

- **Strict Mode**  (`"use strict"`)
  
  - It catches some common coding bloopers, throwing exceptions.
  - It prevents, or throws errors, when relatively "unsafe" actions are taken (such as gaining access to the global object).
  - It disables features that are confusing or poorly thought out.

---

## Functions

- **Basic Functions** ( declaration , returning data )
  - Function Statement (direct declaration) and  
    - Function Statement returns Undefined on execution (if , while , function declaration)
  - Function Expression (using variable)
    - Function Expression always returns a value (typeof, variable function, 2+3)
- **Default Parameters**
- **Callback Functions** - Functions as Arguments  & Return Functions from Functions
- **IIFE** - Immediately Invoked Function Expression
  - contain an anonymous function in braces and then call it at the same time 
  - only the content returned is accessible , abstraction & encapsulation.
- **Closures**
  - An inner function always has access to the variables and parameters of its outer function, even after the outer function has returned.
  - It works because the Scope Chain is a pointer , so even when the function has returned in the execution stack , the scope chain still has access to the variables of the outer function.
- **Argument Object**
- **Inbuilt String methods** (indexOf , startsWith, substring)
- **Inbuilt Number Methods** (MATH object)
- **Other Useful Inbuilt Functions :**
  - Date function
  - Split & Join function
  - Set timeout
  - ParseInt

---

## Arrays

- **Basic** Arrays (declaration) 
- `New Array ()` Syntax
- Array **Properties** : length , index
- Array **Methods**  : pop , push , shift , unshift
- **Iterating** Arrays : `for...of` , `for...in` , for each, map
- **Searching** Arrays  : `indexOf , find , findIndex`
- **Filtering** arrays  : filter , reduce
- **Sorting** Arrays : sort
- **Altering** Arrays : split and join functions
- **Useful Array Functions**  : splice , slice , concat , reverse , every , some

---

## Objects & Properties

- **Basic** Objects (declaration , accessing , mutating)
  
  - new Object () Syntax
  - Functions in objects (Are methods) 

- **Prototypes & Prototype chains**
  
  - Prototypes are methods of objects that can be inherited
  - Every inherited object can access its parents prototype 
  - Therefore , we write those methods in prototype that we want other objects to inherit
  - The prototypes of constructor is the prototype of all its instances too
  - We can check the prototype ,using `object.property` or `object.__proto__`
  - `hasOwnProperty` lets us know if the property is inherited or not
  - `instanceOf` can be used to check what is instance of what

- **Constructors** - used as a blueprint to create multiple objects

- **Constructor Functions** - used to initialize data of object for every instance
  
  - Creating Constructor using Function
  - convention is to keep first letter capital of constructor
    - object variables are assigned values using `this` statement
  - new object is created using , `new constructorName()` and assigning it to a variable 
    - We can create a prototype using  , `object.prototype`
    - We can inherit other constructors by using `call` method with parameters of parent constructor
  - Constructors can also be created using `Object.create` , where we specify the prototype first and then specify the data
  - `Object.create(parent.prototype)` can inherit the prototype of parent to child prototype

- **Primitives & Object**
  
  - Primitives hold the data directly  (number , strings)
  - Objects point the data to other object (objects, arrays)
  - In JavaScript almost Everything is an Object
    - Primitives : Numbers , Strings ,  Booleans, Undefined and Null are not.
    - Primitives can be converted to objects using autoboxing when methods like `string.length` are executed 
    - Everything else is object, Arrays, Functions, Objects...

- Two objects are only equal if they take the same space and position in memory , they wont be equal no matter the keys and properties.

- **Bind, Call & Apply**
  
  - Call can be used to give a different this pointer and call the function immediately
  - Apply , same as call , but the arguments can be passed only as array
  - Bind , sets `this` and other arguments to the function , then gives the functions so that it can be called with those arguments later

---

## Document Object Model (DOM)

- **DOM** 
  - structured representation of HTML
  - DOM connects webpages to scripts like JS
  - for each HTML box there is an object in DOM that we can access and interact with
- DOM **Methods** - querySelecor, getElementById
- **Event Listeners**  - storage , UI listener (mouse)
- Data Storage **CRUD** - local Storage
- `window.location` - assign , hash
- **window** - inner width , inner height, console, document, addeventlistner(to work on multiple tabs)

---

## ES6+

- **let and const** 
  - are only blocked scoped (any block if, while) , whereas normal var is function scoped only
  - cant be used before declaration , whereas var gives a value of undefined 
  - IIFE can be created in es6, just in a block {} without variables
- **Template Strings**
- **Arrow Functions** (lexical this keyword functionality)  
- **Destructuring** : `{ name ,  length } = object` , `[name , length] = array`
- **Spread Operator** : spread array , objects
- **Rest Parameters**
- **Maps** : same like object , but keys can be numbers, functions anything
  - we can loop through them
  - functions : get,set, size , has, delete, clear, entries
- **Class** : syntactical sugar for es5 constructor and inheritance
  - Class Constructor
  - Class methods
  - Subclasses , Super &  Extends
  - Getters and Setters

---

## Asynchronous JavaScript

- Asynchronous Functions can run in background
- **HTTP requests & response** (Old Way)
  - `XMLhttprequest` , `readystatechange`
  - readyState, open, send
- **Promises** 
  - Object that keeps track about whether a certain event has happened or not
  - Determines what happens after the event
  - Implements the concept of a future value that were expecting
  - 4 states = Pending ->  Settled/Resolved -> Fulfilled, Rejected
  - Checking : resolve, reject, 
  - Performing Actions using `.then` &  `.catch`
  - Promise chaining 
- **Async/Await** alternative way to consume promises
  - we can use the response promise given by await to check and catch errors.
- **Fetch Api**  - gives promises that can be consumed using Async/await or promises
- **Axios** - alternative to fetch , directly returns data in JSON
- **API** - Application Programming Interface (Remote Server has a part that works as API)
- **JSON** - JavaScript Object Notation  (json function is available inbuilt in js)
- **AJAX** - Asynchronous Javascript and XML 
- **CrossOrigins**

This is Just the Beginning of your Journey in JavaScript , there's always soo much more to explore ! 

A reference to Advanced JavaScript Concepts : [**JavaScript Behind the Scenes**](./jsBehind.md)

---
