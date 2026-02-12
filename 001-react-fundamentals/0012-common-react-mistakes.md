# Common React Mistakes

## 1. Mistake: Using React.createElement Like an Array

### ❌ Incorrect

    React.createElement[
        ("p", null, "Hello")
    ]

### Why This Is Wrong

- React.createElement is a **function**
- Square brackets are for arrays
- JavaScript treats this as invalid syntax

### ✅ Correct

    React.createElement(
        "p",
        null,
        "Hello"
    )

Rule to remember:

> If it creates something, it is **called**, not indexed.

---

## 2. Mistake: Incorrect Children Nesting

### ❌ Incorrect Example

    React.createElement(
        "ul",
        null,
        React.createElement("li", null, "Apple", "Banana")
    )

### Why This Is Wrong

- One element cannot have multiple **text children** like this
- "Apple" and "Banana" are treated as two children of the same `li`
- This produces invalid UI structure

---

### ✅ Correct Way (Separate Elements)

    React.createElement(
        "ul",
        null,
        React.createElement("li", null, "Apple"),
        React.createElement("li", null, "Banana")
    )

Each list item must be its **own element**.

---

## 3. Understanding Children: Single vs Multiple

### Single Child

    React.createElement("h1", null, "Hello")

- One child
- Passed directly
- No array needed

---

### Multiple Children (Arguments)

    React.createElement(
        "div",
        null,
        "Hello ",
        "World"
    )

React accepts multiple children as **separate arguments**.

---

## 4. Arrays Are Optional (Very Important)

Many beginners think:

> “If there are multiple children, I must use an array”

This is **false**.

### These Are Equivalent

    React.createElement(
        "div",
        null,
        child1,
        child2
    )

and

    React.createElement(
        "div",
        null,
        [child1, child2]
    )

React internally normalizes both.

---

## 5. When Arrays Improve Readability

Arrays are **not required**, but they help when:

- Children are generated dynamically
- You are mapping over data
- The structure becomes visually clearer

Example:

    const items = [
        React.createElement("li", null, "Apple"),
        React.createElement("li", null, "Banana")
    ];

    React.createElement("ul", null, items)

Here, arrays improve clarity.

---

## 6. When Arrays Are Unnecessary

Do NOT use arrays when:

- There is only one child
- Children are static and simple

This is unnecessary:

    React.createElement("p", null, ["Hello"])

Prefer this:

    React.createElement("p", null, "Hello")

---

## 7. Mistake: Rendering a Component Incorrectly

### ❌ Incorrect

    root.render(MyComponent)

### Why This Is Wrong

- MyComponent is a **function**
- React expects a **React element**
- You are passing a reference, not an instance

---

### ✅ Correct (JSX)

    root.render(<MyComponent />)

JSX creates a React element.

---

### ✅ Correct (Without JSX)

    root.render(
        React.createElement(MyComponent)
    )

Both produce a React element object.

---

## 8. Core Rule to Remember

React renders **elements**, not functions.

- Components are functions
- Elements are objects
- React.createElement or JSX creates elements

---

## 9. Mental Checklist for Raw React APIs

Before blaming React, ask:

- Am I calling createElement with parentheses?
- Did I pass props as the second argument?
- Are children structured correctly?
- Am I rendering an element, not a function?
- Did I avoid unnecessary arrays?

Most bugs disappear when these are correct.

**Start Blog 8**
