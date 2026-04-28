# What Are Props?

---

## The Problem Without Props

So far, components like this:

	<FriendlyGreeting />

always show the same thing every time.

That’s not very useful.

---

## What Are Props?

Props make components flexible.

**Props = data you pass into a component**

They are similar to **function arguments**.

---

## Example

	<FriendlyGreeting name="Josh" />

Here, `"Josh"` is a prop.

---

## How to Use Props in a Component

Props are received as a function parameter.

---

### Basic version

	function FriendlyGreeting(props) {
	  return <p>Greetings, {props.name}!</p>
	}

---

### Cleaner version (destructuring — very common)

	function FriendlyGreeting({ name }) {
	  return <p>Greetings, {name}!</p>
	}

---

### What is destructuring?

- Extract values from an object  
- Makes code cleaner and shorter  

---

## How React Handles Props Internally

When you write:

	<FriendlyGreeting name="Josh" />

React converts it into:

	React.createElement(FriendlyGreeting, { name: "Josh" });

---

### What this means

React is simply passing an object:

	{ name: "Josh" }

into your component function.

---

### So this works

	function FriendlyGreeting(props) {
	  console.log(props.name);
	}

---

### Key idea

- Props are just plain JavaScript objects  
- No magic involved  

---

## Example: Rendering Multiple Components

	root.render(
	  <div>
	    <FriendlyGreeting name="Josh" />
	    <FriendlyGreeting name="Anita" />
	    <FriendlyGreeting name="Rahul" />
	  </div>
	);

---

### What happens

Each component receives a different `name` prop:

- Josh  
- Anita  
- Rahul  

---

## Default Props (Fallback Values)

What if no prop is provided?

---

### Example

	<FriendlyGreeting />

Without handling, this would show:

	Greetings, undefined!

---

## Best Practice: Default Values (Destructuring)

	function FriendlyGreeting({ name = "there" }) {
	  return <p>Hey {name}!</p>;
	}

---

### Results

- `<FriendlyGreeting name="Josh" />` → `Hey Josh!`  
- `<FriendlyGreeting />` → `Hey there!`  

---

### Why this is best

- All defaults defined in one place  
- No repeated logic  
- Avoids bugs with falsy values  
- Clean and readable  

---

## Alternative Fallback Methods (Not Preferred)

---

### 1. Using `||` (OR operator)

	<p>Hey {name || "there"}!</p>

---

### Problem

Treats all falsy values as missing:

- `""` → becomes `"there"`  
- `0` → becomes `"there"`  
- `false` → becomes `"there"`  

This can lead to unexpected behavior.

---

## 2. Using `??` (Nullish Coalescing)

	<p>Hey {name ?? "there"}!</p>

---

### Behavior

Falls back only when:

- `null`  
- `undefined`  

---

### Better than `||`, but still not preferred

---

## Final Mental Model

- Props = inputs to a component  
- Passed like HTML attributes  
- Received as an object  
- Used to make components reusable and dynamic  
- Default values should be handled via destructuring  

---

## One-Line Understanding

> Props are inputs passed to React components, allowing the same component to display different data based on what you provide.
