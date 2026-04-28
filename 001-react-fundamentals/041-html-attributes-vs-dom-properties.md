# HTML Attributes vs DOM Properties (Core Difference)

---

## 1. Core Idea

- **HTML Attributes** = what you write in HTML  
- **DOM Properties** = what exists on the actual DOM element (JavaScript object)  

---

## HTML Attribute

- String-based  
- Written in HTML markup  
- Used initially to create the DOM element  
- Does **not automatically update** when the DOM changes  

---

### Example

	<div id="box" class="red"></div>

---

### Here

- `id="box"` → attribute  
- `class="red"` → attribute  

---

## DOM Property

This is the JavaScript representation of the element.

---

### Example

	const el = document.querySelector("#box");

	console.log(el.id);        // "box"
	console.log(el.className); // "red"

---

### Key points

- These are **properties**, not attributes  
- Properties can change dynamically  
- Properties reflect the **current state** of the element  

---

## 2. Attributes ≠ Properties

### Example

	<input value="John" />

---

### Initial state

- Attribute → `"John"`  
- Property → `"John"`  

---

### After changing via JavaScript

	document.querySelector("input").value = "Sam";

---

### Now

- Property → `"Sam"`  
- Attribute → `"John"` (unchanged)

---

### Key understanding

- Attribute = initial value  
- Property = live value  

---

## 3. Why React Uses DOM Properties

React builds **interactive UIs**, not static HTML.

---

### If React used attributes only

- UI would not update  
- Inputs would not reflect user typing  
- Interactivity would break  

---

### React updates properties like:

	element.className = "...";
	element.value = "...";
	element.id = "...";

---

### Key idea

React works with **live values**, so it uses properties.

---

## 4. `class` vs `className` (Most Important Example)

### HTML

	<div class="box"></div>

---

### JavaScript DOM

There is no:

	element.class

---

### Instead

	element.className

---

### React syntax

	<div className="box"></div>

---

### What React does

	element.className = "box";

---

## 5. Attribute → Property Mapping in React

| HTML Attribute | DOM Property | React Uses  |
|----------------|-------------|-------------|
| class          | className   | className   |
| for            | htmlFor     | htmlFor     |
| tabindex       | tabIndex    | tabIndex    |
| maxlength      | maxLength   | maxLength   |
| readonly       | readOnly    | readOnly    |
| onclick        | onClick     | onClick     |

---

### Key rule

React uses **JavaScript property names**, not HTML attribute names.

---

## 6. Why React Uses Properties

- Properties are live  
- Properties update instantly  
- Reflect current state  
- Follow JavaScript naming  
- Consistent across browsers  
- Avoid HTML inconsistencies  

---

## 7. Real-World Example: Input Value

### HTML

	<input value="default" />

---

### DOM property

	input.value; // "default"

---

### After user types

	input.value; // "Hello"

---

### But attribute remains

	input.getAttribute("value"); // "default"

---

### Key insight

If React updated only attributes:

- UI would not reflect user input  

---

## 8. Final Summary

- HTML attributes initialize elements  
- DOM properties represent live state  
- Attributes and properties are different  
- React updates **properties**, not attributes  
- Therefore React uses:

	- className (not class)  
	- htmlFor (not for)  
	- onClick (not onclick)  

---

## Easy Memory Trick

- Attributes = HTML  
- Properties = JavaScript  

---

## One-Line Understanding

> HTML attributes set initial values, but React updates DOM properties because they represent the live, changing state of the UI.
