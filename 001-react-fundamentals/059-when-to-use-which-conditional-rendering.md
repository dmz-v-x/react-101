# Conditional Rendering — When to Use `&&` vs Ternary + Common Mistakes

---

# 1. Question

Understand:

- When to use `&&` vs `?:`  
- Common mistakes beginners make  
- How React treats different values during rendering  

---

# 2. Intuition (Core Idea)

In React, conditional rendering means:

- Show something based on a condition  
- Sometimes show nothing  
- Sometimes choose between two things  

---

## Two main tools

- `&&` → show or hide  
- `?:` → choose between two options  

---

## Mental Model

- One output → `&&`  
- Two outputs → `?:`  

---

# 3. When to Use `&&`

---

## Rule

Show something OR nothing.

---

## Example

	{isOnline && <GreenDot />}

---

## Meaning

- true → show `<GreenDot />`  
- false → show nothing  

---

## Use `&&` when

- You only need to show something conditionally  
- No "else" UI needed  

---

## Common use cases

- Badges  
- Icons  
- Optional messages  
- Buttons  
- Loading indicators  

---

# 4. When to Use Ternary (`?:`)

---

## Rule

Choose between two things.

---

## Example

	{isLoggedIn 
	  ? <Dashboard /> 
	  : <LoginMessage />
	}

---

## Meaning

- true → show Dashboard  
- false → show LoginMessage  

---

## Use ternary when

- You need both true and false cases  
- You want to toggle UI  

---

## Common use cases

- Login vs logout  
- Active vs inactive  
- Premium vs free  
- Switching layouts  

---

# 5. Quick Decision Table

---

| Goal                                  | Use      |
|---------------------------------------|----------|
| Show something only if true           | `&&`     |
| Show A if true, B if false            | `?:`     |
| Toggle between two components         | `?:`     |
| No "else" UI needed                   | `&&`     |

---

# 6. Common Mistakes

---

## Mistake 1 — Using `if` inside JSX

---

### Wrong

	{ if (isOnline) { <Dot /> } }

---

### Why

- `if` is a statement  
- JSX only accepts expressions  

---

## Fix

Use:

- `&&`  
- ternary  
- or move `if` outside JSX  

---

## Mistake 2 — Missing return in `.map()`

---

### Wrong

	items.map(item => {
	  <ItemCard item={item} />
	})

---

### Problem

- `{}` means function body  
- No `return` → nothing renders  

---

### Fix 1

	items.map(item => {
	  return <ItemCard item={item} />
	})

---

### Fix 2 (preferred)

	items.map(item => (
	  <ItemCard item={item} />
	))

---

## Mistake 3 — Using `0 && ...`

---

### Wrong

	{items.length && <ShoppingList />}

---

### Problem

- If `length = 0` → React renders `0`  

---

### Fix

	{items.length > 0 && <ShoppingList />}

---

### OR

	{!!items.length && <ShoppingList />}

---

## Mistake 4 — Wrong key placement

---

### Wrong

	{items.map(item => (
	  <li>
	    <Card key={item.id} />
	  </li>
	))}

---

### Correct

	{items.map(item => (
	  <li key={item.id}>
	    <Card />
	  </li>
	))}

---

## Rule

Key must be on the top-level element returned by `.map()`.

---

## Mistake 5 — Using index as key

---

### Wrong

	{items.map((item, index) => (
	  <Item key={index} />
	))}

---

### Problem

- Changes when list order changes  
- Causes bugs  

---

### Correct

	<Item key={item.id} />

---

## Mistake 6 — Using statements inside `{}`

---

### Wrong

	{if (isLoggedIn) { <Dashboard /> }}

---

### Rule

JSX allows only expressions.

---

# 7. How React Treats Values

---

## React IGNORES

- false  
- null  
- undefined  
- "" (empty string)  

---

## Example

	<div>{false}</div>

---

## Output

	<div></div>

---

# 8. Values React DOES NOT Ignore

---

- 0  
- NaN  
- non-empty strings  

---

## Example

	<div>{0}</div>

---

## Output

	<div>0</div>

---

# 9. Why This Matters

---

## Example

	{items.length && <ShoppingList />}

---

## If length = 0

- React renders `0`  

---

## Fix

Always convert to boolean.

---

# 10. Memory Trick

---

## To hide something, use:

- false  
- null  
- undefined  
- ""  

---

## Avoid passing:

- 0  
- NaN  

---

# 11. Approach (How to Think)

---

## Step 1

Do you need one or two outcomes?

---

## Step 2

- One → use `&&`  
- Two → use `?:`  

---

## Step 3

Ensure condition is boolean  

---

## Step 4

Avoid common mistakes  

---

# 12. Final Summary

---

- `&&` → show or hide  
- `?:` → choose between two options  
- JSX only accepts expressions  
- React ignores false/null/undefined  
- React DOES render 0 and NaN  

---

# 13. Final Mental Model

Condition → expression → JSX → rendered UI  

---

# One-Line Understanding

> Use `&&` to conditionally show something and `?:` to switch between two UI states, while ensuring your conditions are valid expressions that React can render correctly.
