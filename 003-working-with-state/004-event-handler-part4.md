## Event Handler - Part 4

# Step 1 — Function Reference vs Function Call

This is one of the most important concepts in React event handling.

If you understand this deeply, a large number of beginner bugs disappear.

---

# Step 2 — The Core Rule (Memorize This)

## Correct

    <button onClick={doSomething} />

## Incorrect

    <button onClick={doSomething()} />

---

## Key idea

React expects a **function**, not the **result of a function**.

---

# Step 3 — Why This Matters (Think in Time)

You must think in terms of **when things happen**.

---

## Two important moments

- Render time → when React builds the UI  
- Click time → when the user interacts  

---

## Case 1 — With parentheses ()

    onClick={doSomething()}

What you are telling React:

"Run this function immediately during render."

### What actually happens

- Function executes instantly  
- Its return value is assigned to onClick  
- Clicking later does nothing  

---

## Case 2 — Without parentheses

    onClick={doSomething}

What you are telling React:

"Here is the function. Call it later when the user clicks."

### What actually happens

- Function is NOT executed during render  
- React stores the reference  
- Function runs only when clicked  

---

# Step 4 — Visual Timeline (Critical Mental Model)

## Wrong Example

    function App() {
      console.log("render");

      function doSomething() {
        console.log("clicked");
      }

      return <button onClick={doSomething()}>Click</button>;
    }

### Console output

    render
    clicked

### Problem

- Function runs during render  
- Clicking does nothing  

---

## Correct Example

    function App() {
      console.log("render");

      function doSomething() {
        console.log("clicked");
      }

      return <button onClick={doSomething}>Click</button>;
    }

### Console output

    render

### After clicking

    clicked

---

# Step 5 — Real-World Analogy

## Wrong way

    onClick={openDoor()}

Meaning:

You are opening the door immediately instead of waiting.

---

## Correct way

    onClick={openDoor}

Meaning:

You are giving instructions:

"Open the door when the bell rings."

---

# Step 6 — Passing Arguments (Very Common Case)

## Incorrect

    <button onClick={deleteUser(userId)} />

### Problem

- Function runs immediately  
- Not waiting for click  

---

## Correct (Arrow Function)

    <button onClick={() => deleteUser(userId)} />

### Why this works

- () => deleteUser(userId) is a function  
- React calls it on click  
- Inside it, deleteUser(userId) executes  

---

## Expanded Version (Same Logic)

    function handleClick() {
      deleteUser(userId);
    }

    <button onClick={handleClick} />

---

# Step 7 — Why React Does Not Auto-Fix This

React cannot assume your intention.

- Maybe you wanted it to run immediately  
- Maybe you made a mistake  

So React leaves the responsibility to you.

---

# Step 8 — Tiny Quiz

## Which are correct?

    <button onClick={saveData} />
    <button onClick={saveData()} />
    <button onClick={() => saveData()} />
    <button onClick={() => saveData} />

---

## Correct

- <button onClick={saveData} />
- <button onClick={() => saveData()} />

---

## Incorrect

- <button onClick={saveData()} /> → runs immediately  
- <button onClick={() => saveData} /> → returns function but does not call it  

---

# Step 9 — Lock This Rule

React wants:

- A function reference  
- Not a function execution  

---

# Final Mental Model

- doSomething → "call later"  
- doSomething() → "call now"  
