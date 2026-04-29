# useState Hook — Part 1

---

# 0. What is useState?

Before even talking about `useState`, we need to understand:

👉 What problem it solves

---

# 1. The Core Problem (Why useState exists)

In React:

👉 UI is created using functions

Example:

	function App() {
	  return <h1>Hello</h1>;
	}

---

## Problem

Functions:

- run once
- forget everything after execution

---

### Example

	function App() {
	  let count = 0;

	  function increment() {
	    count++;
	    console.log(count);
	  }

	  return <button onClick={increment}>Click</button>;
	}

---

## What happens?

- Click → count becomes 1
- UI DOES NOT update

Why?

👉 React does not track `count`

---

# 2. Key Idea: React Needs Memory

We need:

👉 A way to **store values across renders**

👉 AND trigger re-render when value changes

---

# 3. Enter useState

---

## Definition

`useState` is a React Hook that lets you:

👉 Store data (state)  
👉 Update it  
👉 Re-render UI automatically  

---

# 4. Basic Syntax

---

	const [state, setState] = React.useState(initialValue);

---

## Example

	const [count, setCount] = React.useState(0);

---

## What is returned?

useState returns an array:

	[count, setCount]

---

## Equivalent (without destructuring)

	const arr = React.useState(0);

	const count = arr[0];
	const setCount = arr[1];

---

# 5. Meaning of Each Part

---

## count

👉 Current value

---

## setCount

👉 Function to update value

---

# 6. First Example (Counter)

---

	function Counter() {
	  const [count, setCount] = React.useState(0);

	  return (
	    <button onClick={() => setCount(count + 1)}>
	      Count: {count}
	    </button>
	  );
	}

---

## Flow

Click → setCount → React updates state → re-render → UI updates

---

# 7. Important Mental Model

---

## React does NOT update variable

Instead:

👉 It schedules a re-render  
👉 New state value is used  

---

# 8. Initial Value

---

	const [count, setCount] = React.useState(0);

👉 Initial value = 0  

---

## Runs only once

On first render only

---

# 9. Lazy Initialization (Advanced but Important)

---

## Normal

	const [count] = React.useState(expensiveFunction());

👉 Runs EVERY render

---

## Lazy

	const [count] = React.useState(() => expensiveFunction());

👉 Runs ONLY once

---

## Why?

React calls function ONLY on first render :contentReference[oaicite:0]{index=0}

---

# 10. Why Lazy Initialization Matters

---

## Example

	const [data] = React.useState(() => {
	  return window.localStorage.getItem("key");
	});

---

## Benefit

- Avoid expensive recalculation
- Better performance

---

# 11. Naming Convention

---

	const [user, setUser] = useState();
	const [count, setCount] = useState();

---

## Rule

	state → variable  
	setState → updater  

---

# 12. How setState Works

---

## Example

	setCount(5);

---

## What happens

- React schedules update
- Re-renders component
- New value = 5

---

# 13. Important Rule (Very Important)

---

## State updates are asynchronous

---

## Example

	setCount(count + 1);
	console.log(count);

---

## Output

Old value

---

## Why?

React batches updates

---

# 14. Functional Updates (Very Important)

---

## Problem

	setCount(count + 1);
	setCount(count + 1);

👉 Only increments once

---

## Solution

	setCount(prev => prev + 1);
	setCount(prev => prev + 1);

👉 Correctly increments twice

---

## Why?

Uses latest value

---

# 15. State Triggers Re-render

---

## Example

	const [name, setName] = useState("Sam");

	setName("John");

---

## React does

1. Save new state
2. Re-run component
3. Update UI

---

# 16. What Causes Re-render?

---

✔ State change  
✔ Props change  

---

# 17. What Does NOT Cause Re-render?

---

❌ Normal variables  
❌ console.log  
❌ functions  

---

# 18. Multiple State Variables

---

	const [name, setName] = useState("");
	const [age, setAge] = useState(0);

---

## React tracks them separately

---

# 19. State with Objects

---

	const [user, setUser] = useState({
	  name: "Sam",
	  age: 20
	});

---

## Update

	setUser({
	  ...user,
	  name: "John"
	});

---

## Important

👉 Never mutate state

---

# 20. Why Not Mutate?

---

❌ Wrong

	user.name = "John";

---

✔ Correct

	setUser({ ...user, name: "John" });

---

## Reason

React needs new reference

---

# 21. State with Arrays

---

	const [items, setItems] = useState([]);

---

## Add item

	setItems([...items, newItem]);

---

## Remove item

	setItems(items.filter(item => item.id !== id));

---

# 22. Key Gotchas (Important)

---

## 1. State is not immediate

	setState → async

---

## 2. Never mutate state

---

## 3. Always use setter

---

## 4. Don't rely on old state

Use functional update

---

# 23. Rules of Hooks

---

## Rule 1

Call hooks at top level

---

## Rule 2

Don't call inside loops or conditions

---

## Rule 3

Call only inside React functions

---

# 24. Why useState is Called Hook

---

Hook = special function to "hook into React internals" :contentReference[oaicite:1]{index=1}

---

# 25. Internal Idea (Simplified)

---

React keeps:

	state per component

---

Each render:

- React remembers previous state
- Applies updates

---

# 26. Summary (Part 1)

---

✔ useState stores data  
✔ Triggers re-render  
✔ Returns [value, setter]  
✔ Initial value runs once  
✔ Lazy initialization for performance  
✔ Functional updates avoid bugs  
✔ Never mutate state  
