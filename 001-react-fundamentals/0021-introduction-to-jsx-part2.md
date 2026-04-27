# Understanding JSX

---

## The old way of creating React elements

Before JSX, you had to create elements using plain JavaScript:

	const element = React.createElement(
	  'p',
	  { id: 'hello' },
	  'Hello World!'
	);

This works… but it becomes very hard to read when your UI gets bigger.

---

## The new way: JSX

React developers almost always use JSX, which looks like HTML but actually runs inside JavaScript.

Here’s the same example using JSX:

	const element = (
	  <p id="hello">
	    Hello World!
	  </p>
	);

Much cleaner and easier to read.

---

## Why JSX is better (the main reason)

React UIs are often nested, just like HTML:

	<nav>
	  <ul>
	    <li><a>Home</a></li>
	    <li><a>Archives</a></li>
	  </ul>
	</nav>

---

### Writing this without JSX (hard to read)

	const element = React.createElement(
	  "nav",
	  { id: "main-nav" },
	  React.createElement(
	    "ul",
	    null,
	    React.createElement(
	      "li",
	      null,
	      React.createElement("a", { href: "/" }, "Home")
	    ),
	    React.createElement(
	      "li",
	      null,
	      React.createElement("a", { href: "/archives" }, "Archives")
	    )
	  )
	);

This is very hard to read.

---

### Same UI using JSX (clean and readable)

	const element = (
	  <nav id="main-nav">
	    <ul>
	      <li>
	        <a href="/">Home</a>
	      </li>
	      <li>
	        <a href="/archives">Archives</a>
	      </li>
	    </ul>
	  </nav>
	);

Way more readable, right?  
This is why almost everyone uses JSX.

---

## Why do we wrap JSX in parentheses?

	const element = (
	  <p>Hello World</p>
	);

### Key idea

The parentheses are not required, but they:

- Make the code easier to read  
- Allow JSX to start on a new line  
- Prevent JavaScript from getting confused  

---

### Without parentheses

	const element = <p>Hello World</p>;

This is valid, but once you add multiple lines, it becomes messy.

---

### Why parentheses help

They improve formatting and make multi-line JSX predictable.

You can even use this pattern without JSX:

	const message = (
	  "This is perfectly valid JavaScript!"
	);

---

## JSX must be compiled into normal JavaScript (important!)

Browsers do not understand JSX.

---

### Example (this will fail in the browser)

	const element = <p>Hello World</p>;

---

### What happens behind the scenes?

A tool like **Babel** converts your JSX into plain JavaScript.

---

### Example transformation

#### What you write

	<p>Hello</p>

#### What Babel turns it into

	React.createElement("p", null, "Hello");

---

### Important takeaway

By the time your code runs in the browser:

- All JSX is gone  
- Only JavaScript remains  
- JSX is just a developer-friendly syntax  

---

## “Transpile” vs “Compile” — do we care?

Technically:

### Compile

- Convert into machine code  
- Example: C → machine code  

---

### Transpile

- Convert into another human-readable language  
- Example: JSX → JavaScript  

---

### In React

- JSX → JS = transpilation  
- Done using tools like Babel  

---

## Do files need to end in `.jsx`?

### Old days (React 0–14)

If a file had JSX, it had to be:

	Something.jsx

---

### Today

You can write JSX in a `.js` file:

	index.js  
	App.js  
	Header.js  

---

### Why this works

Modern build tools assume:

> Any JavaScript file might contain JSX.

Tools like:

- Vite  
- Webpack  
- Parcel  

handle this automatically.

---

### Developer preference

- Some prefer `.jsx` for clarity  
- Others use `.js` for simplicity  

Both are correct.

---

## Do we need to import React?

### Example code

	import React from 'react';
	import { createRoot } from 'react-dom/client';

	const element = (
	  <p id="hello">Hello World</p>
	);

---

### Common question

“We never used the React variable… so can we delete that line?”

---

## Older React (before React 17)

You **had to import React** because JSX was converted into:

	React.createElement(...)

If you didn’t import it, you would get:

	Error: React is not defined

---

## Modern React (React 17+)

Today, JSX is transformed differently.

---

### Example transformation

#### JSX

	<p>Hello</p>

#### Transformed version

	import { jsx as _jsx } from 'react/jsx-runtime';

	const element = _jsx("p", { children: "Hello" });

---

### Key change

- React is automatically handled  
- No need to manually import React  

---

## So should you still import React?

Technically, you don’t need to.

But many developers still do because:

- Old habit  
- Useful when using React Hooks  
- Keeps compatibility with older setups  

---

## Final Understanding

- JSX is a syntax that looks like HTML but runs in JavaScript  
- It improves readability and developer experience  
- It gets converted into plain JavaScript before execution  
- Modern tools handle everything automatically  
- Importing React is optional in modern React, but still common in practice  

---

## One-Line Mental Model

> JSX is a readable way to describe UI, which gets transformed into normal JavaScript before the browser runs it.
