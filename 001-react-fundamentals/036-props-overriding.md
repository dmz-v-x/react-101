# Props Overriding in React

---

## Basic Rule

Later props override earlier props.

React merges props using standard JavaScript object spread behavior:

	{ ...firstProps, ...secondProps }

If the same key appears multiple times, the **last value wins**.

---

## Basic Prop Overriding Example

	<Component a={1} a={2} />

---

### What React sees

	{ a: 1, a: 2 }

---

### Final result inside component

	{ a: 2 }

---

### Rule

- Duplicate keys → last one overrides earlier ones  

---

## Overriding with Spread Syntax

### Example

	const props1 = { className: "red", id: "box" };
	const props2 = { className: "blue" };

	<Component {...props1} {...props2} />

---

### What React does

	{ ...props1, ...props2 }

---

### Final result

	{
	  className: "blue",
	  id: "box"
	}

---

### Explanation

- `className` from `props2` overrides `props1`  
- `id` remains unchanged  

---

## Overriding with Manual Props

### Example

	<Component {...props} type="button" />

---

### Given

	props = { type: "submit" };

---

### What React does

	{ ...props, type: "button" }

---

### Final result

	{ type: "button" }

---

### Key rule

Manual props written **after spread** override spread values.

---

## Important Order Rule

Order matters:

---

### Case 1 (manual overrides spread)

	<Component {...props} type="button" />

→ `type="button"` wins  

---

### Case 2 (spread overrides manual)

	<Component type="button" {...props} />

→ `props.type` wins  

---

## Overriding Props Passed to DOM Elements

This behavior also applies to native HTML elements.

---

### Example

	const props = { className: "red", id: "box" };

	<div {...props} className="blue" />

---

### Result

	<div class="blue" id="box"></div>

---

### Explanation

- Spread applies first → `className="red"`  
- Manual prop comes later → overrides to `"blue"`  

---

## Another Example (reverse order)

	<div className="blue" {...props} />

---

### Result

	<div class="red" id="box"></div>

---

### Explanation

- Manual prop applied first  
- Spread comes later → overrides  

---

## Real-World Example (Reusable Button)

	function Button({ className, ...rest }) {
	  return (
	    <button
	      className={`btn ${className}`}
	      {...rest}
	    />
	  );
	}

---

### Usage

	<Button className="primary" />

---

### Result

- Combines default + custom class  
- Still allows passing extra props like `onClick`, `disabled`, etc.  

---

## Final Mental Model

- Props merging follows JavaScript object rules  
- Later values override earlier ones  
- Order of props matters  
- Spread = bulk props  
- Manual props = precise overrides  
- Works the same for components and DOM elements  

---

## One-Line Understanding

> In React, props are merged like JavaScript objects, so the last value for a key always overrides earlier ones, and the order of props determines the final result.
