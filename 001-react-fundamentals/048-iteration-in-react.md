# Iteration in React 

---

# 1. Question

Understand:

- Why iteration is needed in React  
- Why hardcoding components is not scalable  
- How `.map()` works in React  
- Why `key` is required  
- How to handle lists, objects, nested loops, and conditions  



---

# 2. Intuition (Core Idea)

In real-world apps, data is **dynamic**.

---

## Example Problem

Earlier, we wrote:

	<ContactCard name="Sunita" />
	<ContactCard name="Henderson" />
	<ContactCard name="Aoi" />

---

## Why this fails in real apps

Because:

- One user may have 3 contacts  
- Another may have 100 contacts  
- Another may have 0 contacts  

---

## Key Realization

We **cannot manually write components** for unknown data.

---

## Mental Model

Data → UI

---

# 3. Concept Used

- Iteration  
- JavaScript `.map()`  
- Dynamic rendering  
- Keys for reconciliation  

---

# 4. Step-by-Step Approach

---

## STEP 1 — Store Data in an Array

	const contacts = [
	  { name: "Sunita", job: "Engineer" },
	  { name: "Henderson", job: "Receptionist" },
	  { name: "Aoi", job: "President" }
	];

---

## STEP 2 — Use `.map()`

	contacts.map(contact => {
	  return <ContactCard />;
	});

---

## What `.map()` does

- Takes each item  
- Runs a function  
- Returns a new array  

---

## Result

	[
	  <ContactCard />,
	  <ContactCard />,
	  <ContactCard />
	]

---

## Important

React can render arrays directly.

---

## STEP 3 — Pass Props

	contacts.map(contact => (
	  <ContactCard
	    name={contact.name}
	    job={contact.job}
	  />
	));

---

## STEP 4 — Wrap in JSX

	<ul>
	  {contacts.map(contact => (
	    <ContactCard ... />
	  ))}
	</ul>

---

# 5. The Most Important Rule — `key`

---

## Why key is required

React needs to identify each item uniquely.

---

## Example

	<ContactCard key={contact.id} />

---

## Good keys

- Database ID  
- Email  
- UUID  

---

## Bad keys

### Index

	key={index}

---

### Random

	key={Math.random()}

---

### Non-unique

	key={contact.job}

---

## Why bad keys are dangerous

- Wrong updates  
- Broken animations  
- Lost input state  

---

## Mental Model

Key = identity of each element

---

# 6. Iterating Over Arrays (Most Common)

	<ul>
	  {contacts.map(person => (
	    <li key={person.id}>{person.name}</li>
	  ))}
	</ul>

---

# 7. Iterating Over Objects

---

## Using Object.keys()

	Object.keys(user).map(key => (
	  <li key={key}>
	    {key}: {user[key]}
	  </li>
	));

---

## Using Object.entries()

	Object.entries(user).map(([key, value]) => (
	  <li key={key}>
	    {key}: {value}
	  </li>
	));

---

# 8. Using Fragments in Iteration

---

## Problem

Need multiple elements per item.

---

## Solution

	<dl>
	  {Object.keys(details).map(key => (
	    <React.Fragment key={key}>
	      <dt>{key}</dt>
	      <dd>{details[key]}</dd>
	    </React.Fragment>
	  ))}
	</dl>

---

## Why fragment?

Avoids invalid HTML structure.

---

# 9. Nested Iteration

---

## Example

	contacts.map(contact => (
	  <div key={contact.id}>
	    <h2>{contact.name}</h2>

	    <ul>
	      {contact.tags.map(tag => (
	        <li key={tag}>{tag}</li>
	      ))}
	    </ul>
	  </div>
	));

---

## Concept

.map() inside .map()

---

# 10. Conditional Rendering in Lists

---

## Example

	{contacts.map(contact =>
	  contact.job === "Engineer" ? (
	    <ContactCard key={contact.id} {...contact} />
	  ) : null
	)}

---

## Important

- You can return null  
- React ignores it  

---

# 11. Common Mistakes

---

## Mistake 1 — No return

	contacts.map(contact => {
	  <ContactCard />   // wrong
	});

---

## Fix

	contacts.map(contact => (
	  <ContactCard />
	));

---

## Mistake 2 — Missing key

Always add key.

---

## Mistake 3 — Using index

Avoid unless list is static.

---

# 12. Cleaner Code (Spread Operator)

---

## Instead of

	<ContactCard
	  name={contact.name}
	  job={contact.job}
	  email={contact.email}
	/>

---

## Use

	<ContactCard key={contact.id} {...contact} />

---

## Why better

- Cleaner  
- Less repetition  

---

# 13. Approach (How to Think)

Whenever you see:

---

## Step 1

Do I have a list of data?

---

## Step 2

Use `.map()`  

---

## Step 3

Return JSX for each item  

---

## Step 4

Add key  

---

## Step 5

Handle conditions if needed  

---

# 14. Final Summary

---

## Problem

Cannot hardcode UI for dynamic data.

---

## Solution

Use `.map()`.

---

## Rules

- Always return JSX  
- Always add key  
- Use fragments if needed  
- Avoid index keys  

---

# 15. Final Mental Model

- Data → `.map()` → JSX → UI  

---

# One-Line Understanding

> In React, iteration is done using JavaScript’s `.map()` to convert data arrays into lists of components, with keys used to track each element efficiently.
