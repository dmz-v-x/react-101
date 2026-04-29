# CSS Modules in React 

---

# 1. Question

Understand EVERYTHING about CSS Modules:

- What problem they solve  
- How they work internally  
- How to use them step-by-step  
- Why they are better than global CSS  
- How bundlers transform them  
- Best practices  

---

# 2. Intuition (Core Idea)

---

## The Problem with Normal CSS

CSS is **global by default**.

---

## Example

	.button {
	  color: red;
	}

---

This affects:

- ALL `.button` classes across the entire app  

---

## Problem in large apps

- Class name conflicts  
- Styles overriding each other  
- Hard to maintain  

---

## Mental Model

Global CSS = Shared global space → collisions  

---

# 3. Solution — CSS Modules

---

CSS Modules make CSS:

- Local  
- Scoped  
- Safe  

---

## Key Idea

Each class is **automatically renamed** to something unique.

---

## Mental Model

Your class → unique generated class  

---

# 4. Basic Example

---

## Component

	function Sidenote({ title, children }) {
	  return (
	    <aside>
	      <h3>{title}</h3>
	      <p>{children}</p>
	    </aside>
	  );
	}

---

## Add CSS Module

---

### Sidenote.module.css

	.wrapper {
	  padding: 16px;
	  background: #eef;
	}

	.title {
	  margin-bottom: 8px;
	}

---

### Sidenote.js

	import styles from "./Sidenote.module.css";

	function Sidenote({ title, children }) {
	  return (
	    <aside className={styles.wrapper}>
	      <h3 className={styles.title}>{title}</h3>
	      <p>{children}</p>
	    </aside>
	  );
	}

---

# 5. What is `styles`?

---

## It is NOT CSS

It is a JavaScript object.

---

## Example

	console.log(styles);

---

## Output

	{
	  wrapper: "_Sidenote_wrapper_abc123",
	  title: "_Sidenote_title_xyz456"
	}

---

## Meaning

- Left side → your class names  
- Right side → generated unique names  

---

# 6. What Actually Happens Behind the Scenes

---

## Step 1 — You write CSS

	.wrapper {
	  padding: 16px;
	}

---

## Step 2 — Bundler processes it

Tools like:

- Vite  
- Webpack  
- Next.js  

---

## Step 3 — Class names get transformed

	.wrapper →

	_components_Sidenote_module__wrapper_7h32k

---

## Step 4 — CSS is injected into DOM

Inside `<head>` like normal CSS.

---

## Step 5 — JS object is created

	{
	  wrapper: "_components_Sidenote_module__wrapper_7h32k"
	}

---

## Step 6 — JSX uses mapped class

	className={styles.wrapper}

---

## Final Output in browser

	class="_components_Sidenote_module__wrapper_7h32k"

---

# 7. Why This Solves Problems

---

## No global conflicts

Every class is unique.

---

## No overrides

Two `.button` classes won’t clash.

---

## No need for BEM

No naming gymnastics needed.

---

# 8. Why Class Names Are Unique

---

Bundlers include:

- File path  
- File name  
- Class name  

---

## Example

	src/components/Sidenote/Sidenote.module.css

---

## Output

	_components_Sidenote_module__wrapper_7h32k

---

## Result

Impossible to collide.

---

# 9. How to Use CSS Modules (Step-by-Step)

---

## Step 1

Create file:

	Component.module.css

---

## Step 2

Write CSS normally

---

## Step 3

Import it

	import styles from "./Component.module.css";

---

## Step 4

Use classes

	className={styles.className}

---

# 10. Naming Flexibility

---

You can rename `styles`:

	import classes from "./Sidenote.module.css";

---

Works the same:

	classes.wrapper

---

# 11. Advantages

---

- Local scoping  
- No collisions  
- Cleaner code  
- Works with plain CSS  
- Easy to learn  
- No extra libraries required  

---

# 12. Comparison with Other Methods

---

## Global CSS

- Simple  
- But unsafe  

---

## BEM

- Structured  
- But verbose and manual  

---

## CSS Modules

- Automatic scoping  
- Clean and scalable  

---

# 13. Best Practices

---

## Keep styles near components

	Button.jsx  
	Button.module.css  

---

## Use descriptive names

	.wrapper  
	.title  
	.buttonPrimary  

---

## Avoid global styles unless necessary

---

## Use composition for reuse

---

# 14. Advanced Concept — Composition (Optional)

---

You can reuse styles:

	.primary {
	  color: blue;
	}

	.button {
	  composes: primary;
	  padding: 10px;
	}

---

# 15. Common Mistakes

---

## Mistake 1 — Forgetting `.module.css`

Wrong:

	styles.css  

Correct:

	styles.module.css  

---

## Mistake 2 — Using string class

Wrong:

	className="wrapper"

---

Correct:

	className={styles.wrapper}

---

## Mistake 3 — Expecting global behavior

CSS Modules are scoped, not global.

---

# 16. When to Use CSS Modules

---

Use when:

- Medium to large apps  
- You want scoped styles  
- You don’t want extra libraries  

---

Avoid when:

- Very small apps  
- You need global theming system  

---

# 17. Final Summary

---

- CSS Modules make CSS local  
- Class names are automatically unique  
- Bundlers transform CSS → JS object  
- You use `styles.className` in JSX  
- No conflicts, no BEM, no headaches  

---

# 18. Final Mental Model

CSS Module = CSS file → transformed → JS object → safe class names  

---

# One-Line Understanding

> CSS Modules turn your CSS into locally scoped, uniquely generated class names, eliminating global conflicts while keeping styling simple and predictable.
