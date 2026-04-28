# What is Props Spreading in React?

---

## Definition

Props spreading means passing all properties of an object as props to a component using the spread operator:

	{...object}

---

## Example

	const user = { name: "Sam", age: 20 };

	<UserCard {...user} />

---

### What React does

	<UserCard name="Sam" age={20} />

---

### Key idea

Props spreading = expanding an object into individual props.

---

## How to Achieve Props Spreading

### Basic example

	const props = { title: "Hello", color: "blue" };

	<Component {...props} />

---

### Equivalent to

	<Component title="Hello" color="blue" />

---

## What Happens Under the Hood

This:

	<Component {...props} />

Becomes:

	React.createElement(Component, { ...props });

---

### Important

- No magic  
- No special React behavior  
- Just JavaScript object spreading  

---

## USE CASE 1 — Prop Forwarding

Forward all props from parent to child.

	function Wrapper(props) {
	  return <Child {...props} />;
	}

---

### Without spreading

	<Child title={props.title} color={props.color} size={props.size} />

---

### Problem

- Repetitive  
- Hard to maintain  

---

## USE CASE 2 — Reusable UI Components

	function Button(props) {
	  return <button {...props} className="btn" />;
	}

---

### Usage

	<Button onClick={save} disabled />
	<Button type="submit" id="login-btn" />
	<Button style={{ color: "blue" }} />

---

### Benefit

Your custom component behaves like a native `<button>`.

---

## USE CASE 3 — Combining Props

	const baseStyle = { color: "red", padding: 10 };

	<Component {...baseStyle} fontSize={20} />

---

### Rule

Later props override earlier ones.

- color → red  
- padding → 10  
- fontSize → 20  

---

## USE CASE 4 — API Data

	const user = {
	  name: "Sam",
	  age: 23,
	  location: "USA",
	};

	<UserProfile {...user} />

---

### Cleaner than

	<UserProfile name="Sam" age={23} location="USA" />

---

## USE CASE 5 — Component Composition

	function Card({ children, ...rest }) {
	  return <div className="card" {...rest}>{children}</div>;
	}

---

### Usage

	<Card id="main-card" data-theme="dark">
	  Hello World
	</Card>

---

### Meaning

- `children` → content inside component  
- `...rest` → all other props  

---

# Question

	const children = 'Hello World'
	const className = 'container'
	const props = { children, className }

	const element = <div /> 

### How do we apply props to this `<div>`?

---

## Answer

Use props spreading directly on the element:

	const element = <div {...props} />;

---

## What this becomes

	<div className="container">
	  Hello World
	</div>

---

## Explanation

- `className` → applied as an attribute  
- `children` → becomes inner content  

---

## Important Concept

In JSX:

- `children` is treated specially  
- It becomes the content inside the element  

---

## Equivalent manual version

	const element = (
	  <div className={props.className}>
	    {props.children}
	  </div>
	);

---

## Final Mental Model

- `{...props}` spreads all key-value pairs  
- `children` becomes inner content  
- Other keys become attributes  
- Order matters (later props override earlier ones)  

---

## One-Line Understanding

> Props spreading lets you pass an entire object as props, and when used on a DOM element, it applies attributes and renders `children` automatically.
