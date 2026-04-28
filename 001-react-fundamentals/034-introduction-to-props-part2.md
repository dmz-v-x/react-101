# What Are Props in React?

Props = **inputs to components**.

They work just like function parameters.

---

## Basic Analogy (JavaScript Function)

	function greet(name) {
	  return "Hello " + name;
	}

Here, `name` is an input.

---

## React Version

	function Greeting(props) {
	  return <h1>Hello {props.name}</h1>;
	}

---

### Key idea

Props are how data is passed from **parent → child**.

---

## Properties of Props

Props are:

- Read-only  
- Immutable  
- Supplied by parent components  
- Used to customize child components  

---

## Why Are Props Needed?

Because components should be reusable and dynamic.

---

### Without props

	function Button() {
	  return <button>Click</button>
	}

Every button looks the same.

---

### With props

	function Button({ label }) {
	  return <button>{label}</button>;
	}

---

### Usage

	<Button label="Login" />
	<Button label="Signup" />

---

### Result

- Same component  
- Different output  

---

## How to Pass Props (Parent → Child)

### Parent

	<Element name="Sam" age={20} isAdmin={true} />

---

### Child

	function Element(props) {
	  return <h1>{props.name} is {props.age} years old</h1>;
	}

---

## What Can You Pass as Props?

You can pass any valid JavaScript value.

| Type              | Example                                |
|-------------------|----------------------------------------|
| string            | `<Comp text="hello" />`                |
| number            | `<Comp count={2} />`                   |
| boolean           | `<Comp active={true} />`               |
| array             | `<Comp items={[1,2,3]} />`             |
| object            | `<Comp user={{name:"Sam"}} />`         |
| JSX               | `<Comp header={<Header />} />`         |
| function          | `<Comp onClick={() => alert('hi')} />` |
| null/undefined    | `<Comp value={null} />`                |
| nested components | `<Comp LeftPane={<Sidebar />} />`      |

---

## How to Read Props

---

### Standard way

	function Card(props) {
	  return <p>{props.title}</p>;
	}

---

### Preferred way (destructuring)

	function Card({ title, price }) {
	  return <p>{title} - ${price}</p>;
	}

---

## Default Props

If a prop is not provided, you can set a default.

---

### Best practice (default parameters)

	function Button({ label = "Default" }) {
	  return <button>{label}</button>;
	}

---

## Passing Children Props

Every component automatically receives a special prop:

	props.children

---

### Parent

	<Card>
	  <p>Hello World</p>
	</Card>

---

### Child

	function Card({ children }) {
	  return <div className="card">{children}</div>;
	}

---

### Meaning

`children` = whatever is placed inside the component tag.

---

## Props vs State

| Feature          | Props                | State                    |
|------------------|---------------------|--------------------------|
| Source           | From parent         | Inside component         |
| Mutable?         | No (immutable)      | Yes (mutable)            |
| Purpose          | Configuration       | Interactive behavior     |
| Update required? | Parent re-renders   | Component updates itself |

---

## Props Are Immutable

### Invalid

	props.name = "New name"; // ❌

---

### Correct approach

If you need to modify it, move it into state:

	const [name, setName] = useState(props.name);

---

## Props Re-rendering Behavior

A component re-renders when:

- Its props change  
- Its parent re-renders (unless optimized)  

---

### Example

	<Element value={Math.random()} /> // re-renders every time

---

### Optimized case

	<MemoizedElement value="same" /> // no re-render

---

## Props with Functions (Event Handlers)

Props can also be functions.

---

### Parent

	<Counter onIncrement={() => setCount(count + 1)} />

---

### Child

	function Counter({ onIncrement }) {
	  return <button onClick={onIncrement}>+</button>;
	}

---

### Purpose

Allows child → parent communication.

---

## How React Handles Props Internally

When you write:

	<Component name="Sam" age={20} />

---

React converts it into:

	React.createElement(Component, {
	  name: "Sam",
	  age: 20
	});

---

Then React calls:

	Component({ name: "Sam", age: 20 });

---

### Key idea

Props are just a plain JavaScript object passed into your function.

---

## When NOT to Use Props

- For mutable data → use state  
- For cross-component communication → use context  
- For global data → use context / Redux / Zustand  
- For logic reuse → use custom hooks  

---

## Final Mental Model

- Props = inputs to a component  
- Passed from parent → child  
- Immutable and read-only  
- Used to customize UI  
- Can be any JavaScript value  
- Enable reusability  

---

## One-Line Understanding

> Props are read-only inputs passed from parent to child components, allowing the same component to render different data.
