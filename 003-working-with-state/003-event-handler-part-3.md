## Event Handler - Part 3

# Step 1 — CamelCase Gotcha (onClick vs onclick)

This looks like a small detail, but it is one of the most common beginner mistakes in React.

---

# Step 2 — HTML Way (Not React)

    <button onclick="doSomething()">Click</button>

### What is happening here?

- Attribute name is lowercase: onclick  
- Value is a string  
- The browser reads the string and executes it  

### Key idea

This is **pure HTML behavior**, not React.

---

# Step 3 — React Way (JSX)

    <button onClick={doSomething}>Click</button>

### What is happening here?

- Attribute name is camelCase: onClick  
- Value is a JavaScript function  
- Wrapped in curly braces {}  
- React handles the event internally  

---

# Step 4 — Key Differences

## Naming

- HTML → onclick (lowercase)  
- React → onClick (camelCase)  

---

## Value type

- HTML → string ("doSomething()")  
- React → function reference (doSomething)  

---

## Syntax

- HTML → no braces  
- React → must use {}  

---

# Step 5 — What happens if you use lowercase in React?

    <button onclick={doSomething}>Click</button>

### Result

React will:

- Ignore the handler  
- Show a warning  

Example warning:

    Warning: Invalid event handler property `onclick`. Did you mean `onClick`?

### Important consequence

- The button will NOT work  
- Your handler will never run  

---

# Step 6 — Why camelCase in React?

Because JSX is not HTML.

JSX is **JavaScript-like syntax**.

---

## In JavaScript

Properties use camelCase:

- onClick  
- onChange  
- onKeyDown  
- onMouseEnter  

---

## Examples

    <input onChange={handleChange} />
    <input onKeyDown={handleKeyDown} />
    <div onMouseEnter={handleHover} />

---

# Step 7 — Easy Memory Trick

Think like this:

- If it looks like HTML → lowercase  
- If it is JSX (React) → camelCase  

---

# Step 8 — Tiny Exercise

### Find the bugs

    <button onclick={handleClick}>A</button>
    <input onchange={handleChange} />
    <div onmouseover={handleHover}></div>

---

## Correct versions

    <button onClick={handleClick}>A</button>
    <input onChange={handleChange} />
    <div onMouseOver={handleHover}></div>

---

# Step 9 — Lock This Rule

JSX is NOT HTML.

JSX follows JavaScript rules.

That means:

- Use camelCase for event names  
- Pass functions, not strings  
- Always use {} for JavaScript expressions  

---

# Final Mental Model

- HTML → string-based event handling  
- JSX → function-based event handling  

