## Event Handler - Part 8

# When NOT to Use onClick (and What to Use Instead)

Many beginners overuse onClick.

React works best when you use the **semantic event** that matches the user’s action.

---

# Step 1 — Using onClick for Form Submission

## Incorrect (very common)

    <button onClick={handleSubmit}>Submit</button>

---

## Why this is a problem

- Pressing Enter key will NOT trigger submission  
- Breaks accessibility (keyboard users affected)  
- Bypasses native browser form behavior  

---

## Correct

    <form onSubmit={handleSubmit}>
      <button type="submit">Submit</button>
    </form>

---

## Why this is better

- Enter key works automatically  
- Screen readers understand it  
- Browser semantics are preserved  

---

# Step 2 — Clicking on Non-Interactive Elements

## Incorrect

    <div onClick={openMenu}>Menu</div>

---

## Why this is bad

- div is not keyboard-accessible  
- Cannot be focused  
- No support for Enter or Space keys  
- Violates accessibility standards  

---

## Correct

    <button onClick={openMenu}>Menu</button>

---

## Rule

If it looks clickable, use a button.

---

# Step 3 — Using onClick for Text Input

## Incorrect

    <input onClick={handleChange} />

---

## Correct

    <input onChange={handleChange} />

---

## Why

- onChange fires on every keystroke  
- onClick only fires when mouse is clicked  

---

# Step 4 — Using onClick for Navigation

## Incorrect

    <div onClick={() => goTo("/home")}>Home</div>

---

## Better (HTML)

    <a href="/home">Home</a>

---

## Better (React Router)

    <Link to="/home">Home</Link>

---

## Why this matters

- Middle-click works  
- Open in new tab works  
- Browser navigation behavior is preserved  

---

# Step 5 — Using onClick for Toggle Without State

## Incorrect

    function handleClick() {
      document.body.classList.toggle("dark");
    }

---

## Why this is bad

- Direct DOM manipulation  
- React does not know what changed  
- UI can become inconsistent  

---

## Correct approach

- Event triggers state update  
- State controls UI changes  

---

## Pattern

Event → State → UI

---

# Step 6 — Golden Semantic Mapping

Use the correct event for the correct user action.

---

## Mapping

| User Action        | Correct Event   |
|------------------|----------------|
| Click button      | onClick        |
| Submit form       | onSubmit       |
| Type in input     | onChange       |
| Keyboard press    | onKeyDown      |
| Hover             | onMouseEnter   |
| Focus             | onFocus        |
| Blur              | onBlur         |

---

# Step 7 — Core Principle

Do not choose events based on convenience.

Choose events based on **intent and semantics**.

---

# Final Mental Model

- Use the right HTML element  
- Use the matching React event  
- Let browser behavior work with React, not against it  
