# Component Instances in React

---

# 0. What This Concept Is Really About

This is a **VERY important hidden concept** in React:

👉 Where does state actually live?  
👉 How does React remember data between renders?  

---

The answer is:

👉 **Component Instances**

---

---

# 1. First Question You Must Ask

---

When you write:

```
const [count, setCount] = useState(0);
```

---

👉 Where is this `count` stored?

---

Is it:

- inside JSX?
- inside DOM?
- inside React element?

---

❌ NO  

---

👉 It is stored inside a **component instance**  

---

---

# 2. What is a Component Instance?

---

👉 A component instance is:

```
a hidden object created by React
that stores all data related to that component
```

---

It stores:

✔ State  
✔ Hooks  
✔ Context  
✔ Internal metadata  

---

---

# 3. Very Important Distinction

---

## React Element vs Component Instance

---

### React Element

```
const element = <Counter />
```

---

👉 This is just:

```
a plain JavaScript object
```

---

It describes UI  

---

BUT:

👉 It does NOT store state  

---

---

### Component Instance

---

Created when React **renders** the element  

---

👉 This is where state lives  

---

---

# 4. Key Rule

---

```
ELEMENT ≠ INSTANCE
```

---

👉 Element = description  
👉 Instance = real working unit  

---

---

# 5. When Does Instance Get Created?

---

👉 When component is rendered for the first time  

---

This is called:

```
MOUNTING
```

---

---

# 6. Mounting — Step by Step

---

When React renders:

```
<Counter />
```

---

React does:

---

## Step 1 — Evaluate JSX

```
returns UI description
```

---

## Step 2 — Create DOM nodes  

---

## Step 3 — Create component instance  

---

👉 This instance stores state  

---

---

# 7. Where useState Connects

---

When you write:

```
const [count, setCount] = useState(0);
```

---

👉 React internally does:

```
instance.state = 0
```

---

👉 useState "hooks into" the instance  

---

---

# 8. Why It Is Called a Hook

---

Because:

👉 It hooks into the component instance  

---

---

# 9. Example — Multiple Instances

---

```
<Counter />
<Counter />
<Counter />
```

---

👉 React creates:

```
Instance 1 → count = 0
Instance 2 → count = 0
Instance 3 → count = 0
```

---

👉 Each has its own state  

---

---

# 10. Why State is NOT Shared

---

Because:

👉 Each component = separate instance  

---

---

# 11. What Happens on Re-render

---

When state updates:

```
setCount(1)
```

---

React:

---

## Step 1

Calls component again  

---

## Step 2

Uses SAME instance  

---

## Step 3

Reads updated state  

---

---

👉 Instance persists  

---

---

# 12. Important Concept — Instance Lifetime

---

👉 Instance lives as long as component is mounted  

---

---

# 13. What is Unmounting?

---

👉 Removing component from UI  

---

Example:

```
{show && <Footer />}
```

---

If `show = false`:

👉 Footer is removed  

---

👉 Instance is destroyed  

---

👉 State is LOST  

---

---

# 14. Real Example Explained

---

```
{includeFooter && <Footer />}
```

---

## Case 1 — true

👉 Footer mounts  
👉 Instance created  
👉 State initialized  

---

## Case 2 — false

👉 Footer unmounts  
👉 Instance destroyed  
👉 State gone  

---

---

# 15. Why State Resets

---

Because:

👉 New instance is created when re-mounted  

---

---

# 16. Example

---

```
function Footer() {
  const [color, setColor] = useState("blue");
}
```

---

Toggle OFF → ON:

👉 New instance  

👉 color resets  

---

---

# 17. Important Insight

---

👉 State belongs to INSTANCE  

NOT:

❌ component function  
❌ JSX  

---

---

# 18. Common Confusion

---

## This does NOT create instance:

```
const elem = <Counter />
```

---

👉 It only creates:

```
JS object
```

---

👉 No state  
👉 No instance  

---

---

## This creates instance:

```
root.render(<Counter />)
```

---

👉 React renders → instance created  

---

---

# 19. Why This Matters

---

Without understanding instances:

❌ You won’t understand state reset  
❌ You’ll get confused by conditional rendering  
❌ You’ll misinterpret React behavior  

---

---

# 20. Internal Mental Model

---

Think:

---

```
<Component />
   ↓
React renders
   ↓
Instance created
   ↓
State stored here
```

---

---

# 21. Real-Life Analogy

---

Component = Blueprint  

Instance = Actual building  

---

Blueprint:

```
Counter component
```

---

Instances:

```
Building 1
Building 2
Building 3
```

---

Each building has:

✔ its own rooms  
✔ its own state  

---

---

# 22. Final Key Rules

---

✔ Rendering creates instance  
✔ Instance stores state  
✔ Each instance is independent  
✔ Unmount destroys instance  
✔ Remount creates new instance  

---

---

# 23. One-Line Summary

---

👉 State is stored inside component instances, which are created when a component is rendered and destroyed when it is unmounted. :contentReference[oaicite:0]{index=0}

---
