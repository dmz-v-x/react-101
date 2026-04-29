# useState Hook — Part 2

---

# 0. Quick Recap (From Part 1)

You already understand:

- useState stores data
- It triggers re-render
- It returns [value, setter]
- Updates are async
- Functional updates fix stale issues

Now we go deeper into **how React actually behaves** and the **tricky parts most beginners miss**.

---

# 1. Batching (Very Important Concept)

---

## What is batching?

React **groups multiple state updates together** into one re-render.

---

## Example

	function App() {
	  const [count, setCount] = useState(0);

	  function handleClick() {
	    setCount(count + 1);
	    setCount(count + 1);
	  }

	  return <button onClick={handleClick}>{count}</button>;
	}

---

## What you expect

0 → 2

---

## What actually happens

0 → 1

---

## Why?

Because React batches updates:

	setCount(count + 1)
	setCount(count + 1)

Both use SAME old value

---

## Solution (Functional Update)

	setCount(prev => prev + 1);
	setCount(prev => prev + 1);

---

## Now result

0 → 2

---

# 2. Stale Closure Problem

---

## What is a closure?

A closure "remembers" values from when function was created.

---

## Problem Example

	function App() {
	  const [count, setCount] = useState(0);

	  function delayedIncrement() {
	    setTimeout(() => {
	      setCount(count + 1);
	    }, 1000);
	  }

	  return <button onClick={delayedIncrement}>{count}</button>;
	}

---

## Problem

Click multiple times → only increments once

---

## Why?

- `count` is captured (stale)
- Old value used inside setTimeout

---

## Solution

	setCount(prev => prev + 1);

---

## Rule

👉 If update depends on previous value → ALWAYS use functional update

---

# 3. State is Snapshot-Based (Very Important)

---

React gives you a **snapshot of state per render**

---

## Example

	function App() {
	  const [count, setCount] = useState(0);

	  console.log("Render:", count);

	  return (
	    <button onClick={() => setCount(count + 1)}>
	      {count}
	    </button>
	  );
	}

---

## Key Idea

Each render has its own version of `count`

---

# 4. Re-rendering Explained Clearly

---

When state changes:

1. React schedules update
2. Component function runs again
3. New UI is created
4. DOM is updated

---

## Important

React does NOT "update variable"

👉 It re-runs component

---

# 5. State is NOT persisted like variables

---

Each render:

	function App() {
	  const [count, setCount] = useState(0);
	}

👉 count is NEW variable each render

---

## But React remembers value internally

---

# 6. Derived State (Important Pattern)

---

## Problem

Don't store values that can be calculated

---

## Bad

	const [fullName, setFullName] = useState("");

---

## Good

	const fullName = firstName + lastName;

---

## Rule

👉 If it can be derived → don't store it

---

# 7. Updating Objects (Common Bug)

---

## Wrong

	user.name = "John";
	setUser(user);

---

## Why wrong?

Same reference → React may NOT re-render

---

## Correct

	setUser({ ...user, name: "John" });

---

# 8. Updating Nested State

---

## Example

	const [user, setUser] = useState({
	  profile: {
	    name: "Sam"
	  }
	});

---

## Update

	setUser({
	  ...user,
	  profile: {
	    ...user.profile,
	    name: "John"
	  }
	});

---

# 9. State Splitting vs Single Object

---

## Option 1 (Multiple states)

	const [name, setName] = useState("");
	const [age, setAge] = useState(0);

---

## Option 2 (Single object)

	const [user, setUser] = useState({ name: "", age: 0 });

---

## Rule

- Simple → separate state
- Related → object state

---

# 10. Resetting State

---

## Method 1

	setState(initialValue)

---

## Method 2 (Force reset using key)

	const [key, setKey] = useState(0);

	<Component key={key} />

	setKey(prev => prev + 1);

---

## Why works?

Changing key → React recreates component

---

# 11. Performance Considerations

---

## Myth

"useState is slow"

---

## Reality

- useState is very fast
- React optimizes rendering

---

## Real problem

Unnecessary re-renders

---

## Solution

- useMemo
- useCallback
- React.memo

(Advanced topics)

---

# 12. When NOT to use useState

---

❌ Derived values  
❌ Constants  
❌ Values that never change  

---

# 13. Common Gotchas

---

## 1. State updates async

	setCount(count + 1);
	console.log(count); // old value

---

## 2. Multiple updates overwritten

Fix → functional update

---

## 3. Mutating state

Never do this

---

## 4. Stale closure

Fix → functional update

---

## 5. Infinite re-render

---

### Example

	function App() {
	  const [count, setCount] = useState(0);

	  setCount(1); // ❌ infinite loop

	  return <div>{count}</div>;
	}

---

## Why?

State update → re-render → update again → infinite loop

---

# 14. Best Practices

---

✔ Use functional updates when needed  
✔ Keep state minimal  
✔ Avoid duplication  
✔ Keep state flat  
✔ Never mutate  
✔ Use descriptive names  

---

# 15. Real-World Pattern Example

---

	function Counter() {
	  const [count, setCount] = useState(0);

	  function increment() {
	    setCount(prev => prev + 1);
	  }

	  function decrement() {
	    setCount(prev => prev - 1);
	  }

	  return (
	    <>
	      <button onClick={decrement}>-</button>
	      <span>{count}</span>
	      <button onClick={increment}>+</button>
	    </>
	  );
	}

---

# 16. Final Mental Model (MOST IMPORTANT)

---

Think of useState like:

👉 A memory slot React manages  
👉 You request updates via setter  
👉 React re-renders with new snapshot  

---

# 17. Ultra Simple Analogy

---

Imagine:

- React = chef
- useState = ingredient box

You:

- ask chef to update ingredient
- chef re-cooks dish (re-render)

---

# 18. Final Summary

---

✔ useState stores state  
✔ State is snapshot-based  
✔ Updates are async  
✔ Functional updates avoid bugs  
✔ Never mutate state  
✔ Re-render happens automatically  
✔ React manages state internally  

---

# FINAL ONE-LINE UNDERSTANDING

useState is React’s mechanism for storing and updating dynamic data across renders, where each update triggers a re-render and the component receives a fresh snapshot of the updated state.
