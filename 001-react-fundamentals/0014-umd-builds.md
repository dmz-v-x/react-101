# UMD Builds 

## 1. What Does UMD Mean?

UMD stands for:

Universal Module Definition

The name itself explains the purpose:

> One JavaScript file that works in **many different environments**.

Those environments included:
- Browsers
- Node.js
- Bundlers
- Older systems with no module support

UMD was a **compatibility solution**, not a new language feature.

---

## 2. Why UMD Existed

Before modern JavaScript modules:
- Browsers had no import/export
- JavaScript files ran globally
- Different environments had different module systems

There was **no single standard**.

UMD was created to answer this question:

> How can one library work everywhere without rewriting it?

---

## 3. The World Before import/export

In the early days:
- JavaScript files were loaded using script tags
- Files executed immediately
- Everything lived in the global scope

Example:

    <script src="app.js"></script>

There was:
- No module isolation
- No dependency graph
- No automatic loading order management

---

## 4. How Libraries Exposed Themselves Back Then

Since everything was global, libraries did this:

- Attach themselves to the window object

This made the library accessible everywhere.

Example idea:

    window.React
    window.ReactDOM

This was not a React-specific choice — it was the norm.

---

## 5. How React Was Used with UMD Builds

To use React with UMD, you only needed script tags.

Example:

    <script src="react.development.js"></script>
    <script src="react-dom.development.js"></script>

What happens here:

1. Browser loads react.development.js
2. React attaches itself to window.React
3. Browser loads react-dom.development.js
4. ReactDOM attaches itself to window.ReactDOM

No imports.  
No build step.  
No configuration.

---

## 6. Using React After Loading UMD Builds

Once the scripts were loaded, you could write code like this:

    const element = React.createElement("h1", null, "Hello World");

    const container = document.getElementById("root");
    ReactDOM.render(element, container);

Important points:
- React is accessed via window.React
- ReactDOM is accessed via window.ReactDOM
- These globals exist because UMD attached them

---

## 7. Why No import Was Needed

There was no import because:
- JavaScript did not support modules yet
- Everything was already in the global scope

React and ReactDOM were simply:
- Global variables
- Available everywhere after script loading

This is why old tutorials never showed import statements.

---

## 8. Why UMD Was Popular

UMD had big advantages at the time:

- Extremely easy to use
- No tooling required
- Worked in all browsers
- Worked without Node.js

For learning and small demos, UMD was perfect.

---

## 9. The Big Downsides of UMD

As applications grew, UMD caused problems:

- Global namespace pollution
- Name collisions
- No dependency graph
- Hard to scale
- Hard to optimize
- Hard to tree-shake

These problems pushed the ecosystem forward.

---

## 10. Why UMD Still Exists Today

UMD still exists because:
- Legacy projects depend on it
- Simple demos still benefit from it
- Learning environments use it
- Backward compatibility matters

React still ships UMD builds for these reasons.

---

## 11. UMD vs Modern React Usage (High Level)

UMD:
- Uses script tags
- Exposes globals
- No import/export
- No build step

Modern React:
- Uses ESM
- Uses import/export
- Uses build tools or CDNs
- Avoids globals

Both are valid — context matters.
