# React Reconciliation Algorithm 

---

# 1. Question

Understand:

- What is reconciliation in React  
- How React updates the DOM efficiently  
- Why keys are critical for reconciliation  
- What goes wrong without keys  

---

# 2. Intuition (Core Idea)

Whenever your app changes:

- State updates  
- Props change  

React must update the UI.

---

## But React does NOT rebuild everything

Instead:

1. Re-runs your components  
2. Creates a new **virtual DOM**  
3. Compares it with the old one  
4. Updates only what changed  

---

## This process is called

**Reconciliation**

---

## Mental Model

Old UI → New UI → Compare → Update minimal parts

---

# 3. What is Virtual DOM (Quick Understanding)

React does not directly work with the browser DOM.

It creates a JavaScript object like:

	{
	  type: "div",
	  props: {
	    children: [...]
	  }
	}

---

Then it compares:

- Old virtual DOM  
- New virtual DOM  

---

# 4. The Core Problem React Solves

---

## Example

Old UI:

	Asha  
	Rohan  
	Meera  

New UI:

	Asha  
	Rohan  

---

## React must figure out:

- Which items stayed  
- Which were removed  
- Which changed  
- Which moved  

---

## This is like

"Spot the difference"

---

# 5. Without Keys (Problem)

---

## Example

Old list:

	["A", "B", "C"]

New list:

	["B", "C"]

---

## What React does (by index)

| Old | New | Match |
|-----|-----|-------|
| A   | B   | wrong |
| B   | C   | wrong |
| C   | —   | removed |

---

## React thinks

- A → became B  
- B → became C  
- C → removed  

---

## Result

- Wrong updates  
- UI bugs  
- Broken state  

---

# 6. With Keys (Solution)

---

## Old

	A (id 1)  
	B (id 2)  
	C (id 3)  

---

## New

	B (id 2)  
	C (id 3)  

---

## React compares by key

| Key | Old | New | Action     |
|-----|-----|-----|------------|
| 1   | yes | no  | remove     |
| 2   | yes | yes | reuse node |
| 3   | yes | yes | reuse node |

---

## Result

- Correct updates  
- No confusion  

---

# 7. Real-World Bug Example (Inputs)

---

## Code

	{items.map((item, index) => (
	  <input key={index} defaultValue={item.name} />
	))}

---

## Problem

Remove first item.

---

## What happens

| Index | Old Value | New Value |
|-------|----------|----------|
| 0     | Alice    | Bob      |
| 1     | Bob      | Charlie  |
| 2     | Charlie  | removed  |

---

## Result

Inputs shift incorrectly.

---

## Root Cause

Using index as key.

---

# 8. What React Does Internally

---

## Step 1 — Old list

	[{ key: 1 }, { key: 2 }, { key: 3 }]

---

## Step 2 — New list

	[{ key: 2 }, { key: 3 }]

---

## Step 3 — Match by key

React builds mapping:

| Key | Old? | New? | Action     |
|-----|------|------|------------|
| 1   | yes  | no   | remove     |
| 2   | yes  | yes  | reuse node |
| 3   | yes  | yes  | reuse node |

---

# 9. Why Keys Matter for Performance

---

## Without keys

- React guesses  
- More DOM updates  
- Slower  

---

## With keys

- Direct matching  
- Minimal updates  
- Faster  

---

## Complexity

- With keys → O(n)  
- Without keys → worse (more comparisons)

---

# 10. Why Keys Matter for State

---

## Example

Each list item may have:

- Input value  
- Focus  
- Animation  

---

## With correct keys

- State stays attached to correct item  

---

## Without keys

- State shifts incorrectly  

---

# 11. What Makes a Good Key

---

## Good keys

- Database ID  
- UUID  
- Email (if unique)  
- Slug  

---

## Properties

- Unique among siblings  
- Stable across renders  

---

# 12. Bad Keys

---

## Index

	key={index}

---

## Problem

Changes when list order changes.

---

## Random values

	key={Math.random()}

---

## Problem

Changes every render.

---

## Non-unique values

	key={item.name}

---

## Problem

Duplicates cause bugs.

---

# 13. Approach (How to Think)

---

## Step 1

Are you rendering a list?

---

## Step 2

Assign unique key to each item  

---

## Step 3

Ensure key is stable  

---

## Step 4

Never use index unless list is static  

---

# 14. Final Summary

---

- Reconciliation = React’s diffing algorithm  
- React compares old vs new UI  
- Without keys → React guesses  
- With keys → React matches correctly  
- Keys improve performance and correctness  

---

# 15. Final Mental Model

Keys = identity → identity enables correct diffing → correct diffing enables efficient updates

---

# One-Line Understanding

> React uses keys during reconciliation to match elements between renders, ensuring correct updates, better performance, and stable component state.
