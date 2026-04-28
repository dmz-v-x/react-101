# React Components — Basic Syntax (Simple Explanation)

---

## What is a Component?

React apps are built using **components**.

A component is simply:

- A JavaScript function  
- That returns JSX (UI)

---

## Example Component

	function FriendlyGreeting() {
	  return (
	    <p
	      style={{
	        fontSize: '1.25rem',
	        textAlign: 'center',
	        color: 'sienna',
	      }}
	    >
	      Greetings, weary traveller!
	    </p>
	  );
	}

---

## What the Component Does

- It is a function  
- It returns UI (JSX)  
- React uses that JSX to render content on the page  

---

## Rendering a Component

	root.render(<FriendlyGreeting />);

---

### What this means

- `<FriendlyGreeting />` looks like an HTML tag  
- But it represents your custom component  

It tells React:

> “Create and display this component.”

---

## Components Can Be Written Two Ways

---

### 1. Traditional Function

	function FriendlyGreeting() {
	  return <p>Hello!</p>;
	}

---

### 2. Arrow Function

	const FriendlyGreeting = () => (
	  <p>Hello!</p>
	);

---

### Which is better?

- Both work the same  
- It’s a matter of personal preference  

---

## The Most Important Rule

Component names **must start with a capital letter**.

---

### Correct

	FriendlyGreeting  
	UserCard  
	AppHeader  

---

### Wrong

	friendlyGreeting  
	greeting  

---

### Why?

React uses naming to distinguish between:

- HTML elements  
- Custom components  

---

## How React Knows the Difference

---

### HTML example

	<h1>Hello</h1>

Becomes:

	React.createElement("h1", null, "Hello");

---

### Component example

	<FriendlyGreeting />

Becomes:

	React.createElement(FriendlyGreeting, null);

---

### Key difference

- HTML tags → passed as strings (`"h1"`)  
- Components → passed as functions (`FriendlyGreeting`)  

---

## Why React Uses Capital Letters

At first glance, React could try to guess what is HTML and what is a component.

But that creates ambiguity.

---

### Example

	<button />

---

### Question

Is this:

- The built-in HTML `<button>` tag?  
- Or a custom component named `button`?  

---

### Problem

- Some libraries define components like `button`  
- HTML keeps adding new tags over time  
- React cannot reliably guess  

---

## Solution: Capitalization Rule

- Lowercase → built-in HTML elements  
- Uppercase → custom React components  

---

### This rule is:

- Simple  
- Consistent  
- 100% reliable  

---

## Final Mental Model

- A component = a function that returns JSX  
- JSX describes what UI should look like  
- React converts components into DOM elements  
- Capital letters tell React “this is a component”  

---

## One-Line Understanding

> A React component is a JavaScript function that returns JSX, and must start with a capital letter so React knows it’s a custom UI element.
