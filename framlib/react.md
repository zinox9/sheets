![Cover Image](./images/react.png)

# React CheatSheet
---
> This Sheet contains all the React v17 Concepts all the way from basics to advanced with Router and Redux + Toolkit.

---

## Basics

- React Uses a Component Based Structure to Group and render HTML accordingly

### Why Components ?

- DRY - Dont Repeat yourself = Reusability

- Separation of concerns = Not doing too many things at one place/function

### Basic Folder Structure :

- **src/** - source folder contains all the basic files
  
	- index.js = the beginning of the page rendering , first file to execute
  
	- index.css = can be imported as normal css file in index for global styling
  
	- app.js = renders basic page content in JSX, is imported in index and rendered in place of root in html
  
	- components/ = contains all the javascript files of the components you want to add and will be imported in app.js [capitalized naming]. must have only one root element returned.

- **public/** - contains the final content to be rendered on the page , not needed to edit

### JSX - JavaScript XML :

- HTML coed that is used in React , is converted/transformed into js code to render html structure.
- single curly braces in JSX can contain javascript code `{}`
- elements must be wrapped in 1 parent element before returning 
- JSX behind the scenes uses React.createElement and other functions to render HTML

### Initializing new React Project

1. You can initialize a project manually too , by simply installing react from npm packages
2. Using create-react-app - this initializes a basic project, with all the required packages already inbuilt and setup , for hot reloading, testing etc.
	- Can use `npx create-react-app <app-name>` to initialize the first basic project
3. Nowadays , we can also use **vite.js** which is a better alternative to create-react-app

### Basics React Component

```jsx
// MyComponent.js
import React from 'react'; // importing React from react is optional in sub files in latest React , because it is done in app js and inherited but doing it is good practise and to be on the safer side.
import './MyComponent.css';  // we can directly import a css file in component

function MyComponent(props) {
  return (
    <div className="my-component"> // instead of `class` in html `className` is used.
      <h1>{props.title}</h1>       // All Props are passed as an Object
      <p>{props.description}</p>
      
      <div className="content">   
	      {props.children}  // The Extra data/JSX passed can be accessed using props.children
      </div>
    </div>
  );
}

export default MyComponent;


// App.js
import React from 'react';
import MyComponent from './MyComponent';

function App() {
  return (
    <div>
      <MyComponent 
      title="My Title" 
      description="This is my description." > // Props/Attributes can be used to share data between components
      
      <p>This is some additional content.</p>  // We Can also simply pass extra data into components too
      </MyComponent>
      />  
    </div>
  );
}

export default App;


```

- Can breakdown complex groups of JSX into sub components (**Composition**) , Good practise to keep components smaller 

## States & Events

- State is used to store and manage data that can change over time, and it allows components to keep track of their own state and update their UI accordingly
- Its mutable , locally declared i.e cannot be accessed by other components without passing
- we also need state because updating normal values dosent rerender the page , therefore state is used to update the jsx and rerender the data.
-  every state in every component is handled separately and not connected and effects only its component.

###  Creating States - useState

- useState is a hook [hooks are prefixed with "use" and always used in functional components] , this one allows to create a variable, change and update variables which also update the DOM.
- the value of useState value stays even if the component is rerendered

```jsx
// Counter.js

import React, { useState } from 'react'; // useState is imported directly from react library.

const Counter = () => {
  // Declaring a state variable, initial value is used whenever the component is rendered for the first time.
  const [count, setCount] = useState(0);
  
  // useState returns 2 values that can be destructured.
  // first is the variable itself and second is a function that allows to update the variable.

  // Event handler for incrementing the count
  const handleIncrement = () => {
    setCount(count + 1); // Update the "count" state with a new value
    
    // set Action schedules the update , it takes a small time to update the specified value. 
    // therefore you cant instantly use the value right after setting it as the updation might be delayed.
    // in case of multiple set methods right after another they are batched together and executed together
  };

  // Event handler for decrementing the count
  const handleDecrement = () => {
    setCount(count - 1); // Update the "count" state with a new value
  };

  return (
    <div>
      <h1>Counter</h1>
      <p>Count: {count}</p>
      <button onClick={handleIncrement}>Increment</button>
      <button onClick={handleDecrement}>Decrement</button>
    </div>
  );
};

export default Counter;
```

### Handling Events & Forms

```jsx
import React, { useState } from "react";

const FormExample = () => {
  const [formData, setFormData] = useState({
    firstName: "",
    email: "",
  });

  // name of handler functions 
  const handleChange = (e) => { 
  // this function gets the data whenever it is called through the element
    const { name, value } = e.target;
    setFormData({
      ...formData,
      [name]: value,
    });
  };

  const handleSubmit = (e) => {
    e.preventDefault(); // we prevent the normal functionality of refreshing when form submits and add our logic.=
    alert(
      `Submitted Form Data:\nFirst Name: ${formData.firstName}\nEmail: ${formData.email}`
    );
    // Reset form fields after submitted
    setFormData({
      firstName: "",
      email: "",
    });
  };

  return (
    <form onSubmit={handleSubmit}> // All the form events have "on" prefixed to them in react
      <h1>Form Example</h1>
      <label htmlFor="firstName">First Name:</label> // for is changed to htmlFor in React
      <input
        type="text"
        id="firstName"
        name="firstName"
        value={formData.firstName}
        onChange={handleChange} // we pass the function to be called on change
      />
      <br />
      <br />
      <label htmlFor="email">Email:</label>
      <input
        type="email"
        id="email"
        name="email"
        value={formData.email}
        onChange={handleChange}
      />
      <br />
      <button type="submit" onClick={handleSubmit}> // onClick is used for Events on Buttons
        Submit
      </button>
    </form>
  );
};

export default FormExample;

```

### useRef - DOM manipulations
- useRef is mainly used to do DOM interactions directly from javascript
```jsx
import React, { useRef } from "react";

const MyForm = () => {
  const inputRef = useRef(); // Ref for input field
  const countRef = useRef(0); // Ref for mutable count value

  const handleButtonClick = () => {
    // Accessing DOM properties . here we are using it to just get values
    console.log("Input value:", inputRef.current.value);

    // Triggering DOM methods , triggering dom methods according to need
    inputRef.current.focus();
    inputRef.current.select();

    // Storing mutable value , normally useRef should not be used to update values as it does not rerender the component.
    // There it can be useful at place where only one value is needed to be change and rerender is not needed.
    countRef.current++;
    console.log("Current count:", countRef.current);
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleButtonClick}>Get Input Value, Focus Input, Increment Count</button>
    </div>
  );
};

export default MyForm;

```

- Difference in useRef and useState
	- useState can be used to store and update the form data as the user types or selects options. When both store and update is needed.
	- useRef can be used to get references to input fields, so that you can directly access their values or trigger their methods. When the data is not needed to be stored and don't want to rerender the component.


### Saving Multiple Data - Object State

```jsx
  // We have 2 options , use 3 states to save different values or have just one state with object containing all 3 values
  
  
  // Single states for name, age, and email = Multi State
  const [name, setName] = useState('');
  const [age, setAge] = useState(0);
  const [email, setEmail] = useState('');

  // Object state for user = One State
  const [user, setUser] = useState({
    name: '',
    age: 0,
    email: ''
  });

  // Event handler for updating name
  const handleNameChange = (event) => {
    setName(event.target.value);
  };
  // That's the simple way

  // Event handler for updating user object
  const handleUserChange = (event) => {
   // updating the object replaces it as a whole so we have to use the old object using spread operator
    setUser({
      ...user,
      [event.target.name]: event.target.value
    });
   // The issue here is we are using the old state, in case it is being updated at the same time we might get the wrong value for oldState because of scheduling
   setUser((prevState) => {
      ...prevState,
      [event.target.name]: event.target.value
    });
    // We solve the above issue , by using the function variation of setState which itself provides the UPDATED old value and will never be wrong. Especially helpful when running Asynchronously
  };

```

- we can also update array data in the same way too using spread and passing old value - `setItems(prevItems => [...prevItems, newItem]);`

### Passing Data - Child & Parent

```jsx
import React, { useState } from 'react';

// Child Component
const ChildComponent = ({ childData, onChildDataChange }) => { // A child component can recieve data in props
  const handleInputChange = (event) => {
    const newChildData = event.target.value;
    onChildDataChange(newChildData); // data is saved in parent onChange
    // a child component can also recieve functions from parent component, this can be used to send data to parents
    // this concept is LIFTING STATE UP
  };

  return (
    <div>
      <h2>Child Component</h2>
      <input type="text" value={childData} onChange={handleInputChange} />
      <p>Child Data: {childData}</p>
    </div>
  );
};

// Parent Component
const ParentComponent = () => {
  const [parentData, setParentData] = useState('Hello from parent!');

  const handleChildDataChange = (newChildData) => {
    setParentData(newChildData);
  };

  return (
    <div>
      <h1>Parent Component</h1>
      <p>Parent Data: {parentData}</p>
      <ChildComponent childData={parentData} onChildDataChange={handleChildDataChange} />
      // Here parent is sending the data and a function to update data , to the child
      // Passing data to child , this concept is PASSING STATE DATA
    </div>
  );
};

export default ParentComponent;

```

### Extras

#### Types of React Components

- **Stateless/Presentational/Dumb/Pure Components**
	- Pure components are components that always produce the same output for the same input props and do not have any side effects. Primarily used for rendering UI elements and do not contain any logic or state management. 
- **Stateful/Container/Smart/Impure Components**
	- Impure components, on the other hand, are components that may produce different output for the same input props or have side effects. Impure components are typically used for managing state, handling complex logic, making API calls, or interacting with the DOM.

- **Higher Order Components (HOCs)**
	- functions that take a component as input and return a new component with additional props or behavior. HOCs are used for reusing component logic, such as handling authentication, handling data fetching, or providing common functionality to multiple components.

- **Controlled Component**
	- whenever a component is connected to a state, so that we can manage data, then its a controlled component. A controlled component allows Two Way Binding , where we both use and update its data programmatically.


#### Redering Lists and Conditional Content

```jsx
// MyComponent.js - rendering lists
import React from 'react';
import DataItem from './DataItem'; // Import the child component

const MyComponent = ({ data }) => {
// here data provides us with an array of object of data that we want to render

  const renderDataItems = () => {
	// as jsx can automatically render element of arrays as html elements, we can directly return from map.
    return data.map(item => (
	  // specifying a unique key for every component is very important as it helps react to identify items individually, and not update all the items when asked to. This prevents performance issues and unwanted bugs.
      <DataItem key={item.id} item={item} /> 
      // Render the DataItem child component with props , doing this helps to breakdown the logic and make it easily changeable and reusable.
      // We should never use index as the key as it becomes inconsitent when data is changed.
    ));
  };

  return (
    <div>
      <h1>My Data Items:</h1>
      {renderDataItems()} {/* we use a function to return the list of items we want to render */}
      {/* Call the renderDataItems function to render the data items and not directly map here for a clean code */}
    </div>
  );
};

