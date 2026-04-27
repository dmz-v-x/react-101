# How JSX Works in React — A Step-by-Step, Beginner-Friendly Explanation

---

## 1. Rendering elements without JSX (the old way)
### Using `React.createElement`

	const element = React.createElement(
	    'p',
	    { id: 'hello' },
	    'Hello World!'
	);

This works, but it becomes hard to read as soon as your UI becomes more complex.

### Example: Nested UI (hard to read)

	const element = React.createElement(
	    'div',
	    null,
	    React.createElement('h1', null, 'Hello'),
	    React.createElement('p', null, 'This is hard to read!')
	);

### Problem with this approach

- Deep nesting becomes difficult to understand  
- Code readability drops quickly  
- Harder to maintain and debug  
- Not intuitive for developers familiar with HTML  

This is why developers rarely write React like this today.

---

## 2. JSX — A cleaner and more readable way to write UI

React provides a special syntax called **JSX**.

### What is JSX?

- Looks like HTML  
- Written inside JavaScript  
- Makes UI code easier to read and write  

### Same example written using JSX

	const element = (
	    <p id="hello">
	        Hello World!
	    </p>
	);

Much cleaner and more intuitive.

---

### Rendering JSX to the DOM

	const container = document.querySelector('#root');
	const root = createRoot(container);
	root.render(element);

---

### Why JSX is better

- Looks like HTML → easier to read  
- Works naturally with nested UI  
- Reduces chances of mistakes  
- Matches how developers mentally think about UI  
- Standard approach in modern React apps  

---

### Example of JSX nesting

	const element = (
	    <div>
	        <h1>Hello</h1>
	        <p>This is much easier to read than React.createElement.</p>
	    </div>
	);

---

## Why do we wrap JSX in parentheses?

	const element = (
	    <p>Hello World</p>
	);

### Key idea

Parentheses are **optional** — React does not require them.

This is also valid:

	const element = <p>Hello World</p>;

---

### Then why use parentheses?

When JSX spans multiple lines, parentheses:

- Improve readability  
- Clearly define where JSX starts and ends  
- Prevent common formatting mistakes  

---

### Without parentheses

	const element =
	    <p>Hello World</p>;

This is harder to read and more error-prone.

---

### Conclusion

Parentheses are used for:

- Code clarity  
- Better formatting  
- Developer readability  

They are **not required for functionality**.

---

## Why we need to "compile" JSX

### Key idea

Browsers **do NOT understand JSX**.

---

### Example (this will break in the browser)

	const element = <p>Hello World</p>;

### Why?

Because browsers only understand:

- Plain JavaScript  
- Not HTML inside JavaScript  

---

## So how does JSX actually work?

A tool called **Babel** converts JSX into normal JavaScript **before it reaches the browser**.

---

### Example transformation

#### What you write (JSX)

	const element = <p id="hello">Hello World</p>;

#### What Babel converts it into

	const element = React.createElement(
	    'p',
	    { id: 'hello' },
	    'Hello World'
	);

---

### Important takeaway

When your code runs in the browser:

- All JSX is already removed  
- Only JavaScript remains  
- Specifically: `React.createElement` calls  

---

## "Transpiled" vs "Compiled" — Is there a difference?

Yes, technically.

### Compiling

- Converts one language into another completely different form  
- Example:  
  - C → Machine Code  

---

### Transpiling

- Converts between similar languages or versions  
- Example:  
  - Modern JavaScript → Older JavaScript  
  - JSX → JavaScript  

---

### In React context

- JSX → JavaScript = **Transpilation**  
- Done by tools like Babel  

---

## Do we need the `.jsx` file extension?

### Old React rule

If your file contained JSX, you had to name it:

	Something.jsx

---

### Why was this required?

Because tools needed to know:

> "This file contains JSX — convert it before running."

---

## Modern React rule

You can now write JSX in normal `.js` files:

	index.js  
	App.js  
	Header.js  

---

### Why this works today

Modern build tools automatically handle JSX:

- Vite  
- Webpack  
- Parcel  

They assume:

> "Any `.js` file might contain JSX — just compile it."

---

## So what should you use?

Both are valid:

	index.js  
	index.jsx  

---

### What most developers do

- Use `.js` for everything  
- Keep things simple  
- Rely on tooling to handle JSX  

---

## Final Summary (Mental Model)

- JSX is **just syntax sugar**  
- It looks like HTML but is actually JavaScript under the hood  
- Babel converts JSX → `React.createElement`  
- Browsers only see JavaScript, never JSX  
- Parentheses in JSX are for readability, not functionality  
- `.jsx` extension is optional in modern setups  

---

## One-Line Understanding

> JSX is a developer-friendly way to write UI, which gets converted into plain JavaScript before the browser runs it.
