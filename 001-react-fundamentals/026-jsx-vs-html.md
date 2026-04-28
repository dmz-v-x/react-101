# JSX vs HTML

JSX looks like HTML, but it is **not HTML**.  
Because JSX eventually becomes JavaScript, it has some important differences.

Don’t worry about memorizing everything — React provides helpful warnings.

---

## 1. Reserved Words (Very Important)

JavaScript has keywords that cannot be used as variable names or JSX attributes.

### Example

	const while = 10; // ❌ Error: “while” is a reserved word

---

### HTML vs JSX

In HTML:

	<label for="name">Name:</label>
	<input class="fun-input" />

This is valid in HTML.

---

### Problem in JSX

- `for` is a reserved JavaScript keyword  
- `class` is also a reserved JavaScript keyword  

---

### JSX Alternatives

| HTML    | JSX         |
|---------|------------|
| class   | className  |
| for     | htmlFor    |

---

### Correct JSX version

	<label htmlFor="name">Name:</label>
	<input id="name" className="fun-input" />

---

## 2. Self-Closing Tags

HTML is forgiving:

	<p>This is fine
	<p>No closing tag

---

### JSX is strict

Every tag must be properly closed.

### Not allowed in JSX

	<p>Hello

---

### Correct JSX

	<p>Hello</p>

---

### Self-closing tags

Some tags don’t have children (like `<img>`).

#### HTML

	<img src="cat.jpg">

#### JSX

	<img src="cat.jpg" />

---

## 3. Case-Sensitive Tags

HTML does not care about case:

	<H1>HELLO</H1>

---

### JSX is case-sensitive

Tags must be lowercase (for HTML elements).

### Correct JSX

	<h1>Hello</h1>

---

## 4. Case-Sensitive Attributes (camelCase)

HTML attributes are lowercase:

	<video autoplay></video>

---

### JSX uses camelCase

	<video autoPlay={true}></video>

---

### React warning example

Warning: Invalid DOM property `autoplay`. Did you mean `autoPlay`?

---

### Common conversions

| HTML             | JSX             |
|------------------|-----------------|
| onclick          | onClick         |
| tabindex         | tabIndex        |
| stroke-dasharray | strokeDasharray |

---

## 5. Data and ARIA Attributes (Special Case)

These **do NOT use camelCase**.  
They keep their hyphenated format.

### Example

	<button
	  data-test-id="submit-btn"
	  aria-label="Close"
	>
	  Click Me
	</button>

---

### Used for

- Accessibility (ARIA attributes)  
- Testing (data attributes)  

---

## 6. Inline Styles

### HTML version

	<h1 style="font-size: 2rem;">Hi</h1>

---

### JSX version (uses JavaScript object)

	<h1 style={{ fontSize: "2rem" }}>Hi</h1>

---

### Why two sets of `{}`?

Example:

	<h1 style={{
	  fontSize: '2rem',
	  color: 'red'
	}}>
	  Hi
	</h1>

---

### Explanation

- Outer `{}` → tells JSX “this is JavaScript”  
- Inner `{}` → is the actual JavaScript object  

---

### Quick rules

- CSS properties → camelCase  
  - `background-color` → `backgroundColor`  
  - `border-bottom-color` → `borderBottomColor`  

---

### Units behavior

- Numbers often become `px` automatically  
  - `width: 200` → `"200px"`  
  - `paddingTop: 8` → `"8px"`  

---

### Important exception

Some CSS properties are **unitless**:

	lineHeight: 20   // means 20 (not 20px)

---

## 7. Boolean Attributes

### HTML

	<input required>

---

### JSX supports both

	<input required />
	<input required={true} />

---

### Recommended (clearer)

	<input required={true} />

---

## Final Summary (Mental Model)

- JSX is JavaScript, not HTML  
- Some HTML attributes are renamed (`className`, `htmlFor`)  
- JSX is strict about closing tags  
- JSX is case-sensitive  
- Attributes use camelCase  
- Styles are JavaScript objects  
- Data and ARIA attributes keep hyphens  
- Boolean attributes should be explicit for clarity  

---

## One-Line Understanding

> JSX looks like HTML, but follows JavaScript rules, which is why syntax differences like `className`, camelCase attributes, and strict tag closing exist.
