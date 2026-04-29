## Event Handler - Part 1

# Step 1 — What is an Event?

An **event** is something that happens in the browser.

Examples:
- A click
- A key press
- Mouse movement
- Form submission
- Input change
- A network response

### Real-world analogy

An event is like someone ringing your doorbell.

- Doorbell rings → event happens  
- You respond → your code runs  

You can:
- Open the door
- Ignore it
- Ask who it is

### Key idea

Browsers constantly fire events.

These events act as **signals** that your code can listen to and respond to.

---

# Step 2 — Listening for an Event using addEventListener

This is plain DOM JavaScript.

Understanding this is very important before learning React.

### Code

    // 1. Find the element
    const button = document.querySelector('.btn');

    // 2. Create a handler function
    function doSomething(event) {
      console.log('Button clicked!', event);
    }

    // 3. Attach the listener
    button.addEventListener('click', doSomething);

---

## Line-by-line explanation

### 1. Selecting the element

document.querySelector('.btn')

- Finds the first element with class `.btn`
- This is called **DOM lookup**
- Returns:
  - The element if found
  - null if not found

Important:

If the element is null and you try to use addEventListener, your code will crash.

---

### 2. Creating the handler function

function doSomething(event) { ... }

- This function runs when the event occurs
- The browser automatically calls it
- It receives an argument called **event**

The event object contains details like:
- Which element triggered the event
- What type of event it is
- Extra data (like key pressed)

---

### 3. Attaching the event listener

button.addEventListener('click', doSomething)

This tells the browser:

"Whenever this button is clicked, call doSomething."

Important rule:

You pass the function reference:
- Correct: doSomething  
- Wrong: doSomething()  

If you write doSomething(), it runs immediately instead of waiting for the click.

---

## Extra important details

- querySelector returns only the first matching element
- If the DOM is not loaded yet, selection may fail

To avoid this:
- Place script at the bottom of HTML, or
- Use DOMContentLoaded event

---

# Step 3 — The Event Object

When the handler runs, it receives an event object.

### Example

    function doSomething(event) {
      console.log(event.type);      // "click"
      console.log(event.target);    // clicked element
      // event.preventDefault();
    }

---

## Important properties

### event.target

- The exact element that triggered the event

### event.type

- The type of event
- Example: "click", "keydown"

### event.preventDefault()

- Stops default browser behavior

Examples:
- Prevent form submission
- Prevent link navigation

---

### event.stopPropagation()

- Stops the event from moving to parent elements

---

## Event propagation concepts

### Event Bubbling (default behavior)

Event flows upward:

button → parent div → body → document

So if you click a button inside a div:
- Button handler runs
- Then div handler runs
- Then body handler runs

---

### Event Capturing (advanced)

Opposite of bubbling:

document → body → div → button

Rarely used but important conceptually.

---

## event.target vs event.currentTarget

Example:

    button.addEventListener('click', function(event) {
      console.log(event.target);        
      console.log(event.currentTarget); 
    });

- event.target → actual clicked element
- event.currentTarget → element where listener is attached

These can be different in nested elements.

---

# Step 4 — Removing an Event Listener (Cleanup)

When you attach listeners, you should remove them when no longer needed.

### Example

    // attach
    button.addEventListener('click', doSomething);

    // remove
    button.removeEventListener('click', doSomething);

---

## Key rule

removeEventListener works only if you pass the **same function reference**

---

## Common mistake

    button.addEventListener('click', () => console.log('hi'));

You cannot remove this easily because:
- It is an anonymous function
- No reference is stored

---

## Why cleanup is important

If you keep adding listeners without removing them:

- Memory usage increases
- CPU usage increases
- Same function runs multiple times
- Bugs become difficult to debug

---

## Real-world problem

    function setup() {
      button.addEventListener('click', doSomething);
    }

If setup runs multiple times:
- Multiple listeners get added
- One click triggers multiple logs

---

# Step 5 — Event Naming (Important for React Transition)

In plain DOM:

Event names are strings:
- 'click'
- 'keydown'
- 'submit'

---

In React (JSX):

Event names use camelCase:
- onClick
- onKeyDown
- onSubmit

---

## Key difference

DOM:

- You pass a string + function

React:

- You pass a function directly as a prop

---

# Final Mental Model

Think of the system like this:

- Browser = continuously generating events
- Your code = listening system
- addEventListener = registering interest in an event
- Handler function = response logic

---

## Flow

User action → browser creates event → handler executes → response happens

