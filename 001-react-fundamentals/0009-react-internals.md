# React Internals

## 1. The First Big Truth About React

React does **not** work with the real DOM directly.

Instead, React works with **descriptions of the UI**.

These descriptions are called **React elements**.

Everything else in React is built on this idea.

---

## 2. What Is a React Element?

A **React element** is:
> A plain JavaScript object that describes what the UI should look like.

Important clarifications:
- It is NOT a DOM node
- It is NOT visible on screen
- It does NOT change the browser

It is just **data**.

---

## 3. A React Element Is a Description

Think of a React element as a **blueprint**.

A blueprint:
- Describes a house
- Is not the house itself

Similarly:
- A React element describes UI
- It is not the UI itself

React collects these descriptions and decides what to do with them.

---

## 4. What React.createElement Really Does

When you use React.createElement, React creates a JavaScript object.

Conceptually, something like this:

    {
        type: "h1",
        props: {
            children: "Hello World"
        }
    }

This object:
- Lives in memory
- Is easy to compare
- Is easy to recreate

React prefers data over direct DOM manipulation.

---

## 5. The Virtual DOM (Simple Explanation)

The **Virtual DOM** is:
> A tree of React elements kept in memory.

It mirrors what the UI should look like.

Important points:
- It is NOT the real DOM
- It is NOT slow
- It is just JavaScript objects

Because it is in memory:
- It is fast to create
- It is fast to compare

---

## 6. Why React Uses a Virtual DOM

React needs a safe place to:
- Build new UI versions
- Compare old vs new UI
- Decide minimal changes

Doing this directly on the real DOM would be:
- Slow
- Risky
- Hard to control

The Virtual DOM acts as a **buffer**.

---

## 7. Reconciliation (Why React Is Fast)

**Reconciliation** is React’s process of:
> Comparing the previous UI description with the new one.

Steps:
1. State changes
2. React creates a new Virtual DOM tree
3. React compares it with the old tree
4. React finds what actually changed

This comparison is:
- Predictable
- Optimized
- Much cheaper than full DOM updates

---

## 8. What React Actually Updates

React does NOT:
- Re-render the entire page
- Destroy everything and rebuild it

React:
- Updates only the parts that changed
- Leaves everything else untouched

This is why React feels fast.

---

## 9. Why React Needs a Renderer

React itself only:
- Creates UI descriptions
- Compares descriptions

React does **not** know:
- How to draw on the screen
- What a browser DOM is
- What native mobile views are

So React needs a **renderer**.

---

## 10. What Is a Renderer?

A renderer is:
> A layer that takes React elements and turns them into real UI.

Examples:
- react-dom → renders to browser DOM
- react-native → renders to mobile views
- other renderers → render elsewhere

React = logic  
Renderer = output

---

## 11. Why This Design Is Powerful

Because of this separation:
- React can run in many environments
- UI logic stays the same
- Only the renderer changes

This is why React is flexible and long-lasting.

---

## 12. Removing the “Magic” Feeling

React is not magic because:
- It uses plain JavaScript objects
- It uses comparison, not guessing
- It separates logic from rendering

Everything React does:
- Is deterministic
- Is repeatable
- Is explainable
