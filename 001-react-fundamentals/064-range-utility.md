# Range Utility Exercise 

---

# 1. Question

You are given a component:

	function StarRating({ rating }) {
	  return (
	    <div className="star-wrapper">
	      
	    </div>
	  );
	}

---

## Goal

Render **n number of stars** based on the `rating` prop.

---

## Example

If:

	rating = 4

Then UI should show:

⭐ ⭐ ⭐ ⭐

---

# 2. Intuition (Core Idea)

---

## Problem

We want to repeat the same JSX element multiple times.

---

## Normally in JavaScript

We would use:

- `for` loop  

---

## But in React

- JSX does NOT allow statements like `for`  
- JSX only allows **expressions**  

---

## Key Idea

We need to:

1. Create an array  
2. Convert that array into JSX  
3. Render it  

---

## Mental Model

Number → Array → .map() → JSX  

---

# 3. Approach (Step-by-Step)

---

## Step 1 — Create a list of numbers

We need something like:

	[0, 1, 2, 3]  // for rating = 4

---

## Step 2 — Convert each item into a star

Use `.map()`:

	array.map(() => <img />)

---

## Step 3 — Render inside JSX

React can render arrays directly.

---

# 4. Solution 1 — Using for loop (basic)

---

	function StarRating({ rating }) {
	  let stars = [];

	  for (let i = 0; i < rating; i++) {
	    stars.push(
	      <img
	        key={i}
	        alt=""
	        className="gold-star"
	        src="https://sandpack-bundler.vercel.app/img/gold-star.svg"
	      />
	    );
	  }

	  return <div className="star-wrapper">{stars}</div>;
	}

---

## What’s happening

- Loop runs `rating` times  
- Each iteration adds a star  
- React renders array  

---

# 5. Solution 2 — Using range() (Recommended)

---

## Step 1 — Create range function

	const range = (start, end, step = 1) => {
	  let output = [];

	  if (typeof end === "undefined") {
	    end = start;
	    start = 0;
	  }

	  for (let i = start; i < end; i += step) {
	    output.push(i);
	  }

	  return output;
	};

---

## Step 2 — Use it in component

	function StarRating({ rating }) {
	  return (
	    <div className="star-wrapper">
	      {range(rating).map((num) => (
	        <img
	          key={num}
	          alt=""
	          className="gold-star"
	          src="https://sandpack-bundler.vercel.app/img/gold-star.svg"
	        />
	      ))}
	    </div>
	  );
	}

---

## Why this is better

- Cleaner  
- Reusable  
- Works inside JSX  
- More flexible  

---

# 6. How range() Works

---

## Example

	range(5)

---

## Output

	[0, 1, 2, 3, 4]

---

## Explanation

- Starts from 0  
- Stops before 5  
- Creates array  

---

# 7. Alternative Solution (Built-in JS)

---

	function StarRating({ rating }) {
	  return (
	    <div className="star-wrapper">
	      {Array(rating).fill().map((_, index) => (
	        <img
	          key={index}
	          alt=""
	          className="gold-star"
	          src="https://sandpack-bundler.vercel.app/img/gold-star.svg"
	        />
	      ))}
	    </div>
	  );
	}

---

## Why not preferred

- Harder to read  
- Less flexible  
- Feels hacky  

---

# 8. Key Concepts Used

---

- JSX rendering  
- Arrays in React  
- `.map()`  
- Keys in lists  
- Utility functions  

---

# 9. Important Rule (Keys)

---

Each element must have a unique key:

	key={num}

---

## Why

- Helps React track elements  
- Improves performance  
- Prevents bugs  

---

# 10. Approach (How to Think)

---

## Step 1

Do you need repetition?

---

## Step 2

Convert number → array  

---

## Step 3

Use `.map()`  

---

## Step 4

Return JSX  

---

# 11. Final Summary

---

- JSX cannot use loops directly  
- Use arrays + `.map()`  
- `range()` is a clean helper  
- React renders arrays automatically  

---

# 12. Final Mental Model

Number → Generate array → Map → Render  

---

# One-Line Understanding

> To repeat UI elements in React, convert numbers into arrays and use `.map()` to generate JSX dynamically.
