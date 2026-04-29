# Showing vs Hiding in React

---

# 1. Question

Understand:

- The two ways to show/hide UI in React  
- When to use conditional rendering  
- When to use CSS-based hiding  
- Performance and practical trade-offs  

---

# 2. Intuition (Core Idea)

When you want to control visibility, you have two strategies:

1. Remove the element entirely  
2. Keep the element but hide it visually  

---

## Mental Model

- Conditional rendering → element may not exist  
- CSS hiding → element exists but is invisible  

---

# 3. Method 1 — Conditional Rendering (Add/Remove)

---

## Example

	{isOnline && <div className="green-dot" />}

---

## What happens

- `isOnline = true` → element is created and rendered  
- `isOnline = false` → element is not created at all  

---

## Result

- Clean DOM  
- No extra nodes  

---

## Key Idea

Element **does not exist** when condition is false.

---

# 4. Method 2 — CSS-Based Hiding

---

## Example

	function Friend({ name, isOnline }) {
	  const style = isOnline ? undefined : { display: "none" };

	  return (
	    <li>
	      <div className="green-dot" style={style} />
	      {name}
	    </li>
	  );
	}

---

## What happens

- `isOnline = true` → visible  
- `isOnline = false` → hidden via CSS  

---

## Result

- Element is still in DOM  
- Only visibility changes  

---

## Key Idea

Element **always exists**, just hidden.

---

# 5. Comparison

---

| Aspect                | Conditional Rendering        | CSS Hiding (`display: none`) |
|----------------------|-----------------------------|------------------------------|
| DOM presence         | Removed                     | Still present                |
| Memory usage         | Lower                       | Higher                       |
| Toggle performance   | Slightly slower             | Faster                       |
| Code clarity         | Cleaner                     | Slightly more complex        |

---

# 6. Which One Should You Use?

---

## Default choice

Use **conditional rendering**.

---

## Why

- Cleaner DOM  
- Less memory usage  
- Simpler logic  
- Matches React philosophy  

---

# 7. When to Use CSS Hiding

---

Use CSS hiding when:

- Visibility changes very frequently  
- You need smooth transitions/animations  
- You want to avoid re-creating DOM nodes  

---

## Examples

- Dropdown menus  
- Accordions  
- Tooltips  
- Modals with animations  

---

# 8. Performance Insight

---

## Conditional Rendering

- Removes and adds DOM nodes  
- Slight overhead on frequent toggles  

---

## CSS Hiding

- Keeps DOM intact  
- Only updates styles  
- Faster for rapid toggling  

---

# 9. Practical Guidance

---

## Use Conditional Rendering when:

- Element is rarely toggled  
- You want clean structure  
- You want React to manage lifecycle  

---

## Use CSS Hiding when:

- Element toggles frequently  
- You need animation  
- You care about micro-performance  

---

# 10. Approach (How to Decide)

---

## Step 1

Will this element toggle frequently?

- No → use conditional rendering  
- Yes → consider CSS  

---

## Step 2

Do you need animations?

- Yes → CSS hiding  

---

## Step 3

Do you want clean DOM?

- Yes → conditional rendering  

---

# 11. Final Summary

---

- Conditional rendering removes elements entirely  
- CSS hiding keeps elements but hides them  
- Conditional rendering is preferred in most cases  
- CSS hiding is useful for frequent toggles and animations  

---

# 12. Final Mental Model

Render or not render → React decision  
Hide or show → CSS decision  

---

# One-Line Understanding

> In React, use conditional rendering to remove elements from the DOM by default, and use CSS hiding only when you need faster toggling or smooth visual transitions.
