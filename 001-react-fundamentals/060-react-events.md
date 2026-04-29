# React Events

---

# 1. Question

Understand:

- What React events are  
- How event handling works in React  
- Why React uses camelCase for events  
- How to correctly write event handlers  
- How to pass arguments and use event objects  

---

# 2. Intuition (Core Idea)

Web apps are interactive.

Users can:

- Click buttons  
- Type in inputs  
- Submit forms  
- Hover elements  

---

## React needs a way to respond to these actions.

This is done using **events**.

---

## Mental Model

User action → Event → Function runs → UI updates  

---

# 3. Basic Example

	<button onClick={handleClick}>Click me</button>

---

## What happens

- User clicks button  
- `handleClick` function runs  

---

# 4. Event Names in React

---

## HTML

	<button onclick="...">

---

## React

	<button onClick={...}>

---

## Rule

React uses **camelCase**.

---

## Common mappings

| HTML        | React       |
|-------------|------------|
| onclick     | onClick     |
| onchange    | onChange    |
| onsubmit    | onSubmit    |
| onmouseover | onMouseOver |

---

# 5. Event Handlers Must Be Functions

---

## Wrong (HTML style)

	<button onClick="alert('hi')">Click</button>

---

## Correct

	<button onClick={() => alert('hi')}>Click</button>

---

## Better

	function handleClick() {
	  alert('hi');
	}

	<button onClick={handleClick}>Click</button>

---

## Rule

Always pass a function, not a string.

---

# 6. Passing Function Reference vs Calling It

---

## Wrong

	<button onClick={handleClick()}>Click</button>

---

## Problem

- Function runs immediately  
- Not when user clicks  

---

## Correct

	<button onClick={handleClick}>Click</button>

---

## Rule

Do NOT call the function. Just pass it.

---

# 7. Passing Arguments to Handlers

---

## Problem

	<button onClick={handleClick(5)}>Increment</button>

---

## Why wrong

- Function executes immediately  

---

## Correct

	<button onClick={() => handleClick(5)}>Increment</button>

---

## Why it works

- Arrow function delays execution  
- Runs only on click  

---

# 8. The Event Object (SyntheticEvent)

---

## Example

	function handleInput(e) {
	  console.log(e.target.value);
	}

	<input onChange={handleInput} />

---

## What is `e`?

- Event object  
- Contains information about event  

---

## Example data

- `e.target.value` → input value  
- `e.type` → event type  

---

## Important

React uses **SyntheticEvent**

- Wrapper around native event  
- Works consistently across browsers  

---

# 9. Common Events in React

---

| Event       | Description            |
|-------------|------------------------|
| onClick     | clicking               |
| onChange    | typing in inputs       |
| onSubmit    | form submission        |
| onMouseOver | hover                  |
| onFocus     | element focused        |
| onBlur      | focus lost             |
| onKeyDown   | key pressed            |
| onScroll    | scrolling              |

---

# 10. Preventing Default Behavior

---

## Problem

Forms reload the page on submit.

---

## Solution

	function handleSubmit(e) {
	  e.preventDefault();
	  console.log("submitted!");
	}

	<form onSubmit={handleSubmit}>
	  <button>Submit</button>
	</form>

---

## What happens

- Stops page refresh  
- Runs custom logic  

---

# 11. Full Example

---

	function App() {
	  function handleClick() {
	    alert("Button clicked!");
	  }

	  function handleChange(e) {
	    console.log("Typed:", e.target.value);
	  }

	  return (
	    <>
	      <button onClick={handleClick}>Click me</button>
	      <input onChange={handleChange} placeholder="Type here" />
	    </>
	  );
	}

---

# 12. Approach (How to Think)

---

## Step 1

What user action do you want to handle?

---

## Step 2

Pick correct event:

- click → onClick  
- typing → onChange  
- submit → onSubmit  

---

## Step 3

Write handler function  

---

## Step 4

Pass function reference  

---

# 13. Final Summary

---

- React uses camelCase event names  
- Event handlers must be functions  
- Do not call functions directly in JSX  
- Use arrow functions to pass arguments  
- React provides SyntheticEvent  
- Use `preventDefault()` when needed  

---

# 14. Final Mental Model

User action → Event → Handler → State/UI update  

---

# One-Line Understanding

> React events let you respond to user interactions by attaching functions to JSX elements, using camelCase syntax and JavaScript functions instead of HTML strings.
