# React Keys

---

# 1. Question

Understand:

- Why React needs `key` when rendering lists  
- What problem keys solve  
- What happens without keys  
- What should be used as a key  
- Common mistakes and best practices  

---

# 2. Intuition (Core Idea)

When React renders a list:

	{data.map(item => <Component />)}

React must track:

- Which item stayed  
- Which item was removed  
- Which item moved  
- Which item is new  

---

## Why this matters

React does NOT rebuild the whole UI.

It updates only what changed.

---

## Problem

Without keys:

React cannot identify items correctly.

---

## Mental Model

Key = identity of each item

---

# 3. Real-Life Analogy

Imagine students sitting in a classroom:

| Seat | Student |
|------|--------|
| 1    | Asha   |
| 2    | Rohan  |
| 3    | Meera  |

---

If Meera leaves:

- Without IDs → confusion  
- With IDs → clear removal  

---

## Key = Student ID

---

# 4. Step-by-Step Example

---

## Data

	const data = [
	  { id: 'sunita', name: 'Sunita' },
	  { id: 'henderson', name: 'Henderson' },
	  { id: 'aoi', name: 'Aoi' }
	];

---

## Rendering list

	<ul>
	  {data.map(contact => (
	    <ContactCard
	      key={contact.id}
	      name={contact.name}
	    />
	  ))}
	</ul>

---

## What React sees internally

	[
	  { key: 'sunita' },
	  { key: 'henderson' },
	  { key: 'aoi' }
	]

---

## Now React can track each item correctly

---

# 5. What Happens WITHOUT Keys

React may:

- Reuse wrong components  
- Mix up items  
- Lose input values  
- Break animations  
- Cause flickering  

---

## Key idea

Without keys → React guesses

---

# 6. What Should You Use as a Key

---

## Good keys

- Database ID  
- UUID  
- Email (if unique)  
- Username  

---

## Example

	key={contact.id}

---

## Rules

- Must be unique among siblings  
- Must be stable (same across renders)  

---

# 7. What NOT to Use

---

## Index

	key={index}

---

### Why bad

- Changes when list order changes  
- Causes incorrect updates  

---

## Random values

	key={Math.random()}

---

### Why bad

- Changes every render  
- React loses tracking completely  

---

## Non-unique values

	key={contact.job}

---

### Why bad

- Duplicate keys  
- React confusion  

---

# 8. Important Rule — Where to Put Key

---

## Wrong

	{items.map(item => (
	  <li>
	    <span key={item.id}>{item.name}</span>
	  </li>
	))}

---

## Why wrong

Key must be on the **top-level element returned by `.map()`**

---

## Correct

	{items.map(item => (
	  <li key={item.id}>
	    <span>{item.name}</span>
	  </li>
	))}

---

# 9. Keys with Fragments

---

## Problem

Short syntax `<> </>` cannot take key

---

## Correct

	{items.map(item => (
	  <React.Fragment key={item.id}>
	    <dt>{item.name}</dt>
	    <dd>{item.value}</dd>
	  </React.Fragment>
	))}

---

# 10. Important Concept — Key is NOT a Prop

---

## Example

	function ContactCard({ key, name }) {
	  console.log(key);
	}

---

## Output

	undefined

---

## Why?

React removes `key` before passing props.

---

## Internal structure

	{
	  type: ContactCard,
	  key: "sunita",
	  props: {
	    name: "Sunita"
	  }
	}

---

## Key insight

- `key` is used by React  
- Not accessible inside component  

---

# 11. Best Practices

---

- Use stable unique ID  
- Keep keys consistent  
- Avoid index unless list is static  
- Put key on top-level element  
- Ensure uniqueness within list  

---

# 12. Approach (How to Think)

---

## Step 1

Are you rendering a list?

---

## Step 2

Use `.map()`

---

## Step 3

Add `key`

---

## Step 4

Ensure key is stable and unique  

---

# 13. Final Summary

---

- Keys help React track elements  
- Required when rendering lists  
- Must be unique among siblings  
- Must be stable across renders  
- Not passed as props  

---

# 14. Final Mental Model

List → `.map()` → JSX → keys → React tracks efficiently

---

# One-Line Understanding

> Keys give identity to elements in a list, allowing React to efficiently update only the parts of the UI that actually change.
