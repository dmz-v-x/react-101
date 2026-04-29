## Event Handler - Part 2

# React’s onClick — Same Idea, Different Owner

Before React:
- The **browser owns the DOM**
- You manually manage events

With React:
- **React owns the DOM**
- You ask React to handle events

### Key mindset shift

You are no longer directly controlling the DOM.

You are **describing what should happen**, and React takes care of the implementation.

---

# Step 1 — Plain JavaScript vs React (Big Picture)

## Plain JavaScript

    const button = document.querySelector('.btn');
    button.addEventListener('click', doSomething);

### What is happening here?

- You manually find the element
- You manually attach the event listener
- You must manually clean it up later
- You are directly interacting with the DOM

---

## React

    function App() {
      function doSomething() {
        console.log('Clicked!');
      }

      return <button onClick={doSomething}>Click me</button>;
    }

### What is happening here?

- No querySelector
- No addEventListener
- No manual cleanup

Instead:

- You declare behavior using JSX
- React handles DOM interaction
- React attaches and removes listeners automatically

### Core idea

You are **declaring intent**, not manually wiring behavior.

---

# Step 2 — What does onClick actually mean in React?

### Code

    <button onClick={doSomething}>

### What you are telling React

"React, when you create this button in the DOM, attach a click listener and call doSomething when it is clicked."

### Important clarification

You are NOT adding the listener yourself.

React is doing it for you behind the scenes.

---

## Comparison with HTML

### HTML (old way)

    <button onclick="doSomething()">Click</button>

### React (JSX)

    <button onClick={doSomething}>Click</button>

---

## Key differences

HTML:

- Uses strings
- Executes code from string

React:

- Uses real JavaScript functions
- Safer and more powerful
- No string evaluation

---

# Step 3 — Why React prefers onClick over addEventListener

## Reason 1 — Automatic cleanup (very important)

### Vanilla JavaScript

    button.addEventListener('click', handler);

    // later
    button.removeEventListener('click', handler);

If you forget to remove it:

- Memory leaks occur
- Unexpected behavior happens

---

### React

    <button onClick={handler} />

When:

- Component unmounts
- Element is removed

React automatically removes the listener.

---

## Reason 2 — Better performance

React:

- Centralizes event handling
- Uses internal optimizations
- Reduces unnecessary listeners
- Manages memory efficiently

You do not see this directly, but it improves performance significantly in large applications.

---

## Reason 3 — No direct DOM interaction (critical rule)

### React philosophy

"You describe what you want. React decides how to do it."

---

### What to avoid in React

- document.querySelector(...)
- document.getElementById(...)
- Manual DOM manipulation
- addEventListener (in most cases)

---

### What to use instead

- JSX
- Props like onClick, onChange
- State and props for dynamic behavior

---

## Why avoiding DOM access matters

If you manually manipulate the DOM:

- You break React’s control
- UI can become inconsistent
- Bugs become difficult to track

---

# Step 4 — “Stay within the abstraction”

React is an abstraction over the DOM.

### What does abstraction mean?

It hides complexity and gives you a simpler interface.

---

## If you fight React

- You write more code
- Things feel confusing
- Bugs appear unexpectedly

---

## If you follow React’s model

- Less code
- Predictable behavior
- Easier reasoning

---

## Important idea

Do not mix old patterns (like jQuery-style DOM manipulation) with React.

It creates conflicts.

---

# Step 5 — Visual Mental Model

Think of the system like this:

- You → describe UI and behavior
- React → manages DOM and event wiring
- Browser → executes actual events

---

## Flow

User clicks → Browser creates event → React handles it → Your function runs

---

## Important rule

Do not bypass React to talk directly to the browser unless absolutely necessary.

---

# Step 6 — Tiny Recap 

- onClick in React is not the same as HTML onclick
- You pass a function reference, not a string
- React attaches and removes listeners automatically
- You do not use addEventListener in normal React code

---

## When you might still use addEventListener

Only in special cases:

- window events (e.g., resize, scroll)
- document-level events
- third-party libraries
- non-React-controlled elements

---

# Final Mental Model

- React owns the DOM
- You describe behavior using JSX
- React handles event listeners internally
- You focus on logic, not wiring
