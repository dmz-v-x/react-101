# Other Form Controls in React

---

# 0. What This Lesson Is Really About

This lesson explains:

👉 How different form elements behave in React  
👉 How React simplifies inconsistent HTML behavior  
👉 How ALL form controls follow ONE consistent pattern  

---

# 1. The Problem in Plain HTML (Very Important)

---

In normal HTML, form elements behave inconsistently:

---

## Example 1 — textarea

```
<textarea>
  Hello
</textarea>
```

👉 Value is inside children (NOT value attribute)

---

## Example 2 — select

```
<select>
  <option selected>Option 2</option>
</select>
```

👉 Uses `selected` on option  

---

## Example 3 — input

```
<input value="Hello" />
```

👉 Uses `value`

---

## Problem

👉 Every form control behaves differently  

👉 Hard to manage  

---

# 2. React Fixes This Problem

---

React standardizes ALL form controls  

---

## Universal Pattern

👉 Every form control follows:

```
value OR checked
+
onChange
```

---

✔ One consistent mental model  

---

# 3. Important Terminology

---

👉 “Input” does NOT mean only `<input>`  

---

It means:

✔ input  
✔ textarea  
✔ select  
✔ checkbox  
✔ radio  

---

👉 All are “inputs” in React :contentReference[oaicite:0]{index=0}  

---

# 4. Select Dropdown in React

---

## Step 1 — State

```
const [selectedOption, setSelectedOption] = useState('red');
```

---

## Step 2 — JSX

```
<select
  value={selectedOption}
  onChange={(e) => setSelectedOption(e.target.value)}
>
  <option value="red">Red</option>
  <option value="green">Green</option>
  <option value="blue">Blue</option>
</select>
```

---

# 5. What’s Happening Internally

---

## Step-by-step

---

### Step 1

React sets:

```
value = "red"
```

---

### Step 2

Dropdown shows "Red"

---

### Step 3

User selects "Green"

---

### Step 4

onChange fires:

```
setSelectedOption("green")
```

---

### Step 5

React re-renders

---

### Step 6

Dropdown updates to "Green"

---

# 6. Why This Is Better Than HTML

---

HTML way:

❌ Use `selected` attribute  
❌ Manual control  

---

React way:

✔ Single source of truth  
✔ Clean state-based logic  

---

# 7. Radio Buttons (Important + Tricky)

---

Radio buttons:

👉 Multiple inputs  
👉 One shared state  

---

# 8. Example

---

## Step 1 — State

```
const [value, setValue] = useState('no');
```

---

## Step 2 — JSX

```
<input
  type="radio"
  name="agree"
  value="yes"
  checked={value === "yes"}
  onChange={(e) => setValue(e.target.value)}
/>

<input
  type="radio"
  name="agree"
  value="no"
  checked={value === "no"}
  onChange={(e) => setValue(e.target.value)}
/>
```

---

# 9. Understanding Each Property (VERY IMPORTANT)

---

## name

```
name="agree"
```

👉 Groups radio buttons  

👉 Only one can be selected  

---

## value

```
value="yes"
```

👉 What gets stored in state  

---

## checked

```
checked={value === "yes"}
```

👉 Controls whether selected  

---

## onChange

```
onChange={(e) => setValue(e.target.value)}
```

👉 Updates state  

---

# 10. Mental Model for Radio

---

👉 Multiple inputs  
👉 ONE state  

---

State determines:

✔ Which radio is selected  

---

# 11. Why Radio Uses checked (NOT value)

---

Unlike select:

❌ No single value property  

---

👉 Each radio is independent  

---

So we control:

```
checked = true / false
```

---

# 12. Important Rule

---

👉 Only ONE radio should be true  

---

Otherwise UI breaks  

---

# 13. Checkbox (Quick Concept)

---

Checkbox uses:

```
checked
```

---

Example:

```
const [isChecked, setIsChecked] = useState(false);

<input
  type="checkbox"
  checked={isChecked}
  onChange={(e) => setIsChecked(e.target.checked)}
/>
```

---

👉 Notice:

```
e.target.checked
```

NOT:

```
e.target.value
```

---

# 14. Big Unification Idea

---

React makes everything behave like:

---

## Either

```
value + onChange
```

---

## OR

```
checked + onChange
```

---

👉 That’s the entire system  

---

# 15. Why This Is Powerful

---

Without React:

❌ Different APIs  
❌ Confusing behavior  
❌ Hard to maintain  

---

With React:

✔ One consistent pattern  
✔ Easy to scale  
✔ Predictable UI  

---

# 16. Real-World Use Cases

---

## Select

✔ Country selection  
✔ Category filter  

---

## Radio

✔ Gender selection  
✔ Yes/No decisions  

---

## Checkbox

✔ Accept terms  
✔ Multiple selections  

---

# 17. Final Mental Model

---

Think like this:

---

👉 Form controls = UI representation of state  

---

👉 State is the source of truth  

---

👉 UI reflects state  

---

👉 User updates state via events  

---

# 18. Final Summary

---

✔ HTML form controls are inconsistent  
✔ React standardizes everything  
✔ Use value for most inputs  
✔ Use checked for checkbox/radio  
✔ Always use onChange  
✔ State controls UI  
✔ UI updates state  

---

# FINAL ONE-LINE UNDERSTANDING

React transforms all form controls into a consistent system where state controls the UI using `value` or `checked`, and user interactions update that state through `onChange`.
