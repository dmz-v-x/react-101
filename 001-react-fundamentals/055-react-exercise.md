# React Exercises — Iteration + Keys

---

# Exercise 1 — Avatar Selection

---

# 1. Question

You are given multiple `<Avatar />` components written manually:

	<Avatar src="001.png" />
	<Avatar src="002.png" />
	<Avatar src="003.png" />
	<Avatar src="004.png" />

---

## Problem

- Repetitive code  
- Not dynamic  
- Hard to maintain  
- Violates DRY (Don’t Repeat Yourself)

---

# 2. Intuition

Whenever you see:

- Repeated components  
- Same structure with different data  

---

## Think

"Can I move data into an array and use `.map()`?"

---

## Mental Model

Data → `.map()` → Components

---

# 3. Approach

---

## Step 1 — Create data array

Each avatar needs:

- id  
- alt text  

---

## Code

	const data = [
	  { id: "001", alt: "person with curly hair and a black T-shirt" },
	  { id: "002", alt: "person wearing a hijab and glasses" },
	  { id: "003", alt: "person with short hair wearing a blue hoodie" },
	  { id: "004", alt: "person with a pink mohawk and a raised eyebrow" }
	];

---

## Step 2 — Use `.map()`

Convert data → components

---

## Code

	{data.map(({ id, alt }) => (
	  <Avatar
	    key={id}
	    src={`https://sandpack-bundler.vercel.app/img/avatars/${id}.png`}
	    alt={alt}
	  />
	))}

---

## What’s happening

- Looping through array  
- Creating `<Avatar />` for each item  
- Passing props dynamically  
- Assigning `key={id}`  

---

# 4. Final Answer

	function App() {
	  return (
	    <div className="avatar-set">
	      {data.map(({ id, alt }) => (
	        <Avatar
	          key={id}
	          src={`https://sandpack-bundler.vercel.app/img/avatars/${id}.png`}
	          alt={alt}
	        />
	      ))}
	    </div>
	  );
	}

---

# 5. Important Rule — Keys

---

## Why not index?

- Changes when array changes  
- Causes wrong UI updates  

---

## Rule

- Use stable unique value  
- `key={id}` is correct  

---

---

# Exercise 2 — Shopping Cart

---

# 1. Question

You have an array of items:

Each item has:

- id  
- title  
- price  
- image  
- inStock (true/false)  

---

## Tasks

1. Separate items into:

   - in-stock  
   - out-of-stock  

2. Render two `<CartTable />` components  

3. Inside `<CartTable />`, use `.map()`  

4. Add `key={id}` correctly  

---

# 2. Intuition

---

## Problem breakdown

- One array → split into two groups  
- Each group → render separately  
- Each group → loop using `.map()`  

---

## Mental Model

Data → filter → map → UI

---

# 3. Approach

---

## Step 1 — Split data

	const inStockItems = items.filter(item => item.inStock);
	const outOfStockItems = items.filter(item => !item.inStock);

---

## Step 2 — Render two tables

	<h2>Shopping cart</h2>
	<CartTable items={inStockItems} />

	<h2>Sold out</h2>
	<CartTable items={outOfStockItems} />

---

## Step 3 — Use `.map()` inside component

---

## Code

	function CartTable({ items }) {
	  return (
	    <table className="shopping-cart">
	      <thead>
	        <tr>
	          <th></th>
	          <th>Title</th>
	          <th>Price</th>
	        </tr>
	      </thead>

	      <tbody>
	        {items.map(({ id, imageSrc, imageAlt, title, price }) => (
	          <tr key={id} className="cart-row">
	            <td>
	              <img
	                src={imageSrc}
	                alt={imageAlt}
	                className="product-thumb"
	              />
	            </td>
	            <td>{title}</td>
	            <td>${price}</td>
	          </tr>
	        ))}
	      </tbody>
	    </table>
	  );
	}

---

# 4. Key Observations

---

## Correct key placement

	key={id} → on `<tr>`

---

## Why?

- `<tr>` is the top-level element returned by `.map()`  

---

## Clean code practice

- Use destructuring  
- Avoid repetition  
- Keep components reusable  

---

# 5. Final Summary

---

## Exercise 1

- Move repeated JSX → array  
- Use `.map()`  
- Add `key={id}`  

---

## Exercise 2

- Split data using `.filter()`  
- Render multiple components  
- Use `.map()` inside component  
- Place keys correctly  

---

# 6. Final Mental Model

---

## Universal Pattern

Array → transform (filter/map) → JSX → UI

---

# One-Line Understanding

> In React, repeated UI should always come from data arrays, using `.map()` and proper keys to create clean, scalable, and dynamic components.
