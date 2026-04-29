# Rendering Lists in React Using `.map()`

---

# 1. Question

You have an array of data, and you want:

- One React component per item  
- Without manually writing each component  

Example goal:

3 contacts → 3 `<ContactCard />`

---

# 2. Intuition (Core Idea)

In many frameworks:

- Vue → `v-for`  
- Angular → `*ngFor`  
- Handlebars → `{{#each}}`  

---

## React is different

React does NOT provide special looping syntax.

Instead:

- You use **normal JavaScript**
- Specifically: `.map()`

---

## Mental Model

Data → `.map()` → JSX → UI

---

# 3. Step 1 — The Data

	const data = [
	  {
	    id: 'sunita-abc123',
	    name: 'Sunita Kumar',
	    job: 'Electrical Engineer',
	    email: 'sunita.kumar@acme.co'
	  },
	  {
	    id: 'henderson-def456',
	    name: 'Henderson G. Sterling II',
	    job: 'Receptionist',
	    email: 'henderson-the-second@acme.co'
	  },
	  {
	    id: 'aio-ghi789',
	    name: 'Aoi Kobayashi',
	    job: 'President',
	    email: 'kobayashi.aoi@acme.co'
	  },
	];

---

## Key understanding

This is just a **normal JavaScript array**.

Nothing React-specific.

---

# 4. Step 2 — Desired Output

We want:

	<ul>
	  <ContactCard />
	  <ContactCard />
	  <ContactCard />
	</ul>

---

## Problem

We do NOT want to write components manually.

---

# 5. Step 3 — Using `.map()`

---

## Core Code

	<ul>
	  {data.map(contact => (
	    <ContactCard
	      name={contact.name}
	      job={contact.job}
	      email={contact.email}
	    />
	  ))}
	</ul>

---

## What `.map()` does

- Loops over array  
- Returns a new array  
- Each item becomes JSX  

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

# 6. The Most Common Mistake

---

## Wrong

	{data.map(contact => {
	  <ContactCard name={contact.name} />
	})}

---

## Why wrong?

- `{}` means function body  
- You MUST use `return`  

---

## Fix

	{data.map(contact => {
	  return <ContactCard name={contact.name} />;
	})}

---

## Better (preferred)

	{data.map(contact => (
	  <ContactCard name={contact.name} />
	))}

---

## Rule

- `()` → implicit return  
- `{}` → explicit return required  

---

# 7. Step 4 — JSX inside JavaScript inside JSX

---

## Example

	<ul>
	  {data.map(contact => (
	    <ContactCard name={contact.name} />
	  ))}
	</ul>

---

## Structure

- JSX (`<ul>`)  
- Inside → JavaScript (`map`)  
- Inside that → JSX (`<ContactCard />`)  

---

## Key insight

JSX is just JavaScript.

---

# 8. Step 5 — What React Compiles This Into

---

## Your JSX

	<ul>
	  {data.map(contact => (
	    <ContactCard name={contact.name} />
	  ))}
	</ul>

---

## Becomes

	React.createElement(
	  "ul",
	  {},
	  data.map(contact =>
	    React.createElement(ContactCard, {
	      name: contact.name
	    })
	  )
	);

---

## Key understanding

Everything becomes JavaScript.

---

# 9. Final Correct Version

---

	function App() {
	  return (
	    <ul>
	      {data.map(contact => (
	        <ContactCard
	          key={contact.id}
	          name={contact.name}
	          job={contact.job}
	          email={contact.email}
	        />
	      ))}
	    </ul>
	  );
	}

---

## Important addition

	key={contact.id}

This helps React track elements efficiently.

---

# 10. Approach (How to Think)

---

## Step 1

Do I have an array?

---

## Step 2

Use `.map()`

---

## Step 3

Return JSX for each item

---

## Step 4

Add `key`

---

## Step 5

Render inside JSX using `{}`

---

# 11. Final Summary

---

- React does NOT have special loop syntax  
- Use JavaScript `.map()`  
- `{}` allows JavaScript inside JSX  
- `.map()` must return JSX  
- React can render arrays of JSX  
- JSX compiles to `React.createElement()`  

---

# 12. Final Mental Model

Array → `.map()` → JSX array → Rendered UI

---

# One-Line Understanding

> In React, you use JavaScript’s `.map()` to convert arrays of data into arrays of components, which React then renders directly.
