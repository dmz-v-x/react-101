# React Event Handling Exercise

---

# 0. What Are We Building?

We are building a **small interactive game**:

- A ball → clicking it = WIN
- A bomb → clicking it = LOSE

---

# What This Exercise Teaches

This exercise is NOT about UI.

It teaches:

- Event handling in React (`onClick`)
- Passing functions vs calling functions
- Passing arguments to event handlers
- Understanding how React calls your function
- Understanding event objects

---

# PART 1 — Basic Version (Click Ball)

---

## Step 1 — Initial Code

```
function ClickBallGame() {
  return (
    <div className="wrapper">
      <button className="ball">
        <VisuallyHidden>
          Ball
        </VisuallyHidden>
      </button>
    </div>
  );
}
```

---

## Let’s Break This Down Line by Line

---

### Line 1

```
function ClickBallGame() {
```

👉 We are creating a **React component**

Think:

- This is just a function
- It returns UI (JSX)

---

### Line 2–9

```
return (
  <div className="wrapper">
```

👉 This is JSX (UI structure)

- `<div>` → container
- `className="wrapper"` → CSS styling

---

### Button

```
<button className="ball">
```

👉 This is a clickable button

- Styled like a ball using CSS

---

### VisuallyHidden

```
<VisuallyHidden>
  Ball
</VisuallyHidden>
```

👉 Accessibility feature

- Screen readers can read "Ball"
- But it's invisible visually

---

## Problem in This Version

👉 Clicking the ball does NOTHING

Because:

❌ No event handler attached

---

# Step 2 — Add Click Handler

---

## Code

```
function ClickBallGame() {
  function handleClick() {
    window.alert('You win!');
  }

  return (
    <div className="wrapper">
      <button
        className="ball"
        onClick={handleClick}
      >
        <VisuallyHidden>
          Ball
        </VisuallyHidden>
      </button>
    </div>
  );
}
```

---

## Step-by-Step Explanation

---

### 1. Function Inside Component

```
function handleClick() {
  window.alert('You win!');
}
```

👉 We define a function

- Runs when user clicks
- Shows alert

---

### 2. Attach Event

```
onClick={handleClick}
```

👉 We PASS function (not call it)

React will:

- Store this function
- Run it when button is clicked

---

## Flow

User clicks → React triggers `handleClick` → alert shows  

---

# PART 2 — Advanced Version (Ball + Bomb)

---

## Problem Statement

Now we have TWO buttons:

- Ball → should WIN
- Bomb → should LOSE

---

## Initial Code (Buggy)

```
function ClickBallGame() {
  function handleClick(type) {
    if (type === 'win') {
      alert('You win!');
    } else {
      alert('You lose :(');
    }
  }

  return (
    <div className="wrapper">
      <button
        className="ball"
        onClick={handleClick}
      >
        <VisuallyHidden>
          Ball
        </VisuallyHidden>
      </button>

      <button
        className="bomb"
        onClick={handleClick}
      >
        💣
      </button>
    </div>
  );
}
```

---

## What’s Wrong Here?

Both buttons call:

```
handleClick()
```

BUT:

👉 No argument is passed

---

## So What Happens?

```
function handleClick(type)
```

👉 type = ????

---

## Answer

React calls function like this:

```
handleClick(event)
```

So:

👉 type = Synthetic Event Object

---

## Result

```
if (type === 'win')
```

→ FALSE

So always:

👉 "You lose"

---

# PART 3 — The Fix (Correct Solution)

---

## Correct Code

```
<button
  className="ball"
  onClick={() => handleClick('win')}
>
```

---

```
<button
  className="bomb"
  onClick={() => handleClick('lose')}
>
```

---

# Step-by-Step Explanation

---

## 1. Wrapper Function

```
() => handleClick('win')
```

👉 This is an arrow function

---

## Important

This does NOT run immediately

It means:

👉 “When clicked → run handleClick('win')”

---

## 2. What React Receives

React gets:

```
function() {
  handleClick('win')
}
```

---

## 3. Click Flow

User clicks → React runs wrapper → wrapper calls handleClick('win')

---

## 4. Now type is correct

```
handleClick('win')
```

👉 type = "win"

---

## Condition works

```
if (type === 'win')
```

→ TRUE

---

# PART 4 — Why We Need Wrapper Function

---

## Without wrapper

```
onClick={handleClick('win')}
```

👉 Runs immediately during render

---

## With wrapper

```
onClick={() => handleClick('win')}
```

👉 Runs ONLY when clicked

---

# PART 5 — Deep Understanding

---

## React does this internally:

```
button.onclick = function(event) {
  yourFunction(event)
}
```

---

## So if you do:

```
onClick={handleClick}
```

React calls:

```
handleClick(event)
```

---

## That’s why:

👉 type becomes event object  

---

# PART 6 — Why Not Skip "lose"?

---

## You might think:

```
onClick={handleClick}
```

is fine for bomb

---

## But then:

```
handleClick(type)
```

→ type = event object

---

## Problem

Now type can be:

- "win"
- OR a complex event object

---

## This is BAD design

Why?

- Inconsistent
- Confusing
- Hard to debug

---

## Good practice

Always pass:

```
'win' OR 'lose'
```

---

# PART 7 — Key Concept Summary

---

## React Event System

- React handles events for you
- It passes event object automatically

---

## Function Passing Rule

| Code | Meaning |
|-----|--------|
| onClick={fn} | Pass function |
| onClick={fn()} | Call immediately ❌ |
| onClick={() => fn()} | Correct |

---

## Why Wrapper?

To:

- Delay execution
- Pass arguments
- Control behavior

---

# PART 8 — Real World Use Cases

---

## 1. Delete item

```
onClick={() => deleteItem(id)}
```

---

## 2. API call

```
onClick={() => fetchUser(userId)}
```

---

## 3. Update state

```
onClick={() => setCount(count + 1)}
```

---

# FINAL MENTAL MODEL

---

Think like this:

👉 React needs a function to call later  
👉 You must NOT execute it immediately  
👉 If you need arguments → wrap it  

---

# FINAL ONE-LINE UNDERSTANDING

React event handlers require function references, and when you need to pass arguments, you wrap the function inside another function so it executes only when the event occurs, not during render.
