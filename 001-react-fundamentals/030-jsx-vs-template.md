# JSX vs Template Languages — Simple Explanation

People sometimes think JSX is similar to template languages like:

- Handlebars (`{{ }}`)  
- EJS  
- Pug (Jade)  

But JSX works very differently.  
Let’s break it down step by step.

---

## 1. What Template Languages Do

Template languages let you write HTML with special syntax embedded inside it.

### Example (Handlebars)

	<div>
	  {{#if user}}
	    <h1>{{user.name}}</h1>
	  {{/if}}
	</div>

---

### What template engines do

Template engines (like Handlebars):

- Take this template  
- Combine it with your data  
- Produce a final HTML string  

---

### Example result

If:

	user.name = "Sujata"

Then output becomes:

	<div><h1>Sujata</h1></div>

---

### Important point

Template languages introduce their own mini-language:

- `{{#if}}`  
- `{{#each}}`  
- Loops  
- Conditional blocks  

You must learn these special rules.

---

## 2. JSX is NOT a Template Language

JSX looks like HTML, but behaves very differently.

---

### Example (JSX)

	<div>
	  {user && <h1>{user.name}</h1>}
	</div>

---

### What JSX becomes

	React.createElement(
	  'div',
	  {},
	  user && React.createElement('h1', {}, user.name)
	);

---

### Key idea

- The condition (`user && ...`) is NOT executed yet  
- JSX only becomes JavaScript  
- React decides what to render **later at runtime**  

---

## 3. Big Difference

### Template languages

- Resolve logic at **compile-time**  
- Combine template + data → final HTML immediately  
- Use custom syntax (`{{#if}}`, `{{#each}}`)  

---

### JSX

- Does NOT resolve logic immediately  
- Converts into JavaScript  
- Logic runs **later during rendering (runtime)**  
- Uses real JavaScript syntax  

---

## 4. Why JSX Is Better (in most cases)

---

### No new language to learn

- No `{{#if}}`, no special syntax  
- You already know JavaScript → you already know JSX logic  

---

### Full JavaScript power

You can use:

- `.map()`  
- `.filter()`  
- `.reduce()`  
- Ternary operators (`? :`)  
- Logical AND (`&&`)  
- Functions  
- Variables  

---

### Compared to template engines

Template engines usually provide limited helpers like:

- `{{#each}}`  
- `{{#if}}`  

---

### JSX is just a thin layer

- Adds HTML-like syntax for readability  
- Everything else is plain JavaScript  

---

## Final Mental Model

- Template languages = HTML + custom syntax → final HTML  
- JSX = HTML-like syntax → JavaScript → React rendering  

---

## One Sentence Summary

> Template languages convert markup into HTML, while JSX converts markup into JavaScript — allowing you to use real JavaScript instead of custom template syntax.
