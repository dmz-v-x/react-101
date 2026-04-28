# Reusable Button Component — Step-by-Step (From Scratch)

---

# STEP 0 — Understand the Problem

You are given:

	<button style={{ color: 'red', borderColor: 'red' }}>Cancel</button>
	<button style={{ color: 'black', borderColor: 'black' }}>Confirm</button>

---

## Observe Carefully (VERY IMPORTANT)

### What is SAME?

- `<button>` element  
- `padding`, `margin`, `borderRadius`  
- `border: '2px solid'`  
- `background: 'white'`  

---

### What is DIFFERENT?

- Text → `"Cancel"` vs `"Confirm"`  
- Color → `'red'` vs `'black'`  

---

## Core Intuition

This is a **classic component extraction problem**.

---

### Mental Model

Instead of repeating:

Extract common part  
Make differences dynamic (using props)

---

# STEP 1 — Identify Dynamic Parts

We replace changing values with variables:

- Text → `children`  
- Color → `color`  

---

# STEP 2 — Create Button Component

	function Button({ color, children }) {
	  return (
	    <button
	      style={{
	        border: '2px solid',
	        color: color,
	        borderColor: color,
	        background: 'white',
	        borderRadius: 4,
	        padding: 16,
	        margin: 8,
	      }}
	    >
	      {children}
	    </button>
	  );
	}

---

## What we did

- Extracted repeated styles  
- Used `color` prop for dynamic styling  
- Used `children` for button text  

---

# STEP 3 — Use the Component

	<Button color="red">Cancel</Button>
	<Button color="black">Confirm</Button>

---

## What happens

- `color="red"` → red button  
- `color="black"` → black button  
- `children` → button text  

---

# STEP 4 — Why Use `children` for Text?

Instead of:

	<Button label="Cancel" />

We use:

	<Button>Cancel</Button>

---

### Reason

- Matches real HTML (`<button>Text</button>`)  
- Cleaner and more natural  

---

# STEP 5 — Improve the Component (Better Pattern)

Instead of passing color directly, we can make it semantic:

---

## Version 2 (Recommended in real apps)

	function Button({ variant, children }) {
	  let color;

	  if (variant === "cancel") {
	    color = "red";
	  } else if (variant === "confirm") {
	    color = "black";
	  }

	  return (
	    <button
	      style={{
	        border: '2px solid',
	        color,
	        borderColor: color,
	        background: 'white',
	        borderRadius: 4,
	        padding: 16,
	        margin: 8,
	      }}
	    >
	      {children}
	    </button>
	  );
	}

---

## Usage

	<Button variant="cancel">Cancel</Button>
	<Button variant="confirm">Confirm</Button>

---

## Why this is better

- More readable  
- Business logic instead of raw colors  
- Easier to scale  

---

# STEP 6 — Concept Breakdown

This exercise teaches:

---

## 1. Component Extraction

Take repeated JSX → convert into component

---

## 2. Props

- `color` / `variant` → controls behavior  
- `children` → controls content  

---

## 3. Reusability

One component → many uses  

---

## 4. DRY Principle

Avoid repeating code  

---

# STEP 7 — Common Mistakes

---

## Mistake 1: Hardcoding values

	function Button() {
	  return <button style={{ color: "red" }}>Cancel</button>; // ❌
	}

---

## Mistake 2: Not using children

	function Button({ label }) {
	  return <button>{label}</button>;
	}

---

## Mistake 3: Duplicating styles again

Avoid repeating styles in each usage.

---

# STEP 8 — Final Mental Model

Whenever you see:

- Same structure  
- Different values  

Extract component  
Replace differences with props  

---

# FINAL ONE-LINE UNDERSTANDING

> A reusable button component is created by extracting shared styles and using props (like color or variant) and children to handle differences.
