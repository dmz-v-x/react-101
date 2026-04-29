# React Event Handlers — Passing Arguments (Complete Deep Dive)

---

# 0. What This Topic Is About

This concept explains:

- How React handles event functions (like `onClick`)
- The difference between **passing a function** vs **calling a function**
- Why we need wrapper functions
- How to pass arguments to event handlers
- Performance concerns (and why they are mostly myths)
- Alternative approaches like `.bind()`

---

# 1. Core Mental Model (Very Important)

React events work like this:

👉 You GIVE React a function  
👉 React CALLS it later when the event happens  

---

## Example

	function handleClick() {
	  console.log("Clicked!");
	}

	<button onClick={handleClick}>Click</button>

---

## What happens internally

- React stores `handleClick`
- When user clicks → React calls it

---

# 2. Function Reference vs Function Call

This is the most important concept.

---

## Function Reference

	handleClick

Means:

👉 "Here is the function, run it later"

---

## Function Call

	handleClick()

Means:

👉 "Run it RIGHT NOW"

---

## Example

	function sayHi() {
	  console.log("Hi");
	}

	sayHi        // reference
	sayHi()      // executes immediately

---

# 3. What React EXPECTS

React expects:

👉 A function reference

---

## Correct

	<button onClick={sayHi}>Click</button>

---

## Wrong

	<button onClick={sayHi()}>Click</button>

---

## Why wrong?

Because:

- `sayHi()` runs during render
- React receives the RETURN VALUE (not the function)

---

# 4. The Real Problem — Passing Arguments

---

## Scenario

We have:

	function setTheme(theme) {
	  console.log("Theme:", theme);
	}

---

## We want:

	setTheme("dark")

BUT only when button is clicked.

---

# 5. First Attempt (Fails)

---

## Code

	<button onClick={setTheme}>
	  Toggle
	</button>

---

## Problem

- No argument passed
- React calls: `setTheme()`
- `theme` becomes `undefined`

---

# 6. Second Attempt (Also Wrong)

---

## Code

	<button onClick={setTheme("dark")}>
	  Toggle
	</button>

---

## What happens

- `setTheme("dark")` runs immediately
- During render (NOT click)

---

## Result

- Theme changes instantly
- Nothing happens on click

---

# 7. The Correct Solution — Wrapper Function

---

## Code

	<button onClick={() => setTheme("dark")}>
	  Toggle
	</button>

---

## What we are doing

We are:

👉 Creating a NEW function  
👉 Passing THAT function to React  

---

## Important

	() => setTheme("dark")

is NOT executed immediately.

It means:

👉 “When clicked → run setTheme('dark')”

---

# 8. Step-by-Step Execution Flow

---

## During render

React sees:

	onClick = function() {
	  setTheme("dark")
	}

It stores this function.

---

## When user clicks

React executes:

	setTheme("dark")

---

# 9. Why This Works

Because:

- We pass a function reference
- That function contains the logic we want

---

# 10. Real-World Use Cases

---

## 1. Passing IDs

	<button onClick={() => deleteUser(user.id)}>
	  Delete
	</button>

---

## 2. Updating state

	<button onClick={() => setCount(count + 1)}>
	  Increment
	</button>

---

## 3. API calls

	<button onClick={() => fetchData("users")}>
	  Load Users
	</button>

---

## 4. Conditional logic

	<button onClick={() => {
	  if (isAdmin) {
	    deleteAll();
	  }
	}}>
	  Delete All
	</button>

---

# 11. Why Not Just Call the Function?

Because React needs:

👉 A function to call later  
👉 Not something that runs immediately  

---

# 12. Alternative Solution — .bind()

---

## Code

	<button onClick={setTheme.bind(null, "dark")}>
	  Toggle
	</button>

---

## What .bind does

It creates a new function:

	function() {
	  setTheme("dark");
	}

---

## Why it's less used

- Less readable
- Less common in React community
- No real advantage over arrow functions

---

# 13. Performance Myth (Very Important)

---

## Myth

“Creating functions inside JSX is bad for performance”

---

## Reality

- Creating functions is VERY cheap
- Modern JS engines are extremely fast
- React optimizes event handling internally

---

## Fact

Even low-end devices can create:

👉 Hundreds of thousands of functions per second

---

## Conclusion

👉 You DO NOT need to worry about this

---

# 14. When Performance Actually Matters

---

Only in advanced scenarios:

- Large lists (thousands of items)
- Deep component trees
- Frequent re-renders

---

## Solution (Advanced)

	useCallback()

(Not needed for beginners)

---

# 15. Common Mistakes

---

## ❌ Mistake 1

	<button onClick={handleClick()}>

Runs immediately

---

## ❌ Mistake 2

Forgetting wrapper when passing arguments

	<button onClick={setTheme("dark")}>

---

## ❌ Mistake 3

Thinking arrow function runs immediately

It does NOT.

---

# 16. Mental Model (Very Important)

---

Think like this:

❌ WRONG thinking:

“onClick = run this code”

---

✔ CORRECT thinking:

“onClick = give React a function to run later”

---

# 17. Simple Analogy

---

Imagine:

You give a remote control to someone.

- Passing function → giving remote  
- Calling function → pressing button immediately  

---

# 18. Final Summary

---

✔ React events need function references  
✔ Functions should NOT be called during render  
✔ Use arrow functions to pass arguments  
✔ Wrapper functions delay execution  
✔ `.bind()` is an alternative but less common  
✔ Performance concerns are mostly myths  

---

# Final One-Line Understanding

In React, event handlers must be passed as function references, and when you need to pass arguments, you wrap the function inside another function so React can call it later instead of executing it immediately.
