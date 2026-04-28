# What Are Components? (Super Simple Explanation)

---

## What is a Component?

React is built around **components**.

A component is:

- A small, self-contained piece of the UI  
- That includes:
  - Markup (HTML-like JSX)  
  - Styles  
  - Logic (JavaScript)  

Everything needed for that part of the interface lives together.

---

## Traditional Web Development (Before React)

Normally, we separate code by type:

- HTML in one place  
- CSS in another  
- JavaScript in another  

---

### Example structure

	index.html     → markup  
	styles.css     → styles  
	script.js      → logic  

---

### Problem with this approach

The code for one feature is split across multiple files, making it harder to:

- Understand  
- Maintain  
- Reuse  

---

## React’s Model: Think in Components

React suggests a different approach:

> Instead of organizing code by file type, organize it by feature.

---

### Instead of this

	button.html  
	button.css  
	button.js  

---

### We create

	Button.jsx  

---

### What goes inside a component

- JSX (markup)  
- CSS (or CSS-in-JS)  
- JavaScript logic  

All bundled together in one place.

---

### Benefit

Everything related to one UI piece lives in a single file, making it:

- Easier to read  
- Easier to maintain  
- Easier to scale  

---

## Reuse: How Components Help

Before React, reuse was handled separately in different layers.

---

### HTML reuse → Partials

Reusable HTML snippets.

---

### CSS reuse → Classes

	.btn {
	  padding: 8px 32px;
	  background: blue;
	}

---

### JavaScript reuse → Functions

	function shout(sentence) {
	  return sentence.toUpperCase() + "!!";
	}

---

### Problem

Each layer had its own reuse system.

---

## React’s Solution: Components

React combines all reuse into a single concept: **components**.

---

### A component bundles

- UI (JSX)  
- Styling  
- Behavior (JavaScript logic)  

---

### Example usage

	<Button label="Save" />

---

### Reusing the same component

	<Button label="Submit" />
	<Button label="Cancel" />

---

### Key idea

- Same component  
- Different data (props)  
- Multiple uses  

---

## Why Components Are Powerful

- Group everything in one place  
- Make code reusable  
- Improve readability  
- Help manage large applications  
- Encourage clean structure  
- Enable building your own UI library  

Examples:

- Buttons  
- Cards  
- Modals  
- Forms  

---

## Final Mental Model

- Think of your UI as a collection of small building blocks  
- Each block = a component  
- Combine components to build larger interfaces  

---

## One-Line Understanding

> A component is a reusable, self-contained piece of UI that includes its structure, style, and behavior in one place.
