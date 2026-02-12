# Raw React APIs

## 1. React Before JSX (Important Context)

JSX did NOT exist in the beginning.

React was originally used by calling **functions directly**.

The most important of these functions is:

- React.createElement

Everything in React still builds on this API.

---

## 2. What React.createElement Really Is

React.createElement is a **factory function**.

It creates a **React element object**.

It does NOT:
- Create DOM nodes
- Update the screen
- Touch the browser

It only creates **descriptions**.

---

## 3. The Signature of React.createElement

React.createElement takes **three types of arguments**, in this order:

1. type  
2. props  
3. children (one or many)

Conceptually:

    React.createElement(type, props, children)

---

## 4. The First Argument — type

The type tells React **what kind of element** this is.

Examples:
- "div"
- "h1"
- "p"
- A component function

Example:

    React.createElement("h1", null, "Hello")

---

## 5. The Second Argument — props

Props are:
- Attributes
- Configuration
- Data passed to the element

Examples:
- className
- id
- title
- event handlers

Example:

    React.createElement(
        "h1",
        { id: "greeting", className: "title" },
        "Hello"
    )

If there are no props, you must pass:
- null

You cannot skip this argument.

---

## 6. The Third Argument — children (Core Topic)

Children represent:
- What goes inside the element

This is where most confusion happens.

---

## 7. Single Child

If the element has **one child**, pass it directly.

Example:

    React.createElement("h1", null, "Hello World")

The child here is:
- A string

This is the simplest and most common case.

---

## 8. Multiple Children (As Arguments)

If there are **multiple children**, you can pass them as separate arguments.

Example:

    React.createElement(
        "ul",
        null,
        React.createElement("li", null, "Apple"),
        React.createElement("li", null, "Banana")
    )

Each child is passed **one after another**.

---

## 9. Multiple Children (As an Array)

You can also pass children as an array.

Example:

    React.createElement(
        "ul",
        null,
        [
            React.createElement("li", null, "Apple"),
            React.createElement("li", null, "Banana")
        ]
    )

This is:
- Optional
- Not required
- Often used for readability

---

## 10. Array vs Arguments (Important Clarification)

These two are **equivalent**:

    React.createElement(
        "ul",
        null,
        child1,
        child2
    )

and

    React.createElement(
        "ul",
        null,
        [child1, child2]
    )

React internally normalizes both forms.

---

## 11. When Should You Use Arrays?

Use arrays when:
- Children are generated dynamically
- You are mapping over data
- Readability improves

Do NOT use arrays:
- Just because you think they are required
- For single children

Arrays are **optional**, not mandatory.

---

## 12. Common Incorrect Usage (Very Important)

### ❌ Bracket Syntax Error

This is WRONG:

    React.createElement[
        ("p", null, "Text")
    ]

React.createElement is a function, not an array.

You must use parentheses.

---

### ❌ Missing props argument

This is WRONG:

    React.createElement("h1", "Hello")

Because:
- "Hello" is treated as props
- children are missing

Correct version:

    React.createElement("h1", null, "Hello")

---

### ❌ Incorrect children nesting

This is WRONG:

    React.createElement(
        "ul",
        null,
        React.createElement("li", null, "A", "B")
    )

One element cannot have two text children like this.

---

## 13. Correct Usage Patterns

Correct single child:

    React.createElement("p", null, "Hello")

Correct multiple children:

    React.createElement(
        "p",
        null,
        "Hello ",
        "World"
    )

Correct nested structure:

    React.createElement(
        "div",
        null,
        React.createElement("p", null, "Text"),
        React.createElement("p", null, "More Text")
    )

---

## 14. Why JSX Exists (Preview)

React.createElement works, but:
- It is verbose
- It is hard to read
- It is deeply nested

JSX exists to:
- Make UI readable
- Match how humans think about markup
- Reduce mental overhead

JSX compiles directly into React.createElement.
