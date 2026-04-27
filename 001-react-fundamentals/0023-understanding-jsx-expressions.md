# Understanding JSX Expressions

---

## Example

Let’s look at this example:

	const shoppingList = ['apple', 'banana', 'carrot'];

	const element = (
	  <div>
	    Items left to purchase: {shoppingList.length}
	  </div>
	);

---

## What’s happening here?

- `{shoppingList.length}` is JavaScript inside JSX  
- React evaluates `shoppingList.length` → `3`  
- That value is inserted into the UI  

So the final rendered output becomes:

	Items left to purchase: 3

---

## What JSX becomes after compiling

	const compiledElement = React.createElement(
	  'div',
	  {},
	  'Items left to purchase: ',
	  shoppingList.length
	);

---

### Key idea

- Both versions do the same thing  
- JSX is just **syntactic sugar** over `React.createElement`  
- JSX improves readability and developer experience  

---

# Comments in JSX

---

## Correct way to write comments

To add a comment inside JSX, you must use:

- Curly braces `{}`  
- JavaScript multi-line comment `/* */`  

### Example

	<div>
	  {/* This is a comment */}
	</div>

---

## What does NOT work

	<div>
	  // This breaks JSX!
	</div>

---

### Why this fails

- `//` comments out the rest of the line  
- It can break JSX parsing (especially around closing braces `}`)  
- JSX expects valid JavaScript expressions inside `{}`  

---

# Dynamic Attributes in JSX

---

## Using `{}` inside attributes

You can inject JavaScript into attributes using `{}`.

### Example

	const uniqueId = 'content-wrapper';

	const element = (
	  <main id={uniqueId}>
	    Hello World
	  </main>
	);

---

## What it compiles to

	React.createElement(
	  'main',
	  { id: uniqueId },
	  "Hello World"
	);

---

## Static version (no interpolation)

	<main id="content-wrapper">
	  Hello World
	</main>

---

### When to use which?

- Use **static values** if they never change  
- Use `{}` when the value is dynamic  

---

# Attribute expressions can contain ANY JavaScript

Not just variables — you can use full expressions.

---

## Example

	const userEmail = "sumeet@thegreat.com";

	const element = (
	  <main id={userEmail.replace('@', '-')}>
	    Hello World
	  </main>
	);

---

## Compiled version

	React.createElement(
	  'main',
	  { id: userEmail.replace('@', '-') },
	  "Hello World"
	);

---

## Important concept

- React does **not execute** this code during compilation  
- It only converts JSX → JavaScript  

---

### Two phases

**Compile-time**
- JSX → JavaScript  

**Run-time**
- JavaScript actually executes in the browser  

---

# Type Coercion in JSX

---

## Key idea

React automatically converts values into strings when needed.

---

## Example: Boolean values

	<input required="true" />   // string "true"
	<input required={true} />   // boolean true → converted to string

Both behave the same in HTML.

---

## Example: Numbers

	<input type="range" min="1" max="20" />   // strings
	<input type="range" min={1} max={20} />   // numbers

Both are valid.

---

## Why this works

- HTML attributes are typically strings  
- React handles conversion automatically  

---

# Boolean Attributes

---

## HTML style

In plain HTML:

	<input required>

This means:

	required = true

---

## JSX allows the same

	<input required />

---

## Equivalent explicit version

	<input required={true} />

---

## Recommended approach

Use the explicit version:

	<input required={true} />

---

## Why this is recommended

In JavaScript:

	const name = 'Spot';
	const dog = { name };

	console.log(dog); // { name: 'Spot' }

---

### What this means

- `{ name }` becomes `{ name: name }`  
- NOT `{ name: true }`  

---

## Key takeaway

- HTML shorthand and JavaScript object shorthand behave differently  
- This can confuse beginners  
- Writing `required={true}` is clearer and more predictable  

---

# Final Summary (Mental Model)

- `{}` lets you run JavaScript inside JSX  
- JSX expressions are evaluated and rendered into the UI  
- JSX compiles into `React.createElement`  
- Comments inside JSX must use `{/* */}`  
- Attributes can use dynamic expressions  
- React automatically handles type conversion  
- Boolean attributes should be written explicitly for clarity  

---

## One-Line Understanding

> JSX expressions allow you to embed and evaluate JavaScript inside UI code, which React converts into plain JavaScript before rendering.
