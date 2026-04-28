# Props + `children` + Composition in React

---

## 1. How Props + `children` Work Together

A component can accept both:

- Normal props (data/configuration)  
- `children` (content inside the component)

---

### Example

	function AlertBox({ type, children }) {
	  const colors = {
	    warning: "orange",
	    error: "red",
	    success: "green"
	  };

	  return (
	    <div style={{ border: `2px solid ${colors[type]}`, padding: 20 }}>
	      {children}
	    </div>
	  );
	}

---

### Usage

	<AlertBox type="warning">
	  Check your input!
	</AlertBox>

	<AlertBox type="success">
	  Saved successfully!
	</AlertBox>

---

### What’s happening

- `type` → controls styling (configuration)  
- `children` → provides content  

---

### Key idea

- Props = how component behaves  
- `children` = what it displays inside  

---

## 2. Component Composition (Core Idea of React)

Composition means:

- Build small components  
- Combine them into bigger components  
- Combine those into full UI screens  

---

### Example

	function Card({ children }) {
	  return <div className="card">{children}</div>;
	}

	function UserInfo({ name }) {
	  return <p>Name: {name}</p>;
	}

	function UserCard() {
	  return (
	    <Card>
	      <UserInfo name="Sumeet" />
	      <button>Follow</button>
	    </Card>
	  );
	}

---

### Structure

	UserCard
	 ├── Card
	 │     ├── UserInfo
	 │     └── button

---

### Key idea

React UIs are built by **nesting components inside each other**.

---

## 3. Cloning or Modifying Children (Advanced)

Sometimes you want to:

- Add props to children  
- Modify children  
- Wrap children with extra behavior  

---

### Tool: `React.cloneElement`

---

### Example

	function LabelledField({ label, children }) {
	  const newChild = React.cloneElement(children, {
	    style: { border: "1px solid black" }
	  });

	  return (
	    <label>
	      {label}
	      {newChild}
	    </label>
	  );
	}

---

### Usage

	<LabelledField label="Email:">
	  <input type="email" />
	</LabelledField>

---

### What happens

The child gets modified:

	<input type="email" style={{ border: "1px solid black" }} />

---

### Common use cases

- Form libraries  
- Controlled components  
- Wrapping inputs or links  
- Injecting behavior automatically  

---

## Bonus: When NOT to Use `children`

Do not use `children` when:

- The component expects a simple value  
- The component is not meant to wrap UI  

---

### Bad

	<Button>
	  {"Save"}
	</Button>

---

### Better

	<Button label="Save" />

---

### Rule

Use `children` when the component behaves like a **container/wrapper**.

---

## Final Cheat Sheet

- `children` is just a prop that holds nested content  
- Combine props + `children` for flexible components  
- Composition = building UI by nesting components  
- Use `React.Children` utilities when needed  
- Use `React.cloneElement` to modify children  
- Validate children to avoid bugs  
- Best use case → layout and wrapper components  

---

## One-Line Understanding

> Combine props for configuration and `children` for content, and use composition to build complex UIs from small reusable components.
