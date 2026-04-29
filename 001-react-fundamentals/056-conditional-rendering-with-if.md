# Conditional Rendering with `if` in React

---

# 1. Question

Understand:

- Why `if` cannot be used directly inside JSX  
- What JSX allows inside `{}`  
- How to correctly use `if` for conditional rendering  
- Why `undefined` works safely in JSX  

---

# 2. Intuition (Core Idea)

In React:

- You can write JavaScript inside JSX using `{}`  

BUT:

- Only **expressions** are allowed  
- NOT **statements**

---

## What is the difference?

- Expression → produces a value  
- Statement → performs an action  

---

## Examples

Expressions:

	2 + 2
	name
	isLoggedIn && <p>Hello</p>

Statements:

	if (...) { ... }
	for (...) { ... }

---

## Mental Model

JSX `{}` = "give me a value to render"

---

# 3. Why `if` Does NOT Work Inside JSX

---

## Wrong Code

	<li>
	  {if (isOnline) {
	     <div className="green-dot" />
	  }}
	  {name}
	</li>

---

## Why it fails

- `if` is a statement  
- It does NOT return a value  
- JSX expects a value  

---

## Equivalent JavaScript (invalid)

	console.log(
	  if (loggedIn) { "Yes" }
	)

---

## JSX Compilation (simplified)

	React.createElement(
	  "li",
	  null,
	  if (isOnline) {
	    React.createElement("div")
	  },
	  name
	)

---

This is invalid JavaScript.

---

# 4. Correct Approach — Move `if` Outside JSX

---

## Idea

Prepare the value BEFORE JSX.

---

## Code

	function Friend({ name, isOnline }) {
	  let prefix;

	  if (isOnline) {
	    prefix = <div className="green-dot" />;
	  }

	  return (
	    <li className="friend">
	      {prefix}
	      {name}
	    </li>
	  );
	}

---

## What’s happening

- If online → `prefix` contains JSX  
- If offline → `prefix` is `undefined`  

---

# 5. Why This Works

---

## JSX Rendering Rules

React ignores:

- `undefined`  
- `null`  
- `false`  

---

## So:

- If `prefix` exists → render it  
- If `prefix` is undefined → ignore it  

---

## Internally

	if (isOnline) {
	  prefix = React.createElement("div");
	}

	return React.createElement(
	  "li",
	  null,
	  prefix,
	  name
	);

---

## Key Insight

Everything becomes valid JavaScript.

---

# 6. Bonus — Undefined Attributes

---

## Example

	function Greeting() {
	  let someClass;

	  return <div className={someClass}>Hello</div>;
	}

---

## What happens

- `someClass` is `undefined`  
- React removes the attribute  

---

## Final Output

	<div>Hello</div>

---

## Not

	<div class=""></div>

---

# 7. Rules for `{}` in JSX

---

## Allowed

- Variables  
- Expressions  
- Function calls  
- Ternary operators  
- Logical AND (`&&`)  

---

## Not Allowed

- `if` statements  
- `for` loops  
- `while` loops  

---

# 8. Approach (How to Think)

---

## Step 1

Do you need complex logic?

---

## Step 2

Use `if` outside JSX  

---

## Step 3

Store result in a variable  

---

## Step 4

Render variable inside `{}`  

---

# 9. Final Summary

---

| Type                         | Allowed in JSX `{}` |
|------------------------------|--------------------|
| Expressions                  | Yes                |
| Variables                    | Yes                |
| Function calls               | Yes                |
| Ternary (`?:`)               | Yes                |
| Logical AND (`&&`)           | Yes                |
| `if` statements              | No                 |
| `for` loops                  | No                 |

---

# 10. Final Mental Model

JSX `{}` = value only  
Statements must be handled before rendering  

---

# One-Line Understanding

> In React, `if` statements cannot be used inside JSX because JSX only accepts expressions, so conditions must be handled outside JSX and their results rendered inside `{}`.
