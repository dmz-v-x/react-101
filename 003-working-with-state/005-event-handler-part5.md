## Event Handler - Part 5

# Step 1 — React’s Event Object (SyntheticEvent)

When you interact with the UI (click, type, submit, etc.), React passes an **event object** to your handler.

This is similar to the browser’s event system, but React adds an abstraction.

---

# Step 2 — Basic Example

    function App() {
      function handleClick(event) {
        console.log(event);
      }

      return <button onClick={handleClick}>Click me</button>;
    }

---

## What happens when you click?

- handleClick is called  
- React passes one argument  
- That argument is the event object  

---

# Step 3 — What is this event?

## In plain JavaScript

- Browser provides a **native DOM Event**

---

## In React

- React provides a **SyntheticEvent**

---

## Definition

SyntheticEvent = React’s wrapper around the native browser event

---

## Why React uses SyntheticEvent

- Ensures consistent behavior across browsers  
- Provides a unified API  
- Enables internal performance optimizations  

---

## Important note

For almost all use cases:

SyntheticEvent behaves exactly like a normal browser event.

---

# Step 4 — Common Properties You Will Use

### Example

    function handleClick(event) {
      console.log(event.type);   
      console.log(event.target); 
    }

---

## Frequently used properties

| Property                  | Meaning                                      |
|--------------------------|----------------------------------------------|
| event.type               | Type of event ("click", "change", "submit")  |
| event.target             | Element that triggered the event             |
| event.currentTarget      | Element where handler is attached            |
| event.preventDefault()   | Stops default browser behavior               |
| event.stopPropagation()  | Stops event bubbling                         |

---

# Step 5 — Real-World Example: Form Submit

    function handleSubmit(event) {
      event.preventDefault();
      console.log("Form submitted!");
    }

    return (
      <form onSubmit={handleSubmit}>
        <button>Submit</button>
      </form>
    );

---

## Why use preventDefault()?

Default browser behavior:

- Submitting a form reloads the page  

In React:

- We usually do not want a page reload  
- We handle the logic ourselves  

So we stop the default behavior.

---

# Step 6 — Example: Input Change

    function handleChange(event) {
      console.log(event.target.value);
    }

    return <input onChange={handleChange} />;

---

## What is happening here?

- event.target → the input element  
- event.target.value → current text inside input  

---

## Important pattern

This pattern is fundamental in React and used frequently.

---

# Step 7 — target vs currentTarget (Important Distinction)

### Example

    function handleClick(event) {
      console.log(event.target);
      console.log(event.currentTarget);
    }

    return (
      <button onClick={handleClick}>
        <span>Click me</span>
      </button>
    );

---

## If user clicks on span

- event.target → <span>  
- event.currentTarget → <button>  

---

## Rule

- target = where the event originated  
- currentTarget = where the handler is attached  

---

# Step 8 — Important Gotcha (Older React Versions)

Older versions of React used **event pooling**.

This meant event objects were reused.

---

## Problem example

    setTimeout(() => {
      console.log(event.target); // null in older React
    }, 1000);

---

## Modern React (v17+)

- Event pooling is removed  
- This issue no longer occurs  

---

## Best practice (still recommended)

Always extract values early:

    const value = event.target.value;

---

# Step 9 — Mental Model

Think of the flow like this:

- Browser fires an event  
- React intercepts it  
- React wraps it into a SyntheticEvent  
- Your handler receives it and reacts  

---

## Important idea

You are not directly interacting with the browser event system.

React sits in between.
