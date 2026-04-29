# Conditional Rendering in React

---

# 1. Question

Understand:

- How to show or hide UI based on conditions  
- Why React does not have special syntax for conditionals  
- How to use `if`, `&&`, and `?:` in React  
- When to use each method  

---

# 2. Intuition (Core Idea)

In real applications, UI is not static.

You often need to:

- Show something only if a user is logged in  
- Show a loader while data is loading  
- Show different UI depending on state  

---

## Key idea

React does NOT provide special syntax.

Instead:

- You use **normal JavaScript inside JSX**

---

## Mental Model

Condition → Decide → Render UI

---

# 3. Concept Used

- JavaScript conditionals  
- JSX expressions  
- Conditional rendering  

---

# 4. Method A — Using `if` (Outside JSX)

---

## When to use

- Large conditions  
- Multiple return paths  
- Cleaner logic  

---

## Example

	function Dashboard({ user }) {
	  if (!user) {
	    return <p>Please log in</p>;
	  }

	  return <p>Welcome back, {user.name}!</p>;
	}

---

## What happens

- If no user → return login message  
- If user exists → return welcome message  

---

## Important

- `if` cannot be used directly inside JSX  
- Must be used before `return`  

---

# 5. Method B — Using `&&` (Logical AND)

---

## When to use

- Show something only if condition is true  

---

## Example

	{isLoggedIn && <p>Welcome!</p>}

---

## How it works

- If `isLoggedIn = true` → JSX renders  
- If `false` → nothing is rendered  

---

## Important Gotcha

	{0 && <p>Hello</p>}

---

## Output

	0

---

## Why?

Because JavaScript evaluates:

- `0 && something` → returns `0`  

---

## Rule

Use `&&` only when:

- Condition is boolean  

---

# 6. Method C — Using Ternary Operator (`?:`)

---

## When to use

- Choose between two UI states  

---

## Example

	{isLoggedIn 
	  ? <p>Welcome back!</p> 
	  : <p>Please log in.</p>
	}

---

## How it works

- Condition true → first JSX  
- Condition false → second JSX  

---

## Benefit

- Very readable  
- Most commonly used  

---

# 7. Method D — Conditional Attributes

---

## Example

	<button disabled={!isReady}>
	  Submit
	</button>

---

## Meaning

- If not ready → button disabled  
- If ready → enabled  

---

## Key idea

You can use expressions inside attributes.

---

# 8. Combining Techniques

---

## Example

	function Greeting({ user }) {
	  return (
	    <div>
	      <h1>Hello!</h1>

	      {user 
	        ? <p>Welcome back, {user.name}</p> 
	        : <p>Please log in</p>
	      }

	      {user?.isAdmin && <p>You have admin access</p>}
	    </div>
	  );
	}

---

## What’s happening

- Ternary → main condition  
- Optional chaining → safe access  
- `&&` → additional condition  

---

# 9. Approach (How to Think)

---

## Step 1

What type of condition?

---

## Step 2

Choose method:

- Big logic → `if`  
- Show or hide → `&&`  
- Either/or → `?:`  

---

## Step 3

Write JSX accordingly  

---

# 10. Final Summary

---

| Task                        | Best Method        |
|-----------------------------|-------------------|
| Choose between two options  | Ternary `?:`      |
| Show something if true      | `&&`              |
| Complex conditions          | `if` before return|

---

# 11. Final Mental Model

Condition → JavaScript expression → JSX rendered

---

# One-Line Understanding

> In React, conditional rendering is done using normal JavaScript (`if`, `&&`, `?:`) inside JSX to dynamically control what UI gets displayed.
