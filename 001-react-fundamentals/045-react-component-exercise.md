# React Component Exercises

---

# Exercise 1 — Extract `<ProductCard>`

---

## Step 1 — Observe the Code

	<div className="product">
	  <h2>Chocolate Cake</h2>
	  <p>Price: $10</p>
	</div>

Repeated 3 times.

---

## Step 2 — Identify Pattern

### Same:
- `div.product`
- `<h2>`
- `<p>`

### Different:
- Name  
- Price  

---

## Step 3 — Create Component

	function ProductCard({ name, price }) {
	  return (
	    <div className="product">
	      <h2>{name}</h2>
	      <p>Price: ${price}</p>
	    </div>
	  );
	}

---

## Step 4 — Use Component

	function App() {
	  return (
	    <div>
	      <ProductCard name="Chocolate Cake" price={10} />
	      <ProductCard name="Strawberry Cake" price={12} />
	      <ProductCard name="Vanilla Cake" price={9} />
	    </div>
	  );
	}

---

## Concept Used

- Component extraction  
- Props  

---

# Exercise 2 — Use `children`

---

## Step 1 — Observe Pattern

	<div className="card">
	  CONTENT
	</div>

Only inner content changes.

---

## Step 2 — Create Wrapper Component

	function Card({ children }) {
	  return <div className="card">{children}</div>;
	}

---

## Step 3 — Use It

	function App() {
	  return (
	    <>
	      <Card>
	        <h3>Title 1</h3>
	        <p>This is card one.</p>
	      </Card>

	      <Card>
	        <h3>Title 2</h3>
	        <p>This is card two.</p>
	      </Card>
	    </>
	  );
	}

---

## Concept Used

- `children`  
- Wrapper components  

---

# Exercise 3 — Props + Children (Alert)

---

## Step 1 — Identify Pattern

### Same:
- padding  
- text color  

### Different:
- background color  
- message  

---

## Step 2 — Create Component

	function Alert({ type, children }) {
	  let bgColor;

	  if (type === "error") {
	    bgColor = "red";
	  } else if (type === "success") {
	    bgColor = "green";
	  }

	  return (
	    <div style={{ padding: 20, background: bgColor, color: "white" }}>
	      {children}
	    </div>
	  );
	}

---

## Step 3 — Use It

	function App() {
	  return (
	    <>
	      <Alert type="error">
	        Something went wrong!
	      </Alert>

	      <Alert type="success">
	        Everything looks good.
	      </Alert>
	    </>
	  );
	}

---

## Concept Used

- Props (type)  
- Children (content)  
- Conditional logic  

---

# Exercise 4 — Dynamic List + Components

---

## Step 1 — Given Data

	const users = [
	  { name: "Asha", age: 22 },
	  { name: "Miguel", age: 19 },
	  { name: "Priya", age: 25 },
	];

---

## Step 2 — Create Component

	function UserItem({ name, age }) {
	  return <li>{name} ({age})</li>;
	}

---

## Step 3 — Use `.map()`

	function App() {
	  return (
	    <ul>
	      {users.map(user => (
	        <UserItem
	          key={user.name}
	          name={user.name}
	          age={user.age}
	        />
	      ))}
	    </ul>
	  );
	}

---

## Important Concept

- `.map()` returns array → JSX supports it  
- `key` helps React track items  

---

# Exercise 5 — Layout with Slots

---

## Step 1 — Understand Requirement

We need two areas:

- Left  
- Right  

---

## Step 2 — Create Component

	function Layout({ left, right }) {
	  return (
	    <div style={{ display: "flex" }}>
	      <div>{left}</div>
	      <div>{right}</div>
	    </div>
	  );
	}

---

## Step 3 — Use It

	function App() {
	  return (
	    <Layout
	      left={<Sidebar />}
	      right={<MainContent />}
	    />
	  );
	}

---

## Concept Used

- Component composition  
- Passing JSX as props  

---

## Final Big Picture

---

## Pattern Recognition (MOST IMPORTANT)

Every problem follows this:

1. Find repetition  
2. Extract component  
3. Replace changing parts with props  
4. Use children when content is inside  
5. Use `.map()` for lists  
6. Use composition for layout  

---

## Master Mental Model

- Components = reusable UI blocks  
- Props = configuration  
- Children = inner content  
- `.map()` = dynamic rendering  
- Composition = combining components  

---

## One-Line Summary

> Every React UI problem reduces to identifying repeated structure, extracting it into components, and controlling differences using props and children.
