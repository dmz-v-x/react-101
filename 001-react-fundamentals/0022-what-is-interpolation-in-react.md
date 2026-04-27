# What is Interpolation in React?

---

## Definition

Interpolation means putting JavaScript inside JSX using `{ ... }`.

### Example

	<h1>{userName}</h1>

Here, `{userName}` is interpolation.

Whatever you put inside `{ }` will be evaluated as JavaScript, and the result will be rendered to the UI.

---

## Syntax

	{ ... }

---

## Basic Rule

Inside `{ }`, you can write any **JavaScript expression**.

---

## What is an Expression?

An expression is something that **produces a value**.

### Examples of expressions

	2 + 3
	name
	isLoggedIn
	items.length
	price * discount
	condition ? A : B

---

## What you CANNOT put inside `{ }`

You **cannot** use JavaScript statements inside JSX interpolation.

### Not allowed (statements)

	if (...) { ... }
	for (...) { ... }
	while (...) { ... }
	let x = 10
	const y = 20

### Why?

Because these are **statements**, not expressions, and JSX only accepts expressions.

---

## What you CAN put inside `{ }`

Everything below is allowed:

- Variables  
- Math operations  
- String building  
- Ternary operator  
- Function calls  
- Array methods like `.map()`  
- Logical AND (`&&`)  
- Objects (with restrictions)  

---

# Interpolation Usage in JSX

---

## 1. Using variables inside interpolation

	const name = "Sam";

	return <h1>Hello {name}</h1>;

---

## 2. Using expressions (math, string, logic)

	const price = 10;
	const tax = 0.2;

	return <p>Total: {price + price * tax}</p>;

---

## 3. Using the ternary operator (conditional rendering)

	<p>{isLoggedIn ? "Welcome back!" : "Please log in"}</p>

This is extremely common in React.

---

## 4. Using logical AND (`&&`) for conditional display

Used when you only want to show something if a condition is true.

	{isAdmin && <button>Delete User</button>}

### Behavior

- If `isAdmin = true` → button shows  
- If `isAdmin = false` → nothing renders  

---

## 5. Using functions

	function upper(text) {
	  return text.toUpperCase();
	}

	<p>{upper("hello")}</p>

---

## 6. Using arrays with `.map()` (very common)

React **strongly prefers** `.map()` for rendering lists.

### Example

	const items = ["Apple", "Banana", "Cherry"];

	<ul>
	  {items.map(item => <li key={item}>{item}</li>)}
	</ul>

### Important concept

- `.map()` performs looping  
- But it returns an **array**  
- Arrays are valid expressions → so JSX allows it  

This is the **standard way to render lists in React**.

---

## 7. Using objects (important restriction)

You **cannot render objects directly**:

	<p>{ {name: "Sam"} }</p>   // Invalid

This will cause an error.

---

### Correct way (access properties)

	<p>{user.name}</p>         // ✔ Valid

---

## 8. Using interpolation in attributes (very important)

Interpolation is commonly used for dynamic attributes.

### Example: className

	<div className={isActive ? "active" : "inactive"}>

---

### Example: style (dynamic)

	<p style={{ color: theme === "dark" ? "white" : "black" }}>

---

## 9. Inline objects (React style object)

React uses JavaScript objects for inline styles:

	<div style={{ backgroundColor: "red", padding: "10px" }}>

---

## 10. Using fragments

You can return multiple elements without adding extra DOM nodes:

	<>
	  <h1>Title</h1>
	  <p>Paragraph</p>
	</>

Fragments help keep the DOM clean.

---

## Final Summary (Mental Model)

- `{}` = "run JavaScript here"  
- Only **expressions** are allowed inside `{}`  
- JSX evaluates the expression and renders the result  
- `.map()` is the standard way to render lists  
- Ternary (`? :`) and `&&` are commonly used for conditional rendering  
- Objects cannot be rendered directly, but their properties can  
- Interpolation is heavily used in attributes like `className` and `style`  

---

## One-Line Understanding

> Interpolation in React means embedding JavaScript expressions inside JSX using `{}`, and rendering their evaluated result to the UI.
