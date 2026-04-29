## Event Handler - Part 6

# Common Beginner Mistakes with React Event Handlers

We will go one mistake at a time, understand **why it happens**, and then see the **correct fix**.

---

# Step 1 — Mistake: Calling the Function Instead of Passing It

## Incorrect

    <button onClick={handleClick()} />

---

## Why this is wrong

- The function runs immediately during render  
- It does not wait for a click  
- The return value is assigned to onClick  
- Clicking the button does nothing  

---

## Correct

    <button onClick={handleClick} />

---

## Rule

Always pass a **function reference**, not a function call.

---

# Step 2 — Mistake: Using onclick Instead of onClick

## Incorrect

    <button onclick={handleClick} />

---

## What happens

- React ignores the handler  
- The button does nothing  
- A warning appears in the console  

---

## Correct

    <button onClick={handleClick} />

---

## Rule reminder

- JSX uses camelCase  
- HTML uses lowercase  

---

# Step 3 — Mistake: Forgetting preventDefault() in Forms

## Incorrect

    function handleSubmit() {
      console.log("submitted");
    }

    <form onSubmit={handleSubmit}>
      <button>Submit</button>
    </form>

---

## What happens

- Browser reloads the page  
- React app resets  
- State is lost  

---

## Correct

    function handleSubmit(event) {
      event.preventDefault();
      console.log("submitted");
    }

---

## Key idea

Prevent the browser’s default behavior and handle it in React.

---

# Step 4 — Mistake: Using addEventListener Inside React Components

## Incorrect

    useEffect(() => {
      document.querySelector("button")
        .addEventListener("click", handleClick);
    }, []);

---

## Why this is problematic

- React is unaware of this listener  
- Cleanup must be handled manually  
- Risk of memory leaks  
- Can cause unexpected bugs  

---

## Correct

    <button onClick={handleClick} />

---

## When addEventListener is acceptable

- window events  
- document events  
- third-party or non-React elements  

---

# Step 5 — Mistake: Misunderstanding onChange Behavior

## HTML behavior

- onchange fires when input loses focus  

---

## React behavior

- onChange fires on every keystroke  

    <input onChange={handleChange} />

---

## Important note

This is intentional and useful for real-time updates.

---

# Step 6 — Mistake: Mutating Variables Directly

## Incorrect

    function handleClick() {
      count++; 
    }

---

## Why this is wrong

- React does not detect the change  
- UI will not update  

---

## Correct pattern

Use state updates instead (covered in later modules).

---

## Key idea

Event handlers should trigger **state updates**, not mutate variables directly.

---

# Step 7 — Mistake: Overusing Inline Arrow Functions Without Understanding

## Example

    <button onClick={() => doSomething()} />

---

## Important clarification

- This is not wrong  
- But a new function is created on every render  

---

## Impact

- Usually fine  
- Can affect performance in large or complex components  

---

## When to use it

- When passing arguments  
- When logic is small and simple  

---

# Step 8 — Golden Rules Summary

## Always follow these rules

- Pass function references, not function calls  
- Use camelCase for event names  
- Use preventDefault() for form submissions  
- Avoid direct DOM manipulation  
- Let React manage the DOM  
- Use events to trigger state updates, not manual DOM changes  

---

# Final Mental Model

- Events trigger handlers  
- Handlers update state  
- State updates re-render UI  
