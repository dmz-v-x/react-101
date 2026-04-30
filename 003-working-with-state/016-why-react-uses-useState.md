# Why React Uses useState

---

# 0. What This Lesson Is Really About

This lesson answers a very important question:

👉 Why does React feel “complicated”?  
👉 Why can’t we just use normal variables like:

	let count = 0;

👉 Why do we need useState at all?

---

# 1. The Comparison (React vs Simpler Idea)

---

## React Way

```
const [count, setCount] = React.useState(0);

<button onClick={() => setCount(count + 1)} />
```

---

## “Simple” Way (What beginners expect)

```
let count = 0;

<button onClick={() => {
  count = count + 1;
}} />
```

---

## Looks better, right?

✔ Less code  
✔ Easier to read  

---

## But…

❌ It DOES NOT work  

---

# 2. The Core Problem

---

👉 JavaScript variables are NOT reactive  

---

## Meaning

If you change a variable:

	count = count + 1

---

👉 Nothing happens automatically  

---

React has NO idea something changed

---

# 3. Why React Needs useState

---

React needs 2 things:

---

## 1. Store value between renders  

## 2. Trigger re-render when value changes  

---

👉 Normal variables do neither  

---

# 4. Big Problem: Functions Reset Everything

---

## Example

```
function helloWorld() {
  let count = 0;
  count = count + 1;
}
```

---

Call it multiple times:

```
helloWorld();
helloWorld();
helloWorld();
```

---

## Each time:

	count = 0 → 1

---

👉 It NEVER remembers previous value  

---

# 5. Same Problem in React

---

## React component

```
function App() {
  let count = 0;
}
```

---

👉 Every render:

	count resets to 0  

---

## So:

❌ State is lost  

---

# 6. What React Actually Does

---

React solves this by:

👉 Storing state OUTSIDE your function  

---

## Important idea

Your component function is:

👉 Just a template  

---

Real data lives inside React

---

# 7. Conceptual Model (Very Important)

---

Instead of:

```
let count = 0;
```

---

React internally does something like:

```
count = getStoredValue()
```

---

And:

```
setCount(newValue)
```

---

Means:

👉 Save value  
👉 Trigger re-render  

---

# 8. What useState Actually Does

---

	useState gives you:

---

## 1. Current value

	count

---

## 2. Setter function

	setCount()

---

## That setter does TWO things:

---

### 1. Updates stored value  

### 2. Triggers re-render  

---

👉 This is the key  

---

# 9. Why Not Just Force Re-render?

---

You might think:

```
count = count + 1;
React.reRender();
```

---

## Why this fails

Because:

👉 On re-render → function runs again  

---

```
let count = 0;
```

---

👉 It resets again  

---

# 10. So What’s the Real Requirement?

---

We need:

---

✔ Persistent storage  
✔ Outside function  
✔ Survives re-renders  

---

👉 That is EXACTLY what useState provides  

---

# 11. Why Svelte Can Do It (Important Insight)

---

Svelte allows:

```
count = count + 1;
```

---

## Why?

👉 Svelte is NOT plain JavaScript :contentReference[oaicite:0]{index=0}  

---

It uses:

👉 A compiler  

---

That transforms code into:

👉 Complex reactive logic  

---

## So:

✔ Simple syntax  
❌ Hidden complexity  

---

# 12. React Philosophy vs Svelte

---

## React

✔ Explicit  
✔ You control updates  
✔ Less magic  
✔ More predictable  

---

## Svelte

✔ Simpler syntax  
✔ More magic  
✔ Compiler handles complexity  

---

# 13. Why React’s Way Is Actually Good

---

Even though it feels harder:

---

## Advantages

---

### 1. Predictability

You know exactly what triggers updates

---

### 2. Debugging is easier

No hidden behavior

---

### 3. Scales better

Large apps need explicit control

---

### 4. No hidden magic

Everything is visible

---

# 14. Real Insight (VERY IMPORTANT)

---

👉 React is NOT a reactive language  

👉 It is JavaScript + React engine  

---

So it MUST:

👉 Use functions like useState  

---

# 15. The “Dance” Explained

---

This “dance”:

```
const [count, setCount] = useState(0);
```

---

Exists because:

---

✔ Variables reset  
✔ React needs persistence  
✔ React needs re-render trigger  

---

👉 One API solves all problems  

---

# 16. Final Mental Model

---

Think of useState like:

---

👉 External memory storage  

---

Your component:

👉 Reads from it  

---

Setter:

👉 Writes to it + triggers re-render  

---

# 17. Real-Life Analogy

---

Imagine:

- Component = worker
- React = storage system

---

Worker:

👉 Reads data  
👉 Updates via system  

---

System:

👉 Saves data  
👉 Re-runs worker  

---

# 18. Final Summary

---

✔ Normal variables are NOT reactive  
✔ Functions reset variables  
✔ React needs persistent state  
✔ useState stores values outside component  
✔ setState triggers re-render  
✔ React avoids hidden magic  
✔ Svelte hides complexity via compiler  

---

# FINAL ONE-LINE UNDERSTANDING

React uses useState because JavaScript variables cannot persist across renders or trigger UI updates, so React provides a controlled system that stores state externally and re-renders the component when that state changes.
