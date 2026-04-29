# Rendering Collections with Keys in Complex Structures

---

# 1. Question

Understand how to correctly use **keys** in complex list scenarios:

- Nested lists  
- Fragments  
- Multiple `.map()` calls  
- Lists inside tables  
- Lists inside components  
- Combining `.map()` with conditions  

---

# 2. Intuition (Core Idea)

You already know:

	items.map(item => (
	  <Item key={item.id} />
	))

---

## What changes now?

Real-world UI is not flat.

You will have:

- Lists inside lists  
- Multiple lists in one component  
- Fragments instead of elements  
- Conditional rendering  

---

## Mental Model

Each **list** needs its own identity system.

---

# 3. PART 1 — Nested Lists

---

## Question

What if each item has its own list?

---

## Example Data

	const contacts = [
	  {
	    id: "1",
	    name: "Asha",
	    phones: ["999-111", "888-222"]
	  },
	  {
	    id: "2",
	    name: "Rohan",
	    phones: ["777-123"]
	  }
	];

---

## Approach

- Outer list → key for each contact  
- Inner list → key for each phone  

---

## Answer

	<ul>
	  {contacts.map(contact => (
	    <li key={contact.id}>
	      <h3>{contact.name}</h3>

	      <ul>
	        {contact.phones.map(phone => (
	          <li key={phone}>{phone}</li>
	        ))}
	      </ul>

	    </li>
	  ))}
	</ul>

---

## Rule

Each `.map()` needs its own keys.

---

# 4. PART 2 — Fragments with Keys

---

## Problem

Fragments (`<> </>`) cannot accept keys.

---

## Wrong

	data.map(item => (
	  <>
	    <p>{item.title}</p>
	    <p>{item.subtitle}</p>
	  </>
	))

---

## Approach

Use full fragment syntax.

---

## Answer

	data.map(item => (
	  <React.Fragment key={item.id}>
	    <p>{item.title}</p>
	    <p>{item.subtitle}</p>
	  </React.Fragment>
	))

---

# 5. PART 3 — Multiple Lists in Same Component

---

## Question

Do keys need to be unique across all lists?

---

## Example

	<div>
	  {users.map(u => <User key={u.id} {...u} />)}

	  {products.map(p => <Product key={p.id} {...p} />)}
	</div>

---

## Answer

Keys only need to be unique **within each list**.

---

## Rule

Each `.map()` is its own list.

---

# 6. PART 4 — `.map()` Syntax Mistakes

---

## Wrong

	{items.map(item => {
	  <li>{item}</li>
	})}

---

## Problem

- No return → renders nothing  

---

## Fix 1

	{items.map(item => {
	  return <li key={item.id}>{item.name}</li>;
	})}

---

## Fix 2 (Preferred)

	{items.map(item => (
	  <li key={item.id}>{item.name}</li>
	))}

---

# 7. PART 5 — `.map()` + Conditional Rendering

---

## Question

Render only active users.

---

## Approach

Filter first, then map.

---

## Answer

	<ul>
	  {users
	    .filter(user => user.active)
	    .map(user => (
	      <User key={user.id} {...user} />
	    ))
	  }
	</ul>

---

# 8. PART 6 — Mapping Inside Components

---

## Question

How to render object data inside a component?

---

## Example

	function ContactCard({ name, details }) {
	  return (
	    <div>
	      <h2>{name}</h2>

	      <dl>
	        {Object.entries(details).map(([key, value]) => (
	          <React.Fragment key={key}>
	            <dt>{key}</dt>
	            <dd>{value}</dd>
	          </React.Fragment>
	        ))}
	      </dl>
	    </div>
	  );
	}

---

## Key Idea

Fragments are needed because `<dt>` and `<dd>` must be siblings.

---

# 9. PART 7 — Lists Inside Tables

---

## Rule

Key goes on `<tr>`, not `<td>`.

---

## Correct

	<tbody>
	  {rows.map(row => (
	    <tr key={row.id}>
	      <td>{row.name}</td>
	      <td>{row.age}</td>
	    </tr>
	  ))}
	</tbody>

---

## Wrong

	<tr>
	  <td key={row.id}>...</td>
	</tr>

---

# 10. PART 8 — Lists Inside Lists

---

## Example

	{categories.map(category => (
	  <li key={category.id}>
	    <h3>{category.name}</h3>

	    <ul>
	      {category.books.map(book => (
	        <li key={book.id}>{book.title}</li>
	      ))}
	    </ul>
	  </li>
	))}

---

## Rule

Each level needs its own key.

---

# 11. PART 9 — When You DON’T Need Keys

---

## Example

	{condition && <Item />}

---

## Why?

- Not a list  
- Only one element  

---

## Rule

Keys are required only when:

- Rendering multiple siblings  
- Using `.map()`  

---

# 12. Final Summary

---

| Scenario                | What to do                        |
|------------------------|----------------------------------|
| Simple lists           | Use `key={id}`                   |
| Nested lists           | Key each list separately         |
| Fragments              | Use `<React.Fragment key=...>`   |
| Tables                 | Key on `<tr>`                    |
| Multiple maps          | Keys unique per list only        |
| Conditions + mapping   | Filter → map                     |

---

# 13. Final Mental Model

Every `.map()` creates a list → every list needs keys.

---

# One-Line Understanding

> In complex React UIs, every list—whether nested, fragmented, or conditional—must have stable keys so React can correctly track and update elements.
