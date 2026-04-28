# JSX “GOTCHAS” CHEAT SHEET

---

## 1. JSX Needs One Parent Element

### Wrong

	<div>Hello</div>
	<p>World</p>

---

### Correct

	<>
	  <div>Hello</div>
	  <p>World</p>
	</>

---

## 2. `{}` Means “JavaScript Goes Here”

### Valid

	<p>{5 + 5}</p>
	<p>{username}</p>
	<p>{items.length}</p>

---

### NOT valid

	<p>{ if (true) return 5 }</p> // statements NOT allowed

---

### Rule

Only **expressions** work inside `{}`.

---

## 3. The Whitespace Problem

JSX ignores indentation whitespace.

---

### Missing space

	<strong>Hello:</strong>
	{count}

---

### Output

	Hello:3

---

### Fix (add real space)

	<strong>Hello:</strong>{' '}{count}

---

## 4. `class` → `className`, `for` → `htmlFor`

### Wrong

	<div class="box"></div>
	<label for="name"></label>

---

### Correct

	<div className="box"></div>
	<label htmlFor="name"></label>

---

### Why?

These are reserved JavaScript words.

---

## 5. All Attributes Are camelCase

HTML attributes become camelCase in JSX.

| HTML             | JSX             |
|------------------|-----------------|
| onclick          | onClick         |
| tabindex         | tabIndex        |
| autoplay         | autoPlay        |
| stroke-dasharray | strokeDasharray |

---

### Wrong

	<video autoplay></video>

---

### Correct

	<video autoPlay></video>

---

## 6. Data and ARIA Attributes Keep Their Dashes

These are exceptions (no camelCase).

### Example

	<button
	  data-test-id="close-btn"
	  aria-label="Close"
	>

---

## 7. All Tags Must Be Closed

HTML is loose — JSX is strict.

---

### Wrong

	<p>Hello

---

### Correct

	<p>Hello</p>

---

### Self-closing tags

	<img src="cat.jpg" />
	<br />
	<hr />
	<input />

---

## 8. JSX is Case-Sensitive

### Wrong

	<MAIN>
	  <HEADER>

---

### Correct

	<main>
	  <header>

---

### Important

Uppercase tags are treated as **React components**, not HTML elements.

---

## 9. Inline Styles Must Use an Object

### Wrong

	<h1 style="color: red;">Hi</h1>

---

### Correct

	<h1 style={{ color: 'red' }}>Hi</h1>

---

### Rule

CSS properties → camelCase

- `background-color` → `backgroundColor`  
- `font-size` → `fontSize`  

---

## 10. Boolean Attributes

### Both work

	<input required />
	<input required={true} />

---

### Recommended

	<input required={true} />

---

## 11. Statements vs Expressions

JSX allows expressions, not statements.

---

### Wrong

	{if (loggedIn) return <p>Hello</p>}

---

### Correct

	{loggedIn ? <p>Hello</p> : null}

---

## 12. Keys Required for Lists

### Wrong

	{items.map(item => <li>{item}</li>)}

---

### Correct

	{items.map(item => <li key={item.id}>{item.name}</li>)}

---

### Why?

Keys help React efficiently track list changes.

---

## 13. Comments Inside JSX

### Wrong

	<div>
	  // this doesn't work
	</div>

---

### Correct

	<div>
	  {/* this works */}
	</div>

---

## 14. JSX Does Not Support All HTML Attributes Directly

Some HTML attributes are renamed in JSX.

| HTML Attribute  | JSX Equivalent  |
|-----------------|-----------------|
| maxlength       | maxLength       |
| readonly        | readOnly        |
| contenteditable | contentEditable |
| accept-charset  | acceptCharset   |

---

## 15. JSX Ignores `null`, `undefined`, `false`

These render nothing:

	{null}
	{undefined}
	{false}

---

### Useful for conditional rendering

	{isAdmin && <AdminPanel />}

---

## Final Mental Model

- JSX looks like HTML but follows JavaScript rules  
- `{}` = JavaScript expressions only  
- JSX is strict (closing tags, casing, attributes)  
- Some HTML attributes are renamed  
- Whitespace is not automatically preserved  
- Lists require keys  
- `null`, `undefined`, `false` render nothing  

---

## One-Line Summary

> JSX is HTML-like syntax powered by JavaScript rules, so understanding expressions, strict syntax, and attribute differences is key to avoiding common pitfalls.
