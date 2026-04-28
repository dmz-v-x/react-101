# What are Default Props?

---

## Definition

Default props are **fallback values for props**.

They are used when a parent does **NOT pass a prop**.

---

## Simple Analogy (Very Important)

### Normal JavaScript function

	function greet(name = "Guest") {
	  console.log(name);
	}

	greet();        // "Guest"
	greet("Sam");   // "Sam"

---

### Same idea in React

Default props work exactly like default function parameters.

---

## Why Do We Need Default Props?

Because components should be:

- Reusable  
- Safe  
- Predictable  
- Not break when props are missing  

---

## Without Default Props

	function Button({ label }) {
	  return <button>{label}</button>;
	}

	<Button />   // label = undefined

---

### Problem

- UI becomes empty or broken  

---

## With Default Props

	function Button({ label = "Click me" }) {
	  return <button>{label}</button>;
	}

---

### Result

- Works even if `label` is not passed  

---

## Modern Way (Recommended)

Use **default parameters**:

	function Button({ label = "Click me" }) {
	  return <button>{label}</button>;
	}

---

### Why this is best

- Clean  
- Standard JavaScript  
- Works with TypeScript  
- Future-proof  

---

## Legacy Way (Avoid)

	function Button({ label }) {
	  return <button>{label}</button>;
	}

	Button.defaultProps = {
	  label: "Click me",
	};

---

### Notes

- Legacy approach  
- Not recommended for new code  
- May be removed for function components  

---

## How Default Props Work

React does not modify your component.

It simply ensures:

	if (props.label === undefined) {
	  label = "Click me"
	}

---

## Very Important Rule

Default props apply **only when value is `undefined`**

---

### Example

	function Text({ value = "Default" }) {
	  return <p>{value}</p>;
	}

---

### Behavior

	<Text />                      // "Default"
	<Text value={undefined} />   // "Default"
	<Text value={null} />        // null (NOT default)
	<Text value="" />            // "" (NOT default)
	<Text value={0} />           // 0 (NOT default)

---

### Key idea

Only `undefined` triggers default.

---

## Default Props with Multiple Props

	function Card({
	  title = "Untitled",
	  price = 0,
	  currency = "USD",
	}) {
	  return (
	    <div>
	      <h2>{title}</h2>
	      <p>{price} {currency}</p>
	    </div>
	  );
	}

---

### Usage

	<Card />
	<Card title="Book" />
	<Card title="Pen" price={10} />

---

### Result

All combinations work safely.

---

## Default Props with `children`

	function Box({ children = "No content" }) {
	  return <div>{children}</div>;
	}

---

### Usage

	<Box />              // "No content"
	<Box>Hello</Box>     // "Hello"

---

## Default Props with Objects (Careful)

### Problem

	function User({ user = { name: "Guest" } }) {
	  return <p>{user.name}</p>;
	}

- Creates a new object on every render  

---

### Better approach

	const defaultUser = { name: "Guest" };

	function User({ user = defaultUser }) {
	  return <p>{user.name}</p>;
	}

---

## Default Props with Functions

	function Button({ onClick = () => {} }) {
	  return <button onClick={onClick}>Click</button>;
	}

---

### Why?

Prevents errors when `onClick` is missing.

---

## Default Props + Rest Props

	function Input({
	  type = "text",
	  disabled = false,
	  ...rest
	}) {
	  return <input type={type} disabled={disabled} {...rest} />;
	}

---

### Common pattern in real apps

---

## When Should You Use Default Props?

- When a prop is optional  
- When component should not break  
- When missing props would affect UI  
- In reusable components  
- In UI libraries  

---

## When NOT to Use Default Props

- When prop is required  
- When missing value is a bug  
- When value must come from API or state  

---

## Required Props Example

	function Avatar({ src }) {
	  if (!src) {
	    throw new Error("Avatar src is required");
	  }
	  return <img src={src} />;
	}

---

### Why no default?

Because missing `src` is a real error.

---

## Real-World Examples

---

### Button

	function Button({ variant = "primary", disabled = false }) {
	  return <button disabled={disabled}>{variant}</button>;
	}

---

### Alert

	function Alert({ type = "info", message = "Something happened" }) {
	  return <div className={`alert-${type}`}>{message}</div>;
	}

---

### Modal

	function Modal({ isOpen = false }) {
	  if (!isOpen) return null;
	  return <div>Modal</div>;
	}

---

## Final Summary

- Default props = fallback values  
- Applied only when value is `undefined`  
- Use default parameters (`{ prop = value }`)  
- Avoid `Component.defaultProps` in new code  
- Helps build safe and reusable components  

---

## Final Mental Model

- Props come from parents  
- Defaults protect components  
- `undefined` → default applies  
- Any other value → default ignored  

---

## One-Line Understanding

> Default props provide fallback values for missing props, ensuring components remain safe, predictable, and reusable.