export default MyComponent;

// DataItem.js - Rendering Content Conditionally
import React from 'react';

const DataItem = ({ item }) => {
  return (
    <div>
      <p>ID: {item.id}</p>
      <p>Name: {item.name}</p>
      {item.age && <p>Age: {item.age}</p>}
      {/* && operator allows to Conditionally render age only if it exists, else its false and doesnt render */}
      {item.gender ? <p>Gender: {item.gender}</p> : null}
      {/* We can also use Ternary operator, but in most cases && does the work*/}
    </div>
  );
};

export default DataItem;


```


#### More About Forms

- Form Validation , It Can be Done in 3 ways
	1. On Every Keystroke/Value Changes - issue is this warns even before typing is completed
	2. When Input Loses Focus - issue only happens if the user misclicks and loses focus he gets error
	3. When form is submitted - allows user to enter all data, but the error feedback is too late 

- We can use the specific way to validate the form, according to our needs. Example, every key stroke for longest form or on submit for medium forms. Can be as per requirements
	
```jsx
import React, { useState } from 'react';

const FormValidationComponent = () => {
  const [formData, setFormData] = useState({
    email: '',
    password: '',
  });

  const [errors, setErrors] = useState({
    email: '',
    password: '',
  });

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setFormData({ ...formData, [name]: value });
  };

  const handleInputBlur = (e) => {
    const { name, value } = e.target;
    validateInput(name, value);
  };

  const validateInput = (name, value) => {
    let error = '';

    switch (name) {
      case 'email':
        if (!value) {
          error = 'Email is required';
        } else if (!isValidEmail(value)) {
          error = 'Invalid email format';
        }
        break;
      case 'password':
        if (!value) {
          error = 'Password is required';
        } else if (value.length < 6) {
          error = 'Password must be at least 6 characters';
        }
        break;
      default:
        break;
    }

    setErrors({ ...errors, [name]: error });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    // Perform form submission and additional validation if needed
  };

  const isValidEmail = (email) => {
    // Validate email format, you can use a library or regex for more complex validation
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
  };

  return (
    <div>
      <h1>Form Validation Example</h1>
      <form onSubmit={handleSubmit}>
        <div>
          <label>Email:</label>
          <input
            type="email"
            name="email"
            value={formData.email}
            onChange={handleInputChange}
            onBlur={handleInputBlur}
          />
          {errors.email && <p>{errors.email}</p>}
        </div>
        <div>
          <label>Password:</label>
          <input
            type="password"
            name="password"
            value={formData.password}
            onChange={handleInputChange}
            onBlur={handleInputBlur}
          />
          {errors.password && <p>{errors.password}</p>}
        </div>
        <button type="submit">Submit</button>
      </form>
    </div>
  );
};

