## Event Handler - Part 7


# Real-World React Event Handler Examples

We will go one scenario at a time, exactly how these patterns appear in real applications.

---

# Step 1 — Button Click (Most Basic)

## Use case

User clicks a button and something happens.

---

## Code

    function App() {
      function handleClick() {
        console.log("Button clicked");
      }

      return <button onClick={handleClick}>Click me</button>;
    }

---

## What is happening

- React renders the button  
- User clicks  
- React calls handleClick  

---

## Key idea

- No DOM lookup  
- No addEventListener  
- Clean and declarative  

---

# Step 2 — Button with Argument (Delete, Select, etc.)

## Use case

Perform an action on a specific item (e.g., delete item).

---

## Code

    function App() {
      function deleteItem(id) {
        console.log("Deleting item", id);
      }

      return (
        <button onClick={() => deleteItem(42)}>
          Delete
        </button>
      );
    }

---

## Why use an arrow function?

- You need to pass an argument (id)  
- React still expects a function  
- Arrow function provides that wrapper  

---

## Key idea

Very common pattern in lists and dynamic UI.

---

# Step 3 — Input Field (Typing Text)

## Use case

Search box, name input, email input.

---

## Code

    function App() {
      function handleChange(event) {
        console.log(event.target.value);
      }

      return <input onChange={handleChange} />;
    }

---

## What happens

- Every keystroke triggers onChange  
- React passes the event  
- event.target.value gives current input value  

---

## Key idea

This is a core React pattern used in almost every form.

---

# Step 4 — Form Submission

## Use case

Login form, signup form, any form submission.

---

## Code

    function App() {
      function handleSubmit(event) {
        event.preventDefault();
        console.log("Form submitted");
      }

      return (
        <form onSubmit={handleSubmit}>
          <input />
          <button>Submit</button>
        </form>
      );
    }

---

## Key points

- Use onSubmit on the form (not onClick on button)  
- Prevent page reload using preventDefault()  
- One handler can manage the entire form  

---

# Step 5 — Toggle Behavior (Open / Close)

## Use case

Modal toggle, dropdown open/close, sidebar visibility.

---

## Code

    function App() {
      function toggle() {
        console.log("Toggled");
      }

      return <button onClick={toggle}>Toggle</button>;
    }

---

## What happens

- User clicks  
- Handler runs  
- Later, this will update state  

---

## Important idea

- Events trigger state updates  
- State updates control UI  

---

# Step 6 — Keyboard Events

## Use case

Trigger action on Enter, keyboard shortcuts.

---

## Code

    function App() {
      function handleKeyDown(event) {
        if (event.key === "Enter") {
          console.log("Enter pressed");
        }
      }

      return <input onKeyDown={handleKeyDown} />;
    }

---

## Common keyboard events

- onKeyDown  
- onKeyUp  
- onKeyPress (legacy)  

---

## Key idea

React gives access to key information through event.key.

---

# Step 7 — Mouse Events

## Code

    <div
      onMouseEnter={() => console.log("Hover")}
      onMouseLeave={() => console.log("Leave")}
    >
      Hover me
    </div>

---

## Use cases

- Tooltips  
- Hover menus  
- Highlight effects  

---

## Key idea

Mouse events help create interactive UI behavior.

---

# Step 8 — Big Mental Model

## Correct React flow

Events → State → UI

---

## Incorrect approach

Events → Direct DOM manipulation

---

## Explanation

- Events should trigger logic  
- Logic updates state  
- State controls what React renders  

---

# Final Understanding

You should now clearly see:

- Why React event handling is simpler and cleaner  
- Why onClick and similar props are preferred  
- Why React avoids addEventListener in most cases  
- How event handlers are used in real applications  
- How different types of events (click, input, form, keyboard, mouse) work in practice  
