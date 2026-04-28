# What Is the `children` Prop?

---

## Definition

In React, every component can receive a special prop called **`children`**.

**`children` = whatever you put between the opening and closing tags of a component**

---

## Example

	<RedButton>
	  Click me!
	</RedButton>

---

### What happens here

- `"Click me!"` becomes the `children` prop  
- It is passed automatically to the component  

---

## Why Do We Need This?

Let’s build a custom button component.

---

### Using a custom prop (less natural)

	function RedButton({ contents }) {
	  return (
	    <button style={{ color: 'white', backgroundColor: 'red' }}>
	      {contents}
	    </button>
	  );
	}

---

### Usage

	<RedButton contents="Don't click me" />

---

### Problem

This feels different from normal HTML:

	<button>Don't click me</button>

---

## Better Approach: Use `children`

React allows this:

	<RedButton>Don't click me</RedButton>

---

### Updated component

	function RedButton({ children }) {
	  return (
	    <button style={{ color: 'white', backgroundColor: 'red' }}>
	      {children}
	    </button>
	  );
	}

---

### Result

- More natural  
- Matches how HTML works  
- Cleaner API  

---

## How to Access `children`

React automatically passes `children` as a prop.

---

### Example

	function RedButton({ children }) {
	  return <button>{children}</button>;
	}

---

### Key idea

Anything inside:

	<Component> ... </Component>

becomes:

	props.children

---

## What React Does Behind the Scenes

When you write:

	<div>Hello World</div>

---

### React creates

	{
	  type: "div",
	  props: {
	    children: "Hello World"
	  }
	}

---

### Important insight

- `children` is just another prop  
- No special magic  

---

## Alternative Syntax

You can also write:

	<div children="Hello world!" />

---

### Equivalent to

	<div>Hello world!</div>

---

## If Both Forms Are Used — Which Wins?

### Example

	<div children="As an attribute">
	  Between the brackets
	</div>

---

### Result

- Displays: `Between the brackets`  
- Ignores: `children="As an attribute"`  

---

## Why Does Inner Content Win?

React compiles this into:

	React.createElement(
	  'div',
	  { children: "As an attribute" },
	  "Between the brackets"
	);

---

### What React sees

- `children` inside props  
- AND a separate third argument (actual children)  

---

### Rule

React prefers the **third argument** (content between tags).

---

### Reason

- More natural  
- Matches HTML behavior  
- Clearer for developers  

---

## Final Mental Model

- `children` = content inside component tags  
- Automatically passed as a prop  
- Used for layout and composition  
- Preferred over custom props for inner content  
- Inner content overrides `children` attribute  

---

## One-Line Understanding

> The `children` prop is a special prop that represents whatever you place inside a component’s opening and closing tags, making components flexible and composable.
