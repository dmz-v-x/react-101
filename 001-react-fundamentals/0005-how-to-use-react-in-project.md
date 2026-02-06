# How to Use React in a Project (From Absolute Basics)

This section explains **what React actually is**, **how it works internally**, **why we use it**, and **how React code reaches the browser** — step by step, without assuming any prior knowledge.

We’ll also clearly explain:
- React vs ReactDOM
- Raw React APIs
- `react.createElement`
- How React fits into a real project

---

## 1. What Is React?

### Simple Definition

**React is a JavaScript library for building user interfaces.**

More precisely:
> React is a library that helps you **describe what your UI should look like for a given state** and keeps the UI in sync when that state changes.

React focuses on **one thing only**:
- The **view layer** (what users see)

It does NOT handle:
- Routing (by itself)
- HTTP requests
- Databases
- Authentication
- Build systems

Those are handled by other tools.

---

## 2. Why Do We Use React?

As applications grow, UI code becomes:
- Hard to manage
- Full of manual DOM updates
- Bug-prone
- Difficult to reason about

React solves this by:
- Removing manual DOM manipulation
- Enforcing predictable UI updates
- Encouraging component-based architecture
- Making large UIs manageable

In short:
> React scales UI complexity.

---

## 3. How React Works (High-Level Mental Model)

React follows one core idea:

### UI = Function of State

That means:
- You describe **what the UI should look like**
- Based on **current state**
- React handles **how** to update the DOM

You never say:
- “Find this element”
- “Update this text”
- “Remove that node”

React calculates changes for you.

---

## 4. What React Uses Internally

Internally, React uses several important ideas:

---

### 1. Virtual DOM

- React keeps an **in-memory representation** of the UI
- This is called the **Virtual DOM**
- It is just JavaScript objects

When state changes:
- React builds a new Virtual DOM
- Compares it with the previous one (diffing)
- Updates only the real DOM parts that changed

This makes updates:
- Efficient
- Predictable
- Fast

---

### 2. Reconciliation

**Reconciliation** is React’s process of:
- Comparing old UI tree with new UI tree
- Deciding the minimal DOM changes needed

You never run reconciliation manually.
React does it automatically.

---

### 3. Declarative Rendering

React uses **declarative programming**:
- You describe the desired result
- React figures out the steps

This is opposite of imperative DOM manipulation.

---

## 5. How React Is Used in a Real Project

You **never use React alone**.

A real React project usually includes:
- React (UI library)
- ReactDOM (DOM renderer)
- A build system (Vite / Webpack / etc.)

Flow looks like this:

1. You write React code (JSX, components)
2. Build system converts it to plain JavaScript
3. Browser loads the output
4. React runs and updates the DOM

---

## 6. React Package vs ReactDOM Package (Say This Correctly)

This is extremely important.

---

### `react` Package

The **react** package contains:
- Core React logic
- Component creation
- Hooks
- Virtual DOM logic

It is:
- Platform-agnostic

Meaning:
- It does NOT know about the browser
- It does NOT touch the DOM

React can be used for:
- Web
- Mobile (React Native)
- Desktop
- Other platforms

---

### `react-dom` Package

The **react-dom** package:
- Knows about the browser DOM
- Takes React elements
- Renders them into real DOM nodes

In simple terms:
> `react` decides *what* to render  
> `react-dom` decides *where* and *how* to render it in the browser

---

## 7. How React Reaches the Browser

You usually see code like:

    import React from "react";
    import ReactDOM from "react-dom/client";

React:
- Creates elements
- Manages state
- Handles updates

ReactDOM:
- Mounts React elements into a DOM node

---

## 8. What Are “Raw React APIs”?

Before JSX existed, React was used **directly through functions**.

These are called **raw React APIs**.

The most important one is:

### `react.createElement`

This is the **core API** of React.

Everything else builds on top of it.

---

## 9. Understanding `react.createElement`

### What It Does

`React.createElement` creates a **React element object**.

It does NOT:
- Create real DOM nodes
- Render anything on screen

It just creates a **description** of the UI.

---

### Example

    React.createElement("h1", null, "Hello World")

This means:
- Element type: `h1`
- Props: `null`
- Children: `"Hello World"`

React turns this into an object like:

    {
      type: "h1",
      props: {
        children: "Hello World"
      }
    }

This object lives in memory.

---

## 10. JSX Is Just Sugar Over `createElement`

When you write JSX:

    <h1>Hello World</h1>

The build system converts it into:

    React.createElement("h1", null, "Hello World")

Important correction:
> JSX is NOT HTML  
> JSX is syntax that compiles into `React.createElement`

---

## 11. Why We Don’t Write `createElement` Manually

You *can* write raw React:

    const element = React.createElement(
      "div",
      null,
      React.createElement("h1", null, "Hello World")
    );

But this is:
- Hard to read
- Hard to maintain
- Deeply nested

JSX exists to:
- Improve readability
- Match how humans think about UI
- Reduce mental overhead

---

## 12. Putting It All Together (Mental Model)

Let’s connect everything:

1. You write JSX
2. Build system converts JSX → `React.createElement`
3. React creates Virtual DOM objects
4. React compares changes
5. ReactDOM updates the real DOM

You:
- Describe UI
React:
- Figures out updates
Browser:
- Displays the result

---

## Final Takeaway

- React is a **UI library**, not a framework
- React focuses on **what the UI should look like**
- ReactDOM connects React to the browser
- `React.createElement` is the core primitive
- JSX is just a nicer way to write `createElement`
- Build systems prepare React code for browsers

If you understand this foundation,
everything else in React will feel **logical instead of magical**.
