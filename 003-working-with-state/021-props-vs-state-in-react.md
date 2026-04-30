# Props vs State in React

---

# 0. What This Topic Is Really About

This concept answers a very important question:

👉 Where does data live in React?  
👉 How does data move in React?  

---

React has **two main ways to handle data**:

👉 **Props** → data coming INTO a component  
👉 **State** → data managed INSIDE a component  

---

# 1. The Core Difference (One Line)

---

👉 **Props = input (read-only)**  
👉 **State = internal memory (mutable)**  

---

# 2. Understanding Props (From Scratch)

---

## What are Props?

Props are:

👉 Data passed from one component → another  

---

## Real-Life Analogy

Think of a function:

```
function greet(name) {
  return "Hello " + name;
}
```

👉 `name` is like a prop  

---

## React Example

```
<Button variant="primary">
  Confirm
</Button>
```

---

Here:

👉 `variant="primary"` is a prop  
👉 `children` ("Confirm") is also a prop  

---

## Inside the Component

```
function Button({ variant, children }) {
  return <button>{children}</button>;
}
```

---

👉 Props are just **function parameters**

---

# 3. Key Properties of Props

---

✔ Read-only (immutable)  
✔ Passed from parent → child  
✔ Cannot be changed by child  
✔ Used for customization  

---

## Important Rule

```
props are READ-ONLY
```

---

# 4. Why Props Exist

---

Without props:

❌ Every component would be fixed  
❌ No reusability  

---

With props:

✔ Same component → different behavior  

---

## Example

```
<Button variant="primary" />
<Button variant="secondary" />
```

---

👉 Same component, different UI  

---

# 5. Understanding State (From Scratch)

---

## What is State?

State is:

👉 Data that changes over time  
👉 Stored inside a component  

---

## Example

```
const [hasAgreed, setHasAgreed] = useState(false);
```

---

👉 `hasAgreed` = current value  
👉 `setHasAgreed` = function to update it  

---

# 6. Real Example Explained

---

```
<input
  type="checkbox"
  value={hasAgreed}
  onChange={() => setHasAgreed(!hasAgreed)}
/>
```

---

## Step-by-step

---

### Step 1

Initial state:

```
hasAgreed = false
```

---

### Step 2

User clicks checkbox  

---

### Step 3

onChange runs:

```
setHasAgreed(true)
```

---

### Step 4

React re-renders  

---

### Step 5

UI updates  

---

# 7. Key Properties of State

---

✔ Mutable (can change)  
✔ Owned by component  
✔ Causes re-render  
✔ Dynamic  

---

# 8. The MOST IMPORTANT Concept

---

👉 State is LOCAL  

---

This means:

```
App component has state
Button component DOES NOT know about it
```

---

# 9. How Data Moves in React

---

## Problem

We have state in App:

```
hasAgreed
```

---

But Button needs it  

---

## Solution

👉 Pass it via props  

---

```
<Button isEnabled={hasAgreed} />
```

---

# 10. Data Flow in React

---

👉 React uses:

```
ONE-WAY DATA FLOW
```

---

## Flow

```
State (Parent)
   ↓
Props
   ↓
Child Component
```

---

👉 Data only flows DOWN  

---

# 11. Visual Mental Model

---

```
App (state)
   ↓ props
Button
```

---

👉 Props act like **pipes/tunnels**

---

# 12. Props vs State (Side-by-Side)

---

| Feature        | Props                  | State                     |
|----------------|-----------------------|---------------------------|
| Ownership      | Parent                | Component itself          |
| Mutability     | Read-only             | Mutable                   |
| Purpose        | Pass data             | Store changing data       |
| Direction      | Parent → Child        | Internal                  |
| Triggers render| Yes (when changed)    | Yes (when updated)        |

---

# 13. Why This Design Exists

---

React enforces:

👉 Predictability  
👉 Simplicity  
👉 Debugging ease  

---

## Without This System

❌ Chaos  
❌ Hard to track data  
❌ Unpredictable UI  

---

## With This System

✔ Clear data flow  
✔ Easy debugging  
✔ Scalable architecture  

---

# 14. Real-World Flow Example

---

## Step 1 — User clicks checkbox

```
setHasAgreed(true)
```

---

## Step 2 — State updates in App  

---

## Step 3 — App re-renders  

---

## Step 4 — Props update

```
<Button isEnabled={true} />
```

---

## Step 5 — Button updates UI  

---

👉 This is React’s core loop  

---

# 15. Important Gotcha

---

## State is NOT global

---

```
Button cannot access App state directly
```

---

👉 Must pass via props  

---

# 16. Naming Props (Best Practice)

---

Instead of:

```
isEnabled
```

---

Better:

```
disabled
```

---

👉 Match HTML conventions  

---

## Example

```
<button disabled={disabled}>
```

---

---

# 17. Important UX Advice

---

## Disabled buttons problem

---

❌ Users don’t know why it’s disabled  

---

## Better approach

✔ Allow click  
✔ Show validation message  

---

---

# 18. When to Use Props vs State

---

## Use Props When:

✔ Data comes from parent  
✔ Data should not change here  

---

## Use State When:

✔ Data changes over time  
✔ User interaction needed  
✔ UI updates dynamically  

---

---

# 19. Final Mental Model

---

👉 Props = external data  
👉 State = internal data  

---

👉 Props flow DOWN  
👉 State stays LOCAL  

---

👉 Components = functions  
👉 Props = arguments  
👉 State = memory  

---

---

# 20. Final Summary

---

✔ Props = inputs (read-only)  
✔ State = internal memory (changeable)  
✔ State lives inside components  
✔ Props pass data between components  
✔ React uses one-way data flow  
✔ Props act as tunnels for state  

---

# FINAL ONE-LINE UNDERSTANDING

Props pass data into components, while state manages data inside components, and React connects them through a one-way data flow where state changes drive UI updates.
