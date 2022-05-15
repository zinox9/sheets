![Banner](./images/jsBehind.png)

#### Table of Contents

**[JavaScript : Behind the Scenes + Extra Concepts](#JavaScript-:-Behind-the-Scenes-+-Extra-Concepts)**

- [**JavaScript Versions**](#javascript-versions)
- [**Mini Reference**](#mini-reference)
- [**JavaScript Code Execution**](#javascript-code-execution)
  - **How Code is executed** 
  - **Execution Context  & Stack**
  - **Execution Context in Detail** 
    - Variable Object, Scope Chain & 'this' Variable
- [**Asynchronous JS Working**](#asynchronous-js-working)
- [**Extra Concepts**](#extra-concepts)
  - Refactoring, Debugging Code
  - Planning Projects 
  - Event Delegation

---

# JavaScript : Behind the Scenes + Extra Concepts

> **This Sheet Explains some of the Behind the scenes working of JavaScript , how our code is executed and how Asynchronous JS works, it also contains some additional Concepts that can help to code your projects easily.**

To Study JavaScript From Beginning : [**JavaScript Roadmap**](./js.md)

---

## JavaScript Versions

- **2009 (ES5) :** major update, browsers started integrating JS (Fully supported in all browsers)
- **ES6/ES2015 :**  biggest update to language  , after this  annual release cycle started
- now on ES2016 / ES2017 / ES2018 / ES2019 ... 

---

## Mini Reference

- **Function Declaration:**

```javascript
function add() {/* code here */}
```

- **Function Expression:** 

```javascript
var add = function () { /* code here */ }
```

---

## JavaScript Code Execution

- **How Code is executed** 
  
  - Our code -> JS engine (V8) -> Parser ->
    - Abstract syntax Tree -> Machine Code -> Code Runs

- **Execution Context  & Stack**
  
  - Global Execution Context 
    - Code that is not inside any block (like function)
    - it is Associated with the global object , in browser its the window object
    - `var lastName === window.lastName`
  - Each time a function is called new Execution Context Object is added 
    - Execution stack has global context as base , then adds the function context to the stack and removes them from stack when function is returned

- **Execution Context in Detail**
  
  - Execution Context Object consists of 
    
    - Variable Object
    - Scope Chain
    - "This" Variable Pointer
  1. **Creation Phase** 
     
     1. **Creation of Variable Object**
        - Argument object is created  , containing all arguments that were passed to a function
        - Code is scanned for Function declaration , for each function a property is created in Variable object , pointing to the function
        - Code is scanned for Variable declarations, for each variable a property is created in the Variable Object and set to undefined.
        - These upper two phases are **HOISTING**
          - As Creation phase is done before Execution phase , we can call a Function Declaration even before they are declared in code. As it is a pointer in the creation phase.
          - Remember this does not happen for Function Expression as it is referenced as a variable (treated as a variable) , so a function expression is saved in Variable Object set to Undefined (the same happens for Variables)
     2. **Creation Of Scope Chain**
        - Decides Where can a certain data be accessed
        - Each new function creates a scope (variables in its block remain accessible to its stack only)
        - **Lexical Scoping** , a function that is lexically declared within another function gets access to the scope of outer function (Parent Scope)
        - Searching for the variable in Parent scopes creates a Scope Chain
        - Execution Context is the order in which functions are called
        - whereas Scope chain is the order in which function are lexically written
        - That is the reason why variables of Functions can be accessed even after they have been returned (removed from Execution Context, but still pointing in Scope Chain) [**Closures**]
     3. **Determine the value of 'this' variable in creation Phase**
        - In regular function , 'this' keyword points to global object (window)
        - in method  (functions inside object)  call, variable points to the object it is calling
        - this keyword is not assigned a value until the function in which it is defined is actually called (that is why function borrowing works between objects , as 'this' points to the object it is in)
        - Only methods point to the object , 'this' variable of a Function Declaration written inside a method will point to the window
  
  2. **Execution Phase** 
     
     - The Execution context after creation is now executed from top to bottom
     - The code of the functions that generated the context is now executed line by line

---

## Asynchronous JS Working

**The Event Loop:** Behind the scenes

- examples of Asynchronous Functions: setTimeout(), DOM events , XMLHttpRequest are Web APIs

- They create their own execution object and then are added to the Web APIs stack, running in the background away from the main execution stack

- and therefore the execution of main JavaScript Execution stack continues

- Once the Function is in Web APIs stack is complete , it comes in the Message Queue and runs when the main execution stack is empty

- The Event loop keeps checking the Message Queue and pushes the pending Function to the main execution stack as soon as it gets empty

- This is how Asynchronous JS works behind the scenes.

---

## Extra Concepts

- **Refactoring Code**
  
  1. Use DRY principle ( using functions , objects) 
  2. Organize content in different files (according to the type of work)

- **Perform Debugging:** debugger stops can help in JS
  
  ```javascript
  function myfunc() {
   // ... code
   debugger;
   // ... code
  }
  ```

- Debugging in VSCode and Chrome Developer Tools can also be used

- always use `console.log` to check your working at any point of time in program.

- **Planning a Project**
  
  - Always structure your code in modules (categorize it and divide it in files), 
    - using IIFE can help ,  as only the returned data can be accessed outside 
    - using classes and objects will also help to modulate the code
    - use functions to keep your code DRY
  - Always make a rough diagram to have a reference of what you are doing 

- **How To Write JavaScript Code**
  
  - STEP 1 : List the basic and main functionalities of your project  , 
  - STEP 2 : See the working of the Functionalities Step by Step and code the basic functionalities in execution order.
  - STEP 3 : Now look for the extra functionalities and perform STEP 2 again.
  - STEP 4 : Finally Work on your UX
  - STEP 5 : and now your code will be complete.

- **Event Delegation** 
  
  - Simply means due to event bubbling, we can target a child element and give it an event listener using the parent element
  - Its use Cases
    - When we have multiple children to add event to , we can add event listener to parent and then target the child elements we are interested in
    - When we want an event handler attached to an element that is not yet in the DOM when our page is loaded.

From here, you can start digging deeper into these concepts because this is just an overview and summary of inner working & concepts of JavaScript.

To Study JavaScript From Beginning : [**JavaScript Roadmap**](./js.md)

---