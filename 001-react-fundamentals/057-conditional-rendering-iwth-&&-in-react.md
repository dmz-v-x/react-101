# Conditional Rendering with `&&` in React

---

# 1. Question

Understand:

- How to use `&&` for conditional rendering  
- Why `if` cannot be used inside JSX  
- How `&&` actually works in JavaScript  
- The common bug with `0`  
- How to fix that bug  

---

# 2. Intuition (Core Idea)

Sometimes you want to:

- Show something only if a condition is true  
- Otherwise show nothing  

---

## Example

Show online indicator only if user is online.

---

## React solution

Use logical AND (`&&`).

---

## Mental Model

Condition is true → show UI  
Condition is false → show nothing  

---

# 3. Why `if` Cannot Be Used Inside JSX

---

## Wrong

	{if (isOnline) { <Dot /> }}

---

## Reason

- `if` is a **statement**  
- JSX `{}` only allows **expressions**  

---

## Rule

JSX expects a value, not logic statements.

---

# 4. Using `&&` for Conditional Rendering

---

## Correct

	{isOnline && <div className="green-dot" />}

---

## How it works

JavaScript rule:

	A && B

returns:

- `B` if `A` is truthy  
- `A` if `A` is falsy  

---

## So:

- `true && <Dot />` → `<Dot />`  
- `false && <Dot />` → `false`  

---

## React behavior

React ignores:

- false  
- null  
- undefined  

---

## Result

- true → renders element  
- false → renders nothing  

---

# 5. Example

	function Friend({ name, isOnline }) {
	  return (
	    <li className="friend">
	      {isOnline && <div className="green-dot" />}
	      {name}
	    </li>
	  );
	}

---

## What happens

- Online → green dot shown  
- Offline → nothing shown  

---

# 6. How `&&` Maps to `if`

---

## Equivalent logic

	if (isOnline) {
	  return <Dot />;
	} else {
	  return false;
	}

---

## Why it works

React ignores `false`.

---

# 7. The Most Common Gotcha — `0`

---

## Example

	{numOfItems && <ShoppingList />}

---

## If

	numOfItems = 0

---

## Result

- `0 && <ShoppingList />` → returns `0`  
- React renders `0`  

---

## Output

	0

---

## Why?

React does NOT ignore:

- numbers  
- NaN  

---

# 8. Values React Ignores vs Renders

---

| Value               | Ignored by React |
|---------------------|------------------|
| false               | Yes              |
| null                | Yes              |
| undefined           | Yes              |
| "" (empty string)   | Yes              |
| 0                   | No               |
| NaN                 | No               |

---

# 9. Fixing the `0` Problem

---

## Solution 1 — Use boolean condition

	{numOfItems > 0 && <ShoppingList />}

---

## Why it works

- `numOfItems > 0` → always true/false  

---

## Solution 2 — Convert to boolean

	{!!numOfItems && <ShoppingList />}

---

## How `!!` works

- `0` → false  
- non-zero → true  

---

# 10. When to Use `&&`

---

Use `&&` when:

- You want to show something conditionally  
- No "else" case is needed  

---

## Example

	{isAdmin && <AdminPanel />}

---

# 11. When NOT to Use `&&`

---

## Avoid when:

- Left side is not boolean  
- You need "else" case  

---

## Instead use ternary

	{isLoggedIn 
	  ? <Dashboard /> 
	  : <Login />
	}

---

# 12. Approach (How to Think)

---

## Step 1

Do you only need to show something when true?

---

## Step 2

Use `&&`

---

## Step 3

Ensure left side is boolean  

---

## Step 4

Avoid numbers directly  

---

# 13. Final Summary

---

- `&&` is used for conditional rendering  
- Works because of JavaScript short-circuiting  
- React ignores false/null/undefined  
- But NOT `0` or `NaN`  
- Always use boolean conditions  

---

# 14. Final Mental Model

Condition && UI → render UI only if condition is true

---

# One-Line Understanding

> In React, the `&&` operator is used to render something only when a condition is true, but the condition must be a boolean to avoid unintended outputs like `0`.
