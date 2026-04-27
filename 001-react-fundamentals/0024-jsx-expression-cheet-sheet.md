# JSX Expressions Cheat Sheet

---

## JSX Basics

JSX looks like HTML but runs inside JavaScript.

	const element = <h1>Hello</h1>;

---

## JSX must return one parent element

### Not allowed

	<div></div>
	<p></p>

---

### Allowed (using Fragment)

	<>
	  <div></div>
	  <p></p>
	</>

---

## Use `{}` to insert JavaScript

	<p>{5 + 5}</p>
	<p>{username}</p>
	<p>{items.length}</p>

---

## No strings needed

	<p>{'Hello'}</p> // Works, but not needed unless building dynamic strings

---

## COMMENTS IN JSX

### Correct way

	<div>
	  {/* This is a JSX comment */}
	</div>

---

### Wrong way

	// breaks JSX
	<div>// not allowed</div>

---

## ATTRIBUTES

### Static attributes (strings)

	<input id="search-box" />

---

### Dynamic attributes (JavaScript)

	<input id={userId} />

---

### Multi-value expressions

	<input id={user.email.replace('@', '-')} />

---

## BOOLEAN ATTRIBUTES

### These are the same

	<input required />
	<input required={true} />

---

### Recommended for clarity

	<input required={true} />

---

## NUMBER ATTRIBUTES

Both are valid:

	<input min="5" />
	<input min={5} />

---

## STYLES IN JSX

Inline styles use a JavaScript object:

	<div style={{ color: "red", fontSize: "20px" }}>
	  Hello
	</div>

---

## CLASS NAMES

JSX uses `className` instead of `class`:

	<div className="box"></div>

---

## CONDITIONAL RENDERING (VERY COMMON)

### Using ternary operator

	{isLoggedIn ? <p>Welcome!</p> : <p>Please log in</p>}

---

### Using logical AND (`&&`)

	{items.length > 0 && <p>You have items!</p>}

---

## LOOPS (Using `.map()`)

	<ul>
	  {items.map(item => (
	    <li key={item.id}>{item.name}</li>
	  ))}
	</ul>

---

## Final Quick Mental Model

- JSX = HTML-like syntax inside JavaScript  
- `{}` = run JavaScript expressions  
- Must return a single parent element  
- Use `.map()` for lists  
- Use ternary or `&&` for conditions  
- Use `className` instead of `class`  
- Styles are JavaScript objects  
- Attributes can be dynamic using `{}`  

---

## One-Line Summary

> JSX lets you write UI in a readable way while embedding JavaScript expressions directly inside it.
