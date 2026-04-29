# React Core Loop

---

# 0. What Is This Concept About?

This is one of the **MOST IMPORTANT concepts in React**.

It explains:

👉 How React updates the UI  
👉 What happens when state changes  
👉 Why React is called "React"  
👉 How your code turns into real DOM  

---

# 1. Big Picture (Very Simple First)

React works in a loop:

1. You describe UI (using JSX)
2. React creates a snapshot (JavaScript object)
3. State changes
4. React creates a new snapshot
5. React compares old vs new
6. React updates only what changed

---

# 2. The Core Example (Counter)

---

```
function Counter() {
  const [count, setCount] = React.useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Value: {count}
    </button>
  );
}
```

---

# 3. Step 1 — First Render (Mount Phase)

---

## What happens when app loads?

React calls your component:

```
Counter()
```

---

## Inside the function

```
const [count, setCount] = React.useState(0);
```

👉 React creates state:

	count = 0

---

## JSX is returned

```
<button>Value: 0</button>
```

---

# 4. JSX is NOT HTML (Important)

---

React converts JSX into JavaScript:

```
React.createElement(
  'button',
  { onClick: () => setCount(count + 1) },
  'Value: ',
  count
);
```

---

# 5. What React.createElement returns

---

It creates a JavaScript object:

```
{
  type: 'button',
  props: {
    onClick: function,
    children: ['Value: ', 0]
  }
}
```

---

## Important

👉 This is NOT DOM  
👉 This is a "description" of UI  

---

# 6. React Creates Real DOM

---

React reads this object and creates:

```
<button>Value: 0</button>
```

---

## Also attaches event

```
onClick → setCount function
```

---

# 7. This is called "Mount"

---

Mount = first time rendering UI

---

# 8. Now User Clicks Button

---

## What happens?

```
onClick → setCount(count + 1)
```

---

## So:

count = 1

---

# 9. This Triggers Re-render

---

React does NOT update UI directly.

Instead:

👉 React calls component AGAIN

```
Counter()
```

---

# 10. Second Render (New Snapshot)

---

Now:

```
count = 1
```

---

## JSX becomes

```
<button>Value: 1</button>
```

---

## Again converted to JS object

```
{
  type: 'button',
  props: {
    children: ['Value: ', 1]
  }
}
```

---

# 11. Now React Has TWO Snapshots

---

## Old

```
<button>Value: 0</button>
```

---

## New

```
<button>Value: 1</button>
```

---

# 12. The Big Question

---

👉 What changed?

---

# 13. Reconciliation (Core React Magic)

---

React compares:

Old vs New

---

## It finds:

- Button is SAME
- Only text changed

---

## So React decides:

👉 Only update text  

---

# 14. DOM Update (Commit Phase)

---

React does:

```
button.innerText = "Value: 1";
```

---

## Important

👉 React does NOT recreate entire DOM  
👉 Only updates what changed  

---

# 15. This Entire Process = React Loop

---

## Full Flow

### 1. Mount

First render → create DOM

---

### 2. Trigger

User action (click)

---

### 3. Render

Component runs again

---

### 4. Reconciliation

Compare old vs new

---

### 5. Commit

Update DOM

---

# 16. Visual Flow

---

Mount → Trigger → Render → Compare → Update  

---

# 17. Snapshot Mental Model (Very Important)

---

Each render = snapshot

---

## Example

Snapshot 1:

```
Value: 0
```

Snapshot 2:

```
Value: 1
```

---

React compares snapshots like:

👉 "spot the difference" game  

---

# 18. Why React is Fast

---

Because:

- It does NOT rebuild DOM
- It only updates changes

---

# 19. Why This Matters

---

Without this system:

- UI updates would be slow
- More bugs
- Hard to manage state

---

# 20. Important Observations

---

## 1. Component runs again

React does NOT update variable

👉 It re-runs function

---

## 2. State persists outside function

Even though function runs again

---

## 3. UI is derived from state

UI = function(state)

---

# 21. Key Concepts Summary

---

## JSX → JavaScript Object

---

## React Element

A plain object describing UI

---

## Render

Running component function

---

## Reconciliation

Comparing old vs new

---

## Commit

Updating DOM

---

# 22. What React Does NOT Do

---

❌ It does NOT directly manipulate DOM every time  
❌ It does NOT store UI as HTML  
❌ It does NOT mutate variables  

---

# 23. Real-Life Analogy

---

Think of React like:

👉 A photographer

---

Each render:

- Takes a photo (snapshot)
- Compares with previous photo
- Fixes only differences

---

# 24. Final Mental Model (MOST IMPORTANT)

---

React is NOT:

👉 "Update this element"

---

React is:

👉 "Given this state, UI should look like THIS"

---

Then React figures out:

👉 "How to update DOM efficiently"

---

# 25. Final Summary

---

✔ React creates UI descriptions (objects)  
✔ Each render creates a new snapshot  
✔ State change triggers re-render  
✔ React compares old vs new (reconciliation)  
✔ React updates only what's needed (commit)  
✔ This loop is the core of React  

---

# FINAL ONE-LINE UNDERSTANDING

React works by re-running your components to create new UI snapshots, comparing them with previous ones, and efficiently updating only the changed parts of the DOM through a process called reconciliation.
