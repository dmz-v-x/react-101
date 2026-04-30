# Data Binding in React

---

# 0. What This Topic Is Really About

This concept explains:

👉 How input fields connect to state  
👉 How React controls form inputs  
👉 What “controlled” vs “uncontrolled” means  
👉 Why we use `value` + `onChange` together  

---

# 1. What is Data Binding?

---

👉 Data Binding means:

**Connecting UI (input field) ↔ state (JavaScript variable)** :contentReference[oaicite:0]{index=0}  

---

## Example

Typing in input should:

✔ Update state  
✔ Reflect state in UI  

---

# 2. Basic Example

---

```
function SearchForm() {
  const [searchTerm, setSearchTerm] = React.useState('cats');

  return (
    <>
      <input
        value={searchTerm}
        onChange={(event) => {
          setSearchTerm(event.target.value);
        }}
      />

      <p>{searchTerm}</p>
    </>
  );
}
```

---

# 3. What is Happening Here (Step-by-Step)

---

## Step 1

Initial state:

	searchTerm = "cats"

---

## Step 2

React renders:

```
<input value="cats" />
```

---

## Step 3

User types:

```
cats → catsa
```

---

## Step 4

onChange runs:

```
setSearchTerm(event.target.value)
```

---

## Step 5

React updates state:

	searchTerm = "catsa"

---

## Step 6

Component re-renders

---

## Step 7

Input updates automatically

---

# 4. Important Insight

---

👉 Input is ALWAYS synced with state  

---

# 5. value in React vs HTML (CRITICAL DIFFERENCE)

---

## HTML

```
<input value="cats" />
```

👉 Just sets initial value  

👉 User can still edit  

---

## React

```
<input value={searchTerm} />
```

👉 Input is CONTROLLED by state  

👉 User cannot change it directly  

---

👉 It becomes READ-ONLY unless onChange exists  

---

# 6. Why onChange is Required

---

If you do:

```
<input value={searchTerm} />
```

---

👉 Input becomes locked  

---

## Why?

Because React keeps forcing value

---

## Fix

```
onChange={(e) => setSearchTerm(e.target.value)}
```

---

# 7. Two-Way Data Binding

---

👉 With BOTH value + onChange:

✔ State → UI  
✔ UI → State  

---

This is called:

👉 Two-way binding  

---

# 8. What Happens If You Remove One

---

## Case 1 — Remove onChange

```
<input value={searchTerm} />
```

---

👉 Input is read-only  

---

## Case 2 — Remove value

```
<input onChange={...} />
```

---

👉 Input updates state  
❌ But state does NOT update input  

---

👉 One-way binding only  

---

# 9. Controlled vs Uncontrolled Inputs

---

# Controlled Input

---

```
<input value={state} onChange={...} />
```

---

✔ React controls value  
✔ State is source of truth  

---

# Uncontrolled Input

---

```
<input />
```

---

✔ Browser controls value  
✔ React does not track  

---

# 10. Golden Rule

---

👉 Input should be EITHER controlled OR uncontrolled  

👉 Never switch between them  

---

# 11. Common Bug (VERY IMPORTANT)

---

## Problem

```
const [username, setUsername] = useState();

<input value={username} />
```

---

## What happens

	username = undefined

---

👉 React treats it as uncontrolled  

---

Later:

	username = "John"

---

👉 Now it becomes controlled  

---

## Result

⚠ Warning:

“Changing uncontrolled input to controlled” :contentReference[oaicite:1]{index=1}  

---

# 12. Correct Fix

---

```
const [username, setUsername] = useState('');
```

---

👉 Always defined  

---

✔ Always controlled  

---

# 13. Why Empty String Works

---

Even though:

	"" is falsy  

---

👉 It is still a valid value  

---

# 14. Synthetic Events (React Special Feature)

---

React uses:

👉 Synthetic events  

---

## Why?

✔ Cross-browser consistency  
✔ Better developer experience  

---

## Example

```
onChange={(event) => {
  console.log(event.target.value);
}}
```

---

## Access real event

```
event.nativeEvent
```

---

# 15. Alternative: Uncontrolled Forms (Advanced)

---

## Using FormData

```
function handleSubmit(e) {
  const formData = new FormData(e.target);
  const { username } = Object.fromEntries(formData);
}
```

---

## Pros

✔ Less state  

---

## Cons

❌ Cannot show live UI updates  
❌ Harder to sync UI  

---

# 16. Why Controlled Inputs Are Preferred

---

✔ Easy to sync UI  
✔ Real-time updates  
✔ Works with validation  
✔ Works with conditional rendering  

---

# 17. Real-World Use Case

---

Search input:

```
<input value={searchTerm} />
<p>Searching: {searchTerm}</p>
```

---

👉 Without state → impossible  

---

# 18. Key Takeaways

---

✔ Data binding connects input ↔ state  
✔ value makes input controlled  
✔ onChange updates state  
✔ Both together = two-way binding  
✔ Always initialize state  
✔ Avoid switching controlled/uncontrolled  
✔ Controlled inputs are standard in React  

---

# FINAL ONE-LINE UNDERSTANDING

Data binding in React means synchronizing form inputs with state using `value` and `onChange`, allowing React to fully control and reflect user input through its state system.
