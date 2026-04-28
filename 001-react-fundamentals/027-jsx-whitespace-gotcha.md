# The JSX Whitespace Gotcha

---

## The Problem

Sometimes in JSX, things that look like they have spaces… don’t actually have spaces when shown on the page.

### Example

	const daysUntilSantaReturns = 123;

	const element = (
	  <div>
	    <strong>Days until Santa returns:</strong>
	    {daysUntilSantaReturns}
	  </div>
	);

---

### What you expect

	Days until Santa returns: 123

---

### What you actually get

	Days until Santa returns:123

---

### Issue

The space between the colon `:` and the number disappears.

---

## Why does this happen?

### Key idea

JSX does **NOT** compile to HTML.  
JSX compiles to **JavaScript**.

---

### What JSX becomes

	const element = React.createElement(
	  'div',
	  {},
	  React.createElement(
	    'strong',
	    {},
	    'Days until Santa returns:'
	  ),
	  daysUntilSantaReturns
	);

---

### What’s happening here?

The `<div>` has **two children**:

1. A `<strong>` element  
2. A text node (`123`)  

---

### Important detail

There is **no space node** between them.

---

### Final output becomes

	<strong>Days until Santa returns:</strong>123

---

### Conclusion

- JSX indentation is ignored  
- No automatic space is inserted  
- So the missing space is expected  

---

## How to fix it: Add a "space node"

React provides a simple solution.

---

### Add a space manually using `{ ' ' }`

	<div>
	  <strong>Days until Santa returns:</strong>
	  {' '}
	  {daysUntilSantaReturns}
	</div>

---

### What this compiles to

	React.createElement(
	  'div',
	  {},
	  React.createElement('strong', {}, 'Days until Santa returns:'),
	  ' ',     // ← explicit space node
	  daysUntilSantaReturns
	);

---

### Final result

	Days until Santa returns: 123

---

## Why doesn’t React automatically keep spaces?

Whitespace on the web serves **two different purposes**.

---

### 1. Real visible spaces

Example:

	Hello world

Here, the space between words is meaningful.

---

### 2. Formatting / indentation

Example:

	<div>
	  <p>Hello</p>
	</div>

This spacing is only for code readability, not UI.

---

## HTML vs JSX behavior

### HTML

- Treats whitespace (spaces, tabs, newlines) the same  
- Collapses them into a single visible space  

---

### JSX

- Ignores whitespace between elements  
- Does not treat indentation as meaningful  

---

### Why JSX behaves this way

Because in modern layouts (like Flexbox):

- Whitespace should not affect layout  
- Extra spaces could cause inconsistent rendering  

---

## Key takeaway

React requires you to explicitly define:

> “This space is real and should be rendered.”

---

### How?

Using:

	{' '}

---

## Real-World Example: Images in a Row

### HTML behavior

	<img /> <img /> <img />

Even with newlines:

	<img />
	<img />
	<img />

Browsers will show small gaps between images.

---

### But with Flexbox

- Whitespace is ignored  
- Layout is controlled by CSS  

---

### Conclusion

Different systems treat whitespace differently.  
JSX chooses consistency by ignoring indentation.

---

## Prettier handles this automatically

Prettier (code formatter) understands this JSX behavior.

---

### What it does

- Automatically inserts `{ ' ' }` where needed  
- Prevents spacing bugs  
- Keeps code clean and consistent  

---

## Final Summary (Mental Model)

- JSX ignores indentation whitespace  
- No automatic space between elements  
- JSX compiles into JavaScript nodes  
- If you need a space → you must add it explicitly  
- `{ ' ' }` creates a real space node  
- Formatting spaces ≠ rendered spaces  

---

## One-Line Understanding

> JSX ignores formatting spaces, so if you need a visible space in the UI, you must explicitly add it using `{ ' ' }`.
