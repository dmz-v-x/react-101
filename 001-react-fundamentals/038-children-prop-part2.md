# Advanced Usage of the `children` Prop

---

## 1. Passing JSX as `children`

`children` does not have to be plain text.

You can pass many different types of content.

---

### Text

	<RedButton>Click me</RedButton>

---

### JSX elements

	<RedButton>
	  <strong>Warning:</strong> Delete account
	</RedButton>

---

### Multiple elements

	<RedButton>
	  <h3>Are you sure?</h3>
	  <p>This action cannot be undone.</p>
	</RedButton>

---

### Another component

	<RedButton>
	  <UserAvatar />
	</RedButton>

---

### Inside the component

You simply render:

	{children}

React will render whatever was passed.

---

## 2. When to Use `children` vs Normal Props

---

### Use `children` when content belongs inside the component

Think like HTML structure.

---

### Good use cases

	<Card>Some text inside the card</Card>

	<List>
	  <li>Item 1</li>
	  <li>Item 2</li>
	</List>

---

### Why?

These components **wrap content**, so `children` fits naturally.

---

## 3. When to Use Normal Props Instead

Use props when the value is:

- Data  
- Configuration  
- Behavior  

---

### Examples

#### Data

	<UserCard name="Sumeet" age={20} />

---

#### Configuration

	<Modal isOpen={true} onClose={closeModal} />

---

### Key idea

These are **not UI content**, so they should not be `children`.

---

## 4. Making a Wrapper Component

Sometimes you want a component that wraps other content.

---

### Example

	function Card({ children }) {
	  return (
	    <div style={{ padding: 20, border: "1px solid #ccc" }}>
	      {children}
	    </div>
	  );
	}

---

### Usage

	<Card>
	  <h2>Welcome!</h2>
	  <p>This is card content.</p>
	</Card>

---

### Result (conceptual)

	+---------------------------+
	| Welcome!                  |
	| This is card content.     |
	+---------------------------+

---

### Key idea

- `Card` does not care what is inside  
- It simply wraps content with styling  

---

## 5. `children` Can Be a Function (Advanced Pattern)

This is called the **render props pattern**.

---

### Component

	export default function Box({ children }) {
	  return (
	    <div style={{ border: "2px solid blue", padding: "10px" }}>
	      {children("I came from the Box component!")}
	    </div>
	  );
	}

---

### Usage

	import Box from "./Box";

	export default function App() {
	  return (
	    <Box>
	      {(messageFromBox) => (
	        <p>The children function received: {messageFromBox}</p>
	      )}
	    </Box>
	  );
	}

---

### What happens

- `Box` calls the function passed as `children`  
- It sends data: `"I came from the Box component!"`  
- That function returns JSX  
- React renders that JSX  

---

### Output (conceptual)

	[ Border Box ]
	  The children function received: I came from the Box component!

---

## 6. Checking if `children` Exists

You can conditionally render based on `children`.

---

### Example

	function Card({ children }) {
	  return (
	    <div>
	      {children ? children : "No content provided"}
	    </div>
	  );
	}

---

### Behavior

- If children exist → render them  
- If not → show fallback text  

---

## Final Mental Model

- `children` = content inside component tags  
- Can be text, JSX, components, or functions  
- Best used for layout and composition  
- Use normal props for data/configuration  
- Enables powerful patterns like wrappers and render props  

---

## One-Line Understanding

> The `children` prop lets you pass flexible, dynamic content into a component, making it reusable and composable for many different UI scenarios.
