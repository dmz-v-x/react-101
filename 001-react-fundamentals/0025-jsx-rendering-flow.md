# JSX Rendering Flow — From Code to Screen

Below is an easy-to-understand diagram showing the entire journey:

---

## YOUR CODE (JSX)

	const element = (
	  <div id="hello">
	    Hello {name}
	  </div>
	);

---

### What this means

- You write UI using JSX (HTML-like syntax inside JavaScript)  
- `{name}` is a JavaScript expression (interpolation)  

---

## Babel compiles JSX

JSX cannot run in the browser directly, so it gets converted into plain JavaScript.

---

## JS CODE (`React.createElement`)

	const element = React.createElement(
	  "div",
	  { id: "hello" },
	  "Hello ",
	  name
	);

---

### What changed here?

- JSX → function calls  
- `<div>` → `"div"`  
- Attributes → JavaScript object  
- Children → separate arguments  

---

## Runs in the browser

Now this is valid JavaScript, so the browser can execute it.

---

## VIRTUAL DOM OBJECT

	{
	  type: "div",
	  props: {
	    id: "hello",
	    children: ["Hello ", name]
	  }
	}

---

### What is this?

- A plain JavaScript object  
- Represents your UI structure  
- Lightweight and fast to work with  

---

## React reconciles changes

React compares:

- Previous Virtual DOM  
- New Virtual DOM  

This process is called **reconciliation**.

---

## REAL DOM (What you see on the screen)

	<div id="hello">
	  Hello Sarah
	</div>

---

### Final result

- React updates the actual DOM efficiently  
- Only the necessary parts are changed  
- UI gets updated on the screen  

---

# Full Mental Model (Step-by-Step)

1. You write JSX  
2. Babel converts JSX → `React.createElement`  
3. JavaScript runs in the browser  
4. React creates a Virtual DOM object  
5. React compares changes (reconciliation)  
6. React updates the Real DOM  
7. You see the UI on screen  

---

## One-Line Understanding

> JSX is transformed into JavaScript, which creates a Virtual DOM that React uses to efficiently update the real UI in the browser.