```

- Only Frontend validation is not enough , we should always have BackEnd validation, as javascript validation can be bypassed using inspector.

- we can use custom hooks to make/validate multiple inputs in a form , because using a component the state will be handled indivually but making it a hook will allow us to bind the state to the one main form component.

- we can use packages for form handling too like , Formik or ReactHookForm



## Styling In React

- inline styling and adding classes dynamically with conditionals in JSX

- one catch about importing css files directly is that one file imported in any component , those classes can be used in any other component too = two ways to avoid this is 
- we can add styles to JSX using ... `style={{}}` the dashes are removed and names become Camel Case.
  
  - styled components 
    
    - uses tagged template literal 
    
    - and elements as method to style the element
    
    - they return a styled component of the specified element which you can use in your code
    
    - we can send props to styled components and render css dynamically in it itself
    
    - media queries can also be used in styled components
  
  - css modules
    
    - it takes the css from your css classes , and make them unique by giving it a new classname

## Debugging

1. Using Debugger = Goto Sources , file and add debugger stops whereever you want to test [this will pause the code and we can resume it after we want]

2. React DevTools = To get information about the components being used and rendered , with hooks and other info

## Fragments, Portals and Refs

### Fragments
- Used For Grouping JSX , a limitation of JSX

1. We cant return more than 1 root element in JSX.

2. We can fix this , by wrapping everything in 
   
   - div or other element , creates a div soup = unused divs inside divs just for solving this
   
   - wrapping returned components into an array , because react can render arrays of adjacent element [catch is you need a key for array of elements]
   
   - Create a Wrapper component which simply returns the props.children .. and use this around adjascent code
   
   - Wrapper comes by default as ... `<React.Fragment>` or simply `<></>` which does not render any component/code and wraps our code at the same time .. these are **React Fragments**.  

### Portals 

- Portals help to get a cleaner DOM - by reordering elements

- Modals , Overlays , Sidedrawers are rendered inside components which is not good practise to nest them because they are overlay

- We can use portals to keep the component in react at any place we want ... but render it somewhere else in html

- Usage -
  
  1. Add elements in index.html with some Id where you want to transfer your component to, you can also render out of root.
  
  2. we will use react-dom which helps to render a dom for react , which we will import ReactDOM from
  
  3. for the component that you want to render to the ID you created in index.html use `ReactDOM.createPortal(<component with props/> , document.getElementById('yourCustomElementId))`
  
  4. the props are passed down to the component so use it accordingly , i.e the component in portal passes the props to the original component
  
  5. this is the same way root is rendered in App.js ... but this time we are not rendering but portaling it

### Refs

- Refs or references allow us to get access to other DOM elements for accessing Data

- Refs can be used to store a DOM component in it itself , we can use it by 

- creating a variable with useRef ... `const inputRef = useRef()`

- and then on the html element pass a key of `ref = {inputRef}`

- now we can use this inputRef to get the state , value all the properties of the element we have added it to anytime in the code .. it always gives an object with the current key holding the element.

- an example of using ref can be to read an input directly when the submit button is pressed using , `inputRef.current.value` instead of keylogging onChange to the state and also reset the value in the same way

- NOTE : prefer to not use ref to manipulate the DOM , use it to read data and elements of DOM.

- when using Refs to access value of inputs its UNCONTROLLED ... and not controlled. because we are no  more setting the value/state of input in this case

## Side Effects/Hooks , Reducers & Context API

Side Effects = tasks that happen out of normal components rendering , Ex. Http requests , handling data

### useEffect 

- useEffect Executes a function whenever the specified dependencies changes

- `useEffect(() => {...}, [dependencies]);`

- normally open code in an component is executed everytime something is updated, with useeffect we can control when specific code is executed.

- without even specifiying any array , the useeffect will run on every state update of the component

- with an empty dependencies array in useeffect , it will run only on the start when the component is rendered and because no dependencies is given it dosent run again until the component is rendered again.

- for the useeffect to run on demand we can simply add the specific dependencies to watch and run the code when anything specified changes.

- **debouncing**  - making sure that something is not updated again and again but only once when needed. & throttling.

- cleanup function = a function that runs before the useeffect runs after the first time ... it also runs when the component is unmounted from the DOM. is usefull to clear things/data or timers not used anymore.

- we can make a cleanup funtion by returning a function in the useEffect.

### useReducer

- useReducer is useful for complex state , multiple states also when one state is dependent on other state [alternative to useState]

- usage `const [state, dispatchFn] = useReducer(reducerFn, initialState, initFn);`

- state = the normal value that we are using

- dispatchFn = a function to update the state but we pass an Action for the reducerFn to evaluate
  
  - action can be anything string or number but conventionally its an object specifying the task type and payload/value = `{type: 'SAVE_VALUE', val: VALUE}`

- reducerFn = the function which is triggerred automatically when dispatchFn is ran , it recieves latest state and runs the Action and should return updated state. 
  
  - gets Last State from react and action as arguments
  
  - we can create checks for the different actions we are using inside this reducer and take action accordingly

- initialState = is a value we want to set by default

- initialFn = is a function whose returned value we want to set in state [ex. http request]

- useEffect & useReducers
  
  - we can use object destructuring to get specific values from reducers and watch them in useeffect without the need to watch the whole reducer in the useEffect.

- useState vs UseReducer
  
  - useState = base data mgmt , for independent pieces of data and short data
  
  - useReducer = if more power needed , especially in arrays and objects updation to take care that we are using the latest state and also when multiple states are related to each other also for different actions.

### Context API 

- Context a behind the scene disconnected singular state storage for all components , that allows sharing data between components at any level

1. Create a new folder named **store** in src 

2. Create 2 files 
   
   1. **name-context.js**
      
      ```javascript
      import React from "react";
      
      // this dosent have to be object, but using object gives access to manage multiple data
      const nameContext = React.createContext({
         arr: [],
         amount: 0,
         addItem: (item) => {},
         removeItem: (id) => {},
         clearAll: () => {},
      });
      
      // this creates a component for the context that we will provide to our components and let them use it
      // this is just a prototype that lets vscode and react know that these will be value being used in the context
      export default nameContext;
      ```

3. **nameReducer.js**
   
   ```javascript
   import { useReducer } from "react";
   import NameContext from "./name-context";
   
   const defaultNameState = {
      arr: [],
      amount: 0,
   };
   
   const cartReducer = (state, action) => {
      if (action.type === "ADD") {
         //your logic 
         // can update the state directly here and action will contain the props sent with the dispatch
         const newArr = state.arr.concat(action.item);
         const updatedAmount = state.amount + 1;
         return {
            arr: newArr,
            amount: updatedAmount,
         };
      }
   
       // can add checks for other actions here
   
      return defaultCartState;
      // if the action is not specified default value will be returned.
   };
   
   const CartProvider = (props) => {
      const [nameState, dispatchNameAction] = useReducer(
         nameReducer,
         defaultNametate
      );
   
       // we could also use useState if its not complex data
       // we can also skip creating a state here and directly access context , but that brings the limitation to create local states
   
      const addItemToNameHandler = (item) => {
         dispatchNameAction({ type: "ADD", item: item });
      };
   
      const removeItemFromNameHandler = (id) => {
         dispatchNameAction({ type: "REMOVE", id: id });
      };
   
      const clearNameHandler = () => {
         dispatchNameAction({ type: "CLEAR" });
      };
   
      const cartContext = {
         arr: cartState.arr,
         amount: cartState.amount,
         addItem: addItemToNameHandler,
         removeItem: removeItemFromNameHandler,
         clearCart: clearNameHandler,
      };
   
      return (
         //this provider gives the access to all the children for the context
         <NameContext.Provider value={nameContext}>
            //the value prop gives access to all the children with the current updated value
            {props.children}
         </NameContext.Provider>
      );
   };
   
   export default NameProvider;
   ```

4. Now wrap all the components with this middleware provider , in **app.js**
   
   ```javascript
   <NameProvider>
   //other components that need to use this store
   // if we didnt create this middleware provider of ours , we would have had to add the NameContext.Provider directly where we want and manage a state at that place itself
   // creating a custom provider helps to totally isolate all the functionality at one place.
   </NameProvider> 
   ```

5. to use this context in the component , we will use a hook **useContext**
   
   ```javascript
   import useContext from 'react';
   import NameContext from '../store/name-context';
   const compo = (props) => {
       const nameCtx = useContext(NameContext);
       // now this component will be automatically reevaluated whenever CartContext changes
       // another to access context is Context.Consumer which needs a different and lengthy setup    
   
       // to access context data 
       const data = nameCtx.arr;
   
       // we can update the state simply using the functions we created to dispatch data
       nameCtx.addItem(item);
   
   }
   ```
- limitation of context = not optimized for high frequency changes / very fast updates button clicks n all
  
### Rules for hooks
  
  - only call hooks in top level and not in nested functions / if statement
  
  - Optional - try to add everything being used in useEffect to be added in dependencies.
  
  - hooks like useEffect also dont allow to add any async/promise returning data in it , we can by pass it by creating a sub function with async or simply using .then promises in it.
  
  - Can be used only in functions/components [except custom hooks]

### Forward Refs

- Forward ref is a hook that allows you to pass functionalities from children to parent using refs, to access special functionalities or values.

- because functional components cant access ref props

- useImparativeHandle hook = allows to call something in component programmitally

- usage = `useImperativeHandle(ref, () => {return {something: fnName}});`

- in above the ref is the argument ref that we got as prop in the component, and return the object value pair of the function / ref usage that we want to use.

- now to use the ref in the props because react doesnt allow it we use  in component props = `const component = React.forwardRef((props,ref) => {...})`

- now using the ref you passed in the component , you can use it in parent using refPassed.fnName

- we can also simply access the ref of the inbuilt component by assigning it to the props ref , without having to use imperative handler.

 ```javascript
  import { forwardRef, useImperativeHandle } from 'react';
  
  const ChildComponent = forwardRef((props, ref) => {
    const [state, setState] = useState(initialValue);
  
    useImperativeHandle(ref, () => ({
      reset: () => setState(initialValue),
      increment: () => setState(state + 1),
    }));
  
    return <div>{state}</div>;
  });
  
  const ParentComponent = () => {
    const childRef = useRef(null);
  
    return (
      <div>
        <ChildComponent ref={childRef} />
        <button onClick={() => childRef.current.reset()}>Reset</button>
        <button onClick={() => childRef.current.increment()}>Increment</button>
      </div>
    );
  };
  ```



## How React Works , useCallback & useMemo

- All the components created by us go through ReactDOM and are shown in RealDOM

- React uses virtualDOM , it determines what the current component tree looks like and what it should look like. ReactDOM recieves the differences and then updates the RealDOM accordingly

- Whenever State/Props/Context of a component changes , the component is reexectued

### ReEvaluation Issue

- This is a Components Issue, components logic running every time anything changes

- Re-evaluating Components !== Rendering the DOM

- React executes component function and then updates only those parts of the DOM that need to changed based on the differences.

- comparing the last snapshot with the current snapshot , and updating only specific elements.

- On every re-evaluation all the child component functions are also re evaluated.

- Note - its re-evaluating not re-rendering

- To stop functional components from being re-evaluated on every run , and only update when the prop changes we can wrap the exported functional component with `React.memo`

- Ex - `export default React.memo(FuncCompo);`

- This will make the component to only update when the recieved props are changed , and not on every parent reevaluation

- Why is it not used ? because we are trading the performance cost of not re-evaluating the component with the cost to compare its current props with the old ones.

- We can use this for huge component trees with huge logic that dosent need to be re-evaluated again and again.

- there is a catch, with the props re-execution is that it works only with primitive props, and not other props like functions, arrays.

- because when the parent is re-executed everything is recreated, comparing same primitive gives true , but no two functions or arrays are same.

- so if these are props the component is still reevaluated even if they are not changed.

### useCallback 

- used To prevent child components from re-evaluating even if functions change

- it allows us to basically save a function at one place in memory and not recreate it with every execution.

- it points every recreated function to the same location so that it dosent get changed

- to use it we can simply wrap a function with useCallback

- Example

```javascript
  const functionName = useCallback(() => {
//state updates or other code.
  }, []);
```

- UseCallback also takes an array as a dependacy like useEffect , where we add those states which will change the functionality of the function. leaving it empty means that no matter the change the function will always remain the same.

- when there are case , the  function has to be re-created because its dependent on values coming from outside the function , we have to add it as a dependancy in useCallback. or else it will keep using the original stored closure value and will never update it because of useCallback.

### States and components changes

- useState dosent change the value on every re-rendering, because useState is a react based hook which explicitly saves all the info strictly on first render and its not removed / recreated unless the component is removed and added to the dom again. same goes for useReducer.

- **State updates and Schedules** - Everytime a setState function is called to change the value of the state , the value is not changed instantly , instead it schedules the state update. this will effect the code a lot especially when there are multiple state changes and react prioritizes some state change before than the others

- The state change order is always kept, and executed in order.

- that is why a functional form of the state change is recommended to be used so that we always get the latest value

- Ex  - `setState(oldState => !oldState)`

- if we dont do this we get the state values only from the last time component was rerendered.

- we can also useanother way  than the functional way , which is by using useEffect with the dependencies states that we are using , to ensure that we get the latest value on every state change

- in case we have a 2 consecutive state updates with no delays in between [callbacks/promises] , example having them in same function , they are **batched** together and counted as a single state update causing only one rerender.

### useMemo

-  this allows to stop reexcution of specific parts of component while re-evaluation

- when we use React.memo , we control the props of the full component. But when there is one props that needs to be changed at the same time there is  performance heavy functionality that is not changed but is still executed because of one prop change.

- we can prevent this using useMemo it helps to Memoize any kind of data , that means to store any kind of data and not make it be re-excuted, the same as useCallback does for functions.

- it is used in the same way as useCallback , first argument is an anonymous function returning the performance heavy task , and second is the dependencies array which will allow to make the task run when the dependencies are changed and give the updated value.

- usage = 
  
  ```javascript
   const result = useMemo(() => {
       return array.sort((a,b) => a-b);
   }, [array]);
  ```

- and leaving it empty means the result is never changed and dosent have to be excuted again and again. adding array as dependency here means whenever the array is changed  it will be rerendered and it does change on every execution as its not primitive

- so to even prevent this array from being recreated on every execution we can simply create the value of array too using useMemo

- example = `const arr = useMemo(() => [2,5,6,10,9], []);`

- now the array will never be considered changed , empty dependency will ensure that it dosent need to be changed at all and will remain the same.

- Note - use this only for very high performance intensive tasks if needed , because using this is taking up some of your performance itself too.

## Class-based Components

- Normally we use functional component to define components which return the JSX

- The other way is to make class based component which will have a render() function that returns the JSX.

- Example - 
  
  ```javascript
  class Product extends Component {
      render() {
      return <h2>Product</h2>
      }
  }
  ```

- Functional approach is nowaydays used as default everywhere , class-based were required in past (React < 16.8) for states management components and nowaydays they are only used in case for Error boundaries

- React 16.8 brought hooks which gave class-based functionalities to functional

### Basic Usage

- A class based component show be extended from Component , to render and access this.props

- and a render() function has to be there , returning the JSX

- Class based can work together with Functional Components

### States and Events in Classes

- Functions are written in the class and not in render method

- in class based the state has to be named as state and  can only be an object nothing else.

- example 

```javascript
  constructor() {
      super()
      this.state = {
          name : "",
          bool : true,
          obj : {...}
      }
  }
  ```

- the state has to be initialized in constructor always and super needs to be called as it  is extended from Component

- for setting  the state we use this.setState();

- `this.setState({name: "Aj"})` in case of class based the object is not overwrited but merged so other data stays even if we change only one thing, 

- we can get the old value of state the same way as useState -

- `this.setState((oldState) => {name : oldState.name + "12"})`

- we can define helper functions that render specific JSX in render method

- in class based , we have to use state also using this.state.name

- while passing functions in javascript we have to call them using "this" and also bind the class "this" to it if we are using it in function.

- `<button onClick={this.toggle.bind(this)}>`

### Class-based Lifecycles

- Class based dont use hooks but lifecycle methods

- componentDidMount() = Called once component is mounted [evaluated and redered ] = useEffect(..., [])
  
  - this runs only once when the component is rendered for the first time.

- componentDidUpdate() = called once component was updated / state changed = useEffect(...,[someValue]);  
  
  - in the didUpdate function props we can get prevProps and prevState to compare specific state values and update accordingly
  
  ```javascript
    componentDidUpdate(prevProps, prevState){
        if(prevState.value !=== currentValue){
        //other code only executed if this value changed.
        }
    }
    ```

- componentWillUnmount() = Right before component is unmounted = cleanup in useEffect 

### Context in Class based

- Class-based can use Context in almost the same way as functions, only change is how we use it , without useContext() and we can connect only one Context to a single classBased component.

### Error Boundaries - Best use case for class-based

- generally whenever we throw an Error at any place , the app crashes with error , or we use try catch

- For this we can create a new class based component , example named ErrorBoundary and give it a lifecycle method `componentDidCatch()` and this does not have any hook for now.

- `componentDidCatch(){}`  this method is executed whenever any child throws an error.

- Example - 

```javascript
  class ErrorBoundary extends Component {
      constructor() {
          super();
          this.state = {hasError: false}
      }
      componentDidCatch(error){
          this.setState({hasError: true})
      }
      render() {
      if(this.state.hasError){
          return <p>Something Went Wrong</p>
      }
          return this.props.children;
      }
  }
  ```

- and now we can wrap our components in this component and whenever an error is thrown , this will catch and handle them.

## How to connect to Backend DB , using Https Requests

- FrontEnd/React doesnt directly connect to a Database because of security conditionals and performance that is why a backend app(node,php) is used as mediator between react and db.

- Sending requests can be done in 2 ways 
  
  - Axios package
  
  - Fetch Api = already available by browser

- Sending GET request 
  
  - `fetch('url');` is by default a get request. and then we get a response with a delay that is why we can use promises.
  
  - we can use 
  
  ```javascript
    fetch('url').then(response => {
        return response.json(); //this is also delayed and sends a response
    }).then(data => {
        console.log(data.results);   
    });
    ```

- Async/Await 
  
  - It is a replacement of .then and .catch block , a javascript feature that we can simply use with react.

- We can simply handle loading states and errors to show loading data  or error while requests are being made.

- Handling Errors 
  
  - 2xx codes = accepts
  
  - 4xx / 5xx responsed might have to be handled
  
  - We can catch errors using `.catch`  for .then or try catch for async await
  
  - **Fetch** dosent give an error for error status codes whereas axios can catch it.
  
  - To check for errors in fetch , we have to check response.ok or response.status and throw error manually

- Sending POST request
  
  - fetch takes a second argument with object where we can send post request and the data to be sent
  
  ```javascript
    fetch('url', {
        method: 'POST',
        body: JSON.stringify(data), //this sends data as json 
        headers:  {
        'Content-type' : 'application/json' //tells that data is json
        }
    })
    ```

## Custom React Hooks

- Custom hooks are simply functions containing stateful logic , that can use other hooks and react state.

- We can use custom hooks when we have shared functionality between multiple components that are using hooks too 

- Usage
  
  - We should create a separate file for the customhook in a folder named 'hooks' in src, and a must rule is for the function to start with 'use' this tells react that it is going to use other hooks.
  
  ```javascript
    const useCustom = () => {
        //code with states and hooks that you want to use at multiple places
    }
    ```
  
  - Now we can simply use our hook based code in our custom hook and use that at the place that we want by simple calling it like a function.
  
  - When we call a custom hook in a component the state and hooks of it are tied to that specific component, and not common between all components.
  
  - as the custom hook is tied to the function it is used in , it will re-evaluate on every change of the custom hook too. that is why we can use useCallback & useMemo to save it from re-rendering if needed.
  
  - we can return any state/number/variable from a custom component the the component that we want to use it in.
  
  - we can simply pass arguments/parameters to the custom hook for different use cases.
  
  - dont forget to update the inside hooks of custom hook , with dependencies of props

## Redux - State Management , App wide

- Local State - data in single component = useState and useReducer

- Cross-Component State - affects multiple components = uses props to transfer state [useState, useReducer]

- App-Wide State - state that effects entire app = prop chains , context , redux

- Why Redux in place of Context ?
  
  - context has some disadvantages that redux can fulfill [therefore we can use both also too]
  
  - context can become very complex because of multiple providers
  
  - context is not that performant , not good for high frequency changes

- How does Redux Work
  
  - Redux always has all the data at one central store [state]
  
  - Components make a subscription to get the data directly from store
  
  - To update the store data , we have Reducer Functions which mutate /change the data
  
  - Components dispatch/trigger actions with descriptions which forward info to reducer and update the store.

### Basic Redux without React

Redux is based on observer pattern , which is the reason why it is able to do state updates as its able to observe all the changes in the state.

1. install - `npm install redux`

2. Create a reducer , with initial state and actions to perform
   
   ```javascript
     const nameReducer = (state = {counter : 0}, action)=> {
         if(action.type === "..."){
              return {
                 counter: state.counter + 1,
             }
         }
         //and so on state updates
     }
     ```
   
   - automatically called by redux, always recieves old/existing state and  an action. 
   
   - it should always return a new state object 
   
   - it should be a pure function , without any calls / hooks

3. Create a store pointing at the reducer 
   
   ```javascript
     import {createStore} from 'redux'
     const store = createStore(nameReducer);
     ```

4. Create a subcriber which gets triggered on every action and can get state 
   
   ```javascript
     const nameSubscriber = () => {
       const latestState = store.getState();
     }
     ```
   
   - it is a function does not get any parameter , but can get the state in this because it gets triggered everytime a state update occurs.

5. subscribe your subscriber to the store
   
   ```javascript
     store.subscribe(nameSubscriber);
     ```
   
   - this function redux calls everytime state update occurs

6. now simply dispatch your actions to the store to perform actions on state
   
   ```javascript
     store.dispatch({type: 'increment'});
     ```
   
   - this calls reducer to run again and that calls the subscriber.

### Using Redux With React

- `npm install redux react-redux` to install redux in the project

- Create a folder "store" in your src for redux

- Create a file to create your store. ex-index.js
  
  ```javascript
  import {createStore} from 'redux'
  
  // Create a reducer , with initial state and actions to perform
  const nameReducer = (state = {counter : 0}, action)=> {
       if(action.type === "..."){
           return {
               counter: state.counter + 1,
           }
       }
       //and so on state updates
  
      return state;
   }
  
  //automatically called by redux, always recieves old/existing state and an action.
  // it should always return a new state object
  // it should be a pure function , without any calls / hooks
  
  const store = createStore(nameReducer);
  
  //this helps us access the specific state.
  export default store;
  ```

- Next we need to wrap out app with a provider that will give all the components of the app access of the store
  
  ```javascript
  //in app.js
  //other imports ...
  import {Provider} from 'react-redux'
  import store from "./store/index";
  
   ReactDOM.render(
        <Provider store={store}>
            <App />
        </Provider>,
        document.getElementById('root')
   )
  ```

- Next in the component that we want to use the store in , we need to import a hook useSelector
  
  ```javascript
  import {useSelector} from 'react-redux';
  
    const compo = () => {
  
        const counter = useSelector(state => state.counter);
        //like this we can get specific state data we want too
        //useSelector manages creation of subscription for state updates automatically
        // it creates a subscription when component is mounted and updates the data on its own
        // it also unsubscribes when the component is removed from DOM 
  
        //... other code
        // can simply use the counter data normally we will get updated on its own
  
    }
  ```

- To update this state in react redux, we use useDispatch hook which will help us to send actions to the store reducer
  
  ```javascript
    const dispatch = useDispatch(); 
    //this returns a dipatch function with which we can call the redux store
    const increment = () => {
        dispatch({type: 'increment'});
    }
  ```

### Redux with Class-Based Components

- with useDispatch and useSelector react-redux also gives another function named **connect** to connect class based components with redux

- connect needs 2 arguments = 
  
  - first is a function **mapStateToProps** which gets the redux state as an argument and the keys are passed to the component as props
  
  - second is another function **mapDispatchToProps** gets dispatch as an argument and in this we can send function as props to the component and call the dispatch actions

- Usage
  
  ```javascript
  import {connect} from 'react-redux';
  class Counter extends Component {
      //we can use the data sent in props props
      incrementHandler() {
          this.props.increment(); //accessing the dispatch function
      } 
  
      value = this.props.counter; //accessing the value
  
      //other code...
  }
  
  const mapStateToProps = state => {
      return {
          counter: state.counter 
          // accessing the redux state , keys are passed as props
      }
  }
  // function names can be anything , but this is conventional
  const mapDispatchToProps = dispatch => {
      // this function will recieve the dispatch
      return {
          increment: () => dispatch({type: 'increment'}),
          decrement: () => dispatch({type: 'decrement'})
      }
  }
  
  export default connect(mapStateToProps, mapDispatchToProps)(Counter);
  ```

### Attaching payloads to Actions

- we can simply get data in the reducer in the actions , by passing data while dispatching in component

```javascript
  // in the reducer simply access the value using action
  const nameReducer = (state = {counter : 0}, action)=> {
     if(action.type === "ADD"){
         return {
             counter: state.counter + action.amount,
         }
     }
  }
  ```

```javascript
  // now add the data while dispatching from the component
  dispatch({type: 'ADD', amount: 5});
  // this amount will be accessible in the reducer 
  ```

### Working with multiple state properties

- to have multiple states in the reducer and work with them specifically

```javascript
  // in the file with your reducer 
  
  // creating an overall initial state
  const initialState = {
      counter: 0,
      showCounter: true
  }
  
  const counterReducer = (state = initialState, action) => {
  
      if(action.type === 'ADD') {
          // never update the existing state directly because it is a reference , it can work but it can cause unforeseen issues
          return {
              counter: state.counter + 1,
              showCounter: state.showCounter
              // we are having to specify the full state because react dosent merge it instead it just updates the overall state with what we return    
              // always return a brand new object with all the properties
          }
      }
  
      if(action.type === 'toggle'){
          return {
              showCounter: !state.showCounter,
              counter: state.counter
          }
      }
  
      return state;
  
  }
  
  const store = createStore(counterReducer);
  export default store
  ```

- Now we can simple access these values using useSelector in the component we want.

### Redux Challenges

- having to remember all the action names

- a huge state object at one place for bigger projects

- having to return the whole state again everytime a change happens

- all of these issues can be solved using manual minor fixes , but there is better way that is to use Redux Toolkit

## Redux Toolkit

- It is made by the same team of redux , to make things easier to use and not  a must use

- installation - `npm install @reduxjks/toolkit` , you can now remove redux from you packages , as this already has it.

### How to create Slice in Toolkit

- In the file where we created the reducer, example `store/index.js` 

- we have createReducer and createSlice [more powerful] in @reduxjs/toolkit

- createSlice = we prepare a slice of global state , of data that is not connected and in pieces

```javascript
    import {createSlice, configureStore} from '@reduxjs/toolkit';
  
    // 1. Create slice for the state you want
    // createSlice wants an object as argument
    const counterSlice = createSlice({
        name: 'counter', //any custom name that you wish,
        initialState : {counter: 0, showCounter: true}, // this gives it an initial value to start with
        reducers: { // this takes all the reducers we need to perform state updates
            increment(state){ // we dont need if checks here , cause we can directly access these 
               state.counter++; // toolkit uses immer which automtically mutates and does the update , so we can directly work with the state without having to copy it
            },
            increase(state,action){
               state.counter += action.payload; // toolkit automatically attaches any data in a property names payload which cannot be changed
            }
        }
  
    })
  
    const initialAuthState = {
        isAuthenticated: false,
    }
  
    const authSlice = createSlice({
        name: 'authentication',
        initialState : initialAuthState, 
        reducers: {
            login(state) {
                state.isAuthenticated = true;
            },
            logout(state) {
                state.isAuthenticated = false;
            }  
        }
    })
  
    // 2. To let the store know about the slice and reducer to use
    const store = createStore(counterSlice.reducer);
    // this is good if we have just one slice but when we are working with multiple slices
  
    // 2. We can use configureStore in toolkit, alternative to combineReducers of redux to send multiple reducers in state.
    const store = configureStore({
        // reducer : counterSlice.reducer   // this is in case of one main reducer
        reducer : { 
            counter : counterSlice.reducer,
            auth: authSlice.reducer
        }
        // this can be used for multiple slices, these slices will be merged together and used in store automatically
    });
  
    export default store;
  ```

### Dispatching Actions in Slice of Toolkit

- createSlice automatically assigns the reducer functions to the slice as actions through which we can access the methods

```javascript
  counterSlice.actions.increment();
  // toolkit creates action objects when we call these reducers , 
  // which are unique by default, that is why these are also called action creators
  // these returned objects will already have uniques properties automatically being handled behind the scenes.
  // that is why we dont have to worry about creating unique actions and adding if else
  ```

- to access these actions we will have to export them too and import where we want to use them

- in the file where you created your reducer ... example `store/index.js`

```javascript
  export const counterActions = counterSlice.actions;
  export const authAction = authSlice.actions;
  ```

- now in ther component you want to use these , we dispatch the unique object returned by these actions 

```javascript
  import {counterActions} from '.../store/index';
  import {useSelector , useDispatch} from 'react-redux'
  
  const Counter = () => {
      // const counter = useSelector(state => state.counter);
      // if single slice is in store, we can also simply access our redux state in the same old way
      const counter = useSelector(state => state.counter.counter);
      // we have to specify the key of that slice when multiple are set
      const authenticated = useSelector(state => state.auth.isAuthenticated);
  
      const dispatch = useDispatch();
  
      const incrementHandle = () => {
          dispatch(counterActions.increment());
      }
  
      const increaseHandle = () => {
          dispatch(counterActions.increase(10)); 
          // example dipatches {type: UNIQUE_IDENTIFIER, payload: 10}
          // this value is automatically stored in payload and can be access only as payload
          // we can also send any data , array object anything in place of 10 and access as payload
      }    
  }
  ```

### Splitting Up Toolkit Codes

- We can separate slices into different files in the store

- export the slice ... `export default authSlice`  .... we cann also just export the reducer

- and then import it for the store in index

- `import authReducer from './auth'`

- also shiting specific actions into their specific files.

## Advanced Toolkit

### Handling Async Tasks and Side Effects with Redux

- Reducers have a rule , tht they must be pure , synchronous and no side-effects

- this is why it is not allowed to add async functions in our redux reducers

- now we have 2 options to handle side-effects and async tasks
  
  - Write in useEffect etc of components and dispatch only the results
  
  - Make our own **action creators** instead of using the default ones of toolkit

### Adding async calls to the component directly

- Adding async calls in components directly with the transformations of data is not recomended as
  
  - as we have add all the exact same logic of the reducers in the component before sending it to backend
  
  - we wont be able to mutate state as in reducers , because toolkit is not being used in the components

- Fat Reducers vs Fat Components vs Fat Actions
  
  1. Synchronous and pure code = Prefer reducers , avoid  action creators and components
  
  2. Async Code and side effects = Prefer Action creators and components , avoid reducers doing the work

. Another good way is creating async call using the useEffect in a component

  . we get data using UseSelector of the cart

  . watch changes in the cart and add the async call using useEffect

  . therefore everytime the cart changes useEffect will perform the async call

  . we will have to also check if it is the first call or not as , useEffect will be called the first time App.js is rendered too / when cart is created.

### Adding Async calls using Action Creator Thunk

- Right now action creators are being used automatically by toolkit when we are using the reducers given by the toolkit

- To create action creators manually - we use Thunk

- What is Thunk 
  
  - A function that delays an action until later
  
  - An action creator function , which does not return the action data directly but another function which will return the action

- Using Thunk
  
  - Go to the end of the creation of slices to create an async thunk middleware
    
    ```javascript
    const cartSlice = createSlice({...})
    
    export const sendCartData = (cartData) => {
        // return {type: '', payload: 0} // this was done by toolkit automatically
        return async (dispatch) => { // now we can use async await here because we are not in reducer yet and we are performing actions before sending the data to the reducer
            dispatch(cartActions.setStatus({status: "Fetching Data..."}));
    
            const response = await fetch('url', {...});
    
            if (response.ok)
                dispatch(cartActions.setStatus({status: "Fetching Complete});
            else 
                dispatch(cartActions.setStatus({status: "Error Occured"});    
        }
    }
    ```
  
  - now in a cart watching useEffect in App.js
    
    ```javascript
    useEffect(() => {
     if(isInitial){
        isInitial = false;
        retun;
     }
     dispatch(sendCartData(cart)); //this sends the updated cart info
     // Redux toolkit allows us to send a function as an action which returns another function
     // Toolkit itself handles the function action and give it the access to dispatch in it too , for performing actions there
     // redux will go and call the function we made in slice itself
    }, [cart,dispatch]);
    //vs code will suggest to add dispatch here , adding it is no issue as it stays as the same function everytime and wont trigger the useEffect
    ```
  
  - as thunk actions will increase , we can create a separate file cart-actions.js that will store all these thunk functions.

## Redux DevTools

- We can simply install a ReduxDevTools as an extension in browser

- If we used redux without reduxToolkit we had to make a setup for DevTools to work , but with toolkit no setup is needed it works out of the box

- With this we can see all the actions dispatched .. and all the data updates of redux. also controlit manually in browser

---

## Router

- Changes the conventional routing , of rendering/fetching multiple html  pages. But rendering the html content using react by conditionally checking the route of the page. 

- The third party package that helps us do this is react-router 

- To install `npm install react-router-dom`

### Basic Usage

1. Wrap your app with the BrowserRouter Component, to activate react router features in index.js
   
   ```javascript
   import {BrowserRouter} from 'react-router-dom'
   
   //...
   
   
   root.render(
   
   <BrowserRouter>
       <App />
     </BrowserRouter>
   );

```
2. Import Route in your app.js and set the routes for components accordingly

```javascript
import {Route} from 'react-router-dom';


//import Home component
//import other components
// as above components will be loaded as pages , we can store them
// in a different folder named pages or screens.

function App() {
    return (
        <div>
            <Route path="/">  //yourDomain.com/
                <Home/>
            </Route>
            <Route path="/other"> //yourDomain.com/other
                <Other/>
            </Route>
        </div>
    )
}

export default App;
```

### Working With Links and NavLinks

- We cannot simply set the Links to redirect to the route , because that refreshes the page and resets all the info.

- for this react-router has Link component to be used for routing links , prevent browser default , persist the  changes and prevent refreshes

- Usage of basic Link - 
  
  ```javascript
  import {Link} from 'react-router-dom';
  
  
  const Header = () => {
  
      return (
          <header>
              //nav ul li ...
                  <Link to='/home'>Home</Link>
                  <Link to='/products'>Products</Link>
          </header>
      )
  
  }

```
- Link dosent give any classes to the element, react-router also gives a NavLink component which allows us to add a class to the active link

```javascript
import {NavLink} from 'react-router-dom';

// ... imports , component data ... in the component


<NavLink activeClassName={classes.active} to='/home'>
Home
</NavLink>
```

### Dynamic routes and params

- In case of rendering a list of items and redirect to details page of each item , we can create page for each product with dynamic routes and pass parameters to it.
  
  ```jsx
  <Route path='/item-details/:itemId'> 
      <ItemDetails/>
  </Route>
  // this means we can load , domain/item-details/anything
  // whatever we write in anything , /item1 , /p2123w 
  // will redirect us to the item details page
  ```

- We can retrive the custom details passed in the route using `useParams` hook . in the detail page that we loaded =
  
  ```javascript
  import {useParams} from 'react-router-dom'
  
  const ItemDetail = () => {
      const params = useParams();
  
      console.log(params.itemId); 
      //we can access multiple custom params using this key that we provided in the route
      // example /:itemId/:itemPrice
  }
  ```

- When multiple routes match the current path all will be loaded. example - /products will list products and /products/id will render specific product. but both will be rendered at the same time cause both match /products

- **React router matches from top to bottom and from start of the path not the enitre path.**

- For this we have `Switch and Exact`
  
  ```jsx
  import { Route, Switch } from 'react-router-dom';
   // Switch makes it that only one of the matched routes are rendedered and not all
  // but because of router functionality , the first one in order will be rendered which is not always right
  // for that we can use exact which will only let the route render if its exactly the same.
  <Switch>
      <Route path='/welcome'>
         <Welcome />
      </Route>
      <Route path='/products' exact>
          <Products />
      </Route>
      <Route path='/products/:productId'>
           <ProductDetail />
      </Route>
  </Switch>

  ```

- We can also use dynamic javascript in the Routes

### Nested Routes & Redirects

- React Router allows us to make routes anywhere in any component

- We can define Route inside of components , and render specific data only in it when the component is loaded 

```jsx
 <section>
    <h1>The Welcome Page</h1>
    <Route path="/welcome/new-user">
      <p>Welcome, new user!</p>
    </Route>
</section>

 // this will allow us to load the paragraph when , the new user route is added to welcome page.
```

- We can also Redirects to redirect a user to a page that we want to
  
  ```jsx
  import {Redirect} from 'react-router-dom';
  // exact is needed or else route will always match and loop it.
  <Route path='/' exact> 
   <Redirect to='/home'>
  </Route>
  ```

### Extras

- We can create a custom layout component for the basic layout to be used with all routes content .. and wrap our conditional route data in it.
  
  ```jsx
  <Layout> //containing navbar and props.children to render these inside components
      <Switch>
          <Route path="/home"><Home/></Route>
          <Route path="/other"><Other/></Route>
      </Switch>
  </Layout>
  ```

- We can also simply use Route anywhere just as an if else to render dynamic content according to the current route.

- **NOT FOUND PAGE** , to create a not found url catch
  
  ```jsx
  // add a route at the end of all your routes already created that
  // will catch all the remainging url and render not found page
  
  // this will work because react matches routes from top to bottom
  <Switch>
      <Route path="/home"><Home/></Route>
      // after all the routes at end add
      <Route path="*">
          <NotFoundPage />
      </Route> 
  </Switch>
  ```

- **useHistory** is a hook provided by react-router which allows us to programatically navigate through pages using javascript, and not by just Link/NavLink
  
  ```javascript
  import { useHistory } from 'react-router-dom';
  
  const Component = () => {
      const history = useHistory();
  
      history.push('/other'); // sends to next page and allows the user to go back as it is pushed in history
      history.replace('/other'); // sends to the next page and dosent allow the user to go back to previous page
  }
  ```

- **Prompt** components is used to give user an alert when he is leaving a page/accidentally pressed back button while filling a form.
  
  ```jsx
  import { Prompt } from 'react-router-dom';
  
  <Prompt
      when={isFillingForm} //if this this true then the user will be prompted if he tries to leave the page
      message={(location) =>
        'Are you sure you want to leave? All your entered data will be lost!'
      }
  />
  ```

- **useRouteMatch** gives the inner react-router based info about current route & **useLocation** gives the browser level current route info
  
  ```javascript
  const match = useRouteMatch();
  const location = useLocation();
  ```
  
  // match will have the url , but also our made param :itemId and parameter
  // location will have the url and route only
  
  // using match for current page url in nested routes 
  // allows us to manage routes only on the first level and all others will be automatically updated

- React router also offers a custom way to write the url , not just by using string but by

```javascript
history.push(`${location.pathname}?sort=${(Ascending ? 'asc' : 'desc')}`);

//can be written as

history.push({
   pathname: location.pathname,
   search: `?sort=${(Ascending ? 'asc' : 'desc')}`
});
```

### Query Parameters

- when we just need to pass data and not make that part of the route but have it in url to be shareable.

- **useHistory** can be used to add query parameters to the current page

- **useLocation** can be used to get the current pathname with the query parameters.
  
  ```javascript
  import {useLocation, useHistory} from 'react-router-dom';
  
  // in the component
  const history = usehistory();
  const location = useLocation();
  
  history.push('/page?sort=asc'); 
  // this will still rerender the current component even if we are in it
  
  const queryParams = new URLSearhParams(location.search);
  // this is built in constructor class of browser, which will return our query params as object
  
  const sortAsc = queryParams.get('sort') === 'asc';
  // now we can simply use the current param value
  ```

### Version 6 Changes

- Video reference = [React Router 6 - What Changed &amp; Upgrading Guide](https://www.youtube.com/watch?v=zEQiNFAwDGo)

- **Switch** is replaced with **Routes**

- **Route** is now self closed and the component is now passed with element prop
  
  - `<Route path='/home' element={<Home />} />`

- Internal logic for selecting the routes has been changed and **exact** is no longer needed, Router V6 loads the url automatically if its exactly whats written.

- Now router also selects the best path automatically 
  
  - `name/*` will not be loaded even if its declared before a `name/:id` cause we have manually specified that we are expecting text after it
  
  - `name/edit` will be loaded even if `name/:id` is declared before it. As now router will look at what the very exact match is best for it.

- **NavLink** activeClassName prop is removed , now we have to manually find out if the link is active, we can do this by
  
  ```jsx
    // className can take a function in Navlinks now which will give the nav data to it.
    
    <NavLink className={(navData) => navData.isActive ? classes.active: ''} to='/home'>
      Home
    </NavLink>
    ```


- **Redirect** is replaced with Navigate
  
  ```jsx
    <Route path='/' element={<Navigate to='/home'/>} />
    // this will push the next page into history
    
    <Route path='/' element={<Navigate replace to='/home'/>} />
    // this will work exactly like the old redirect and replace the history
    ```

- Now nested **Route** also need to be wrapped in **Routes** 

- Because of new logic of choosing routes , to access nested routes
  
  1. we have to write `/home/*` in the main route to catch all the nested routes inside.
  
  2. in the inner component containg the nested route , we no more have to write `/home/nest` instead normally `nest` in the path and react will understand it because now it is relative.
  
  3. This also effects the **Links** inside components , their path is also relative now.

- Another option to make nested routes , is by adding Route children in the main app.js

  ```jsx
    // in app.js

    <Route path='/home/*' element={<Home/>}>
        <Route path='other' element={<Other />} />
    </Route>
    
    
    // to define where the nested content has to be rendered , in home.js
    // A new component OUTLET is available and will be simply replaced with the nested content
    
    <section>
        <Outlet/>
        <h1>Hi</h1>
    </section>
    ```

- **useHistory** is no longer there in v6 and is replaced with **useNavigate**
  
  ```js
    const navigate = useNavigate();
    navigate('/home'); // will push into history
    navigate('/home', {replace: true}); // will redirect/replace in history
    
    // forward and backward navigation is also possible by
    navigate(-1) // backward
    navigate(1) // forward
    ```

- **Prompt** component also no more exists in v6

- For even more latest and better changes of v6.4 = [React Router 6.4 - Getting Started](https://www.youtube.com/watch?v=L2kzUg6IzxM)

## Deployment

- Before deployment steps 
  
  1. Test Code
  
  2. Optimize Code - and add Lazy Loading
  
  3. Build App for production
  
  4. Upload Production Code to Server
  
  5. Configure Server

### Adding Lazy Loading

- Most of the bundles are download on first render of the website.

- Lazy loading is divinding the code into chunks and only downloading them when speicific route/functionality needs it.

- To use it 

```js
  import React from 'react';
  
  const NewPost = React.lazy(() => import('./pages/NewPost'));
  // this will make the app to not import this component right when the app is loaded
  // instead the component will only be downloaded when it is being rendered
  
  <Route path='/new-post'>
    <NewPost />  // the component is downloaded only when this URL is hit.
  </Route>
  ```

- This rises and issue that , when the page is loaded it is going to take time to download the component. So react needs a fallback UI to show at the mean time.

- For this we have **Suspense** Component

- We Wrap all of our code where we will use lazy loading and define what has to be shown in the mean time

```jsx
  import {Suspense} from 'react';
  
  <section>
      <Suspense fallback={<p>Loading...</p>}>  // can define any jsx in here
      // other elements/components inside
      </Suspense>
  </section>
  ```

### Building and Uploading for production

- create-react-app already has  script , **npm run build**   in package.json which will minify/optimize all our codes into one build folder which we can deploy at any server we wish.

- We can also directly deploy our react project on netlify, using github repository and set it up to run build command itself and use the build command for production , this allows us to get CI/CD too.

- We can use any other static hosting provider too by only deploying our build folder.

### Server Side Routing and Client Side Routing

- In case of react , we make Single Page Applications. All the routing and urls are handled by the js provided by our main URL. therefore we use only one URL

- In case of multi-page-apps , different pages are rendered by hitting different URLs therefore that dosent need any setup.

### Some Places to deploy your React Code at

- Netlify - free

- Vercel - free

- Firebase

- Heroku

- AWS

## Tests in React

- Manual Testing - Writing code and testing it right there , this method is error-prone because we cant test all scenarios and combinations manually

- Automated Testing - We write code that will run and test all the building blocks of our project one by one multiple times automatically
  
  - Unit Tests -  Test the most basic components / functions in isolation [most used/important]
  
  - Integration Tests - Test  combination and working of modules with each other
  
  - End to End Tests - Test complete scenarios of user flows , can be done manually and is mostly completed by integration and unit tests itself

### Tools

- For running the tests , example Jest

- For Simulating things on the screen , react testing library 

- both are available in create-react-app out of the box

### Writing Tests

- Arrange - Set up the test data , conditions and environment

- Act - Run the logic to be tested (a function)

- Assert - Compare execution results with expected values

### Example

- Create a sample component 

```js
  //Greeting.js
  import React from 'react';
  
  function Greeting({ name }) {
    return (
      <div>
        <h1>Hello, {name}!</h1>
      </div>
    );
  }
  
  export default Greeting;
  ```

- Now write a test for the component

```js
  //Greeting.test.js
  import React from 'react';
  import { render,screen } from '@testing-library/react';
  import Greeting from './Greeting';
  
  test('renders a greeting message with the provided name', () => { 
  //test funtion is offered by jest , and here we write the test name
    const { getByText } = render(<Greeting name="John" />); 
  // we render the component on screen
    const greetingMessage = screen.getByText(/Hello, John!/i);
  // now we select the component
   expect(greetingMessage).toBeInTheDocument(); 
  //expect helps us asser the resulta and check if the check has passed
  });
  ```

- Now we can run the tests using `npm test`

### Testing Suites

- We can group multiple tests into one test suite to organize tests together

```js
  describe('Button component', () => {
    test('displays the button label', () => {
      const { getByText } = render(<Button label="Click me" />);
      const buttonElement = getByText(/Click me/i);
      expect(buttonElement).toBeInTheDocument();
    });
  });();
  });
  ```

- Here we can put multiple Tests into the describe function , to group them together into one suite

### User Events testing

- we can simulate userEvents and run tests accordingly by

```js
  import React from 'react';
  import { render, screen } from '@testing-library/react';
  import userEvent from '@testing-library/user-event';
  import LoginForm from './LoginForm';
  
  describe('LoginForm component', () => {
    test('disables the submit button until both fields are filled in', () => {
      render(<LoginForm />);
      const usernameInput = screen.getByLabelText(/username/i);
      const passwordInput = screen.getByLabelText(/password/i);
      const submitButton = screen.getByRole('button', { name: /submit/i });
  
      // Verify that the submit button is disabled initially
      expect(submitButton).toBeDisabled();
  
      // Simulate user input in the username field
      userEvent.type(usernameInput, 'johndoe');
  
      // Verify that the submit button is still disabled
      expect(submitButton).toBeDisabled();
  
      // Simulate user input in the password field
      userEvent.type(passwordInput, 'password123');
  
      // Verify that the submit button is now enabled
      expect(submitButton).not.toBeDisabled();
    });
  });
  ```

### Integration test

- The render function used to render a component, automatically runs the subcomponents used in a component and performs the required checks

### Asynchronous Testing

- For Asynchronous , Promises , we can use "screen.find" in place of "screen.get/query" as this returns a promise. and runs the tests multiple times for a certain time period which can also be specified.

- To successfully use the find function we will also have to convet the test function into an async function and await for the "screen.find" to complete the testing.

### Mock Requests

- As we should not send requests to the actuall server while testing as that will send invalid data into the live server , we have  2 options
  
  1. To not send the request at all and just check our local code if the component is not crashing
  
  2. To send a request to a fake database for testing purpose

. To skip sending a request , we can replace out fetch with a Mock Function 

- Example -

```jsx
  import React from 'react';
  import { render, screen } from '@testing-library/react';
  import UserList from './UserList';
  
  describe('UserList component', () => {
    test('fetches and displays a list of users', async () => {
      const mockUsers = [
        { id: 1, name: 'John Doe' },
        { id: 2, name: 'Jane Smith' },
      ];
      //this  replaces the fetch in the window , with a mock function
      // proviced by jest, and then create our own response to work with
      global.fetch = jest.fn(() =>
        Promise.resolve({
          json: () => Promise.resolve(mockUsers),
        })
      );
      
      render(<UserList />);
      
      expect(screen.getByText(/user list/i)).toBeInTheDocument();
      
      const userListItems = await screen.findAllByRole('listitem');
      expect(userListItems).toHaveLength(2);
      
      // Verify that fetch was called with the correct URL
      expect(fetch).toHaveBeenCalledWith(
        'https://jsonplaceholder.typicode.com/users'
      );
  
    });
  
  });

```

## THE END