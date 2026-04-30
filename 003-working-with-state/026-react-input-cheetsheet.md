# React Input Cheatsheet 

---

# 0. What This Lesson Is Really Teaching

This lesson is NOT just about inputs.

It is teaching:

👉 How ALL form inputs connect to React state  
👉 How controlled components work  
👉 How different inputs behave internally  

---

# 1. The Core Rule (Everything Comes From This)

---

## Golden Rule

```
value / checked  +  onChange  =  controlled input
```

---

👉 This applies to almost ALL inputs  

---

---

# 2. Controlled vs Uncontrolled (Foundation)

---

## Controlled Input

```
<input value={state} onChange={...} />
```

---

👉 React controls the input  

---

## Uncontrolled Input

```
<input defaultValue="Hello" />
```

---

👉 Browser controls the input  

---

---

# 3. Text Inputs (Most Important)

---

## Controlled Text Input

```
const [name, setName] = useState('');
```

---

```
<input
  value={name}
  onChange={(e) => setName(e.target.value)}
/>
```

---

# Step-by-Step

---

### Step 1

User types  

---

### Step 2

onChange fires  

---

### Step 3

```
setName(e.target.value)
```

---

### Step 4

React updates state  

---

### Step 5

UI re-renders  

---

---

# Important Gotcha

---

❌ Wrong:

```
useState()
```

---

✔ Correct:

```
useState('')
```

---

👉 Why?

Because React doesn’t like switching:

```
uncontrolled → controlled
```

---

---

# 4. Text Input Variants

---

Examples:

```
type="email"
type="password"
type="tel"
```

---

👉 ALL behave exactly like text input  

---

✔ Same pattern  
✔ Same logic  

---

---

# 5. Textarea

---

```
<textarea
  value={comment}
  onChange={(e) => setComment(e.target.value)}
/>
```

---

👉 Same as text input  

---

✔ No difference  

---

---

# 6. Radio Buttons (Important Difference)

---

Radio uses:

```
checked
```

---

## Example

```
<input
  type="radio"
  value="yes"
  checked={state === "yes"}
  onChange={(e) => setState(e.target.value)}
/>
```

---

# Why checked?

---

Because:

👉 Multiple inputs share SAME state  

---

---

# Required Attributes

---

| Attribute | Purpose |
|----------|--------|
| name     | group radios |
| value    | represents option |
| checked  | controlled state |
| onChange | update state |

---

---

# 7. Radio Buttons — Iteration Pattern

---

```
OPTIONS.map(option => (
  <input
    key={option}
    value={option}
    checked={option === selected}
  />
))
```

---

👉 This is real-world pattern  

---

---

# BIG Gotcha — Shadowing

---

❌ Wrong:

```
map((language) => ...)
```

---

If state is also `language`

👉 you overwrite it  

---

✔ Use:

```
map((option) => ...)
```

---

---

# 8. Checkboxes

---

## Single Checkbox

---

```
const [checked, setChecked] = useState(false);
```

---

```
<input
  type="checkbox"
  checked={checked}
  onChange={(e) => setChecked(e.target.checked)}
/>
```

---

👉 Uses:

```
e.target.checked
```

---

---

# 9. Multiple Checkboxes (Important Pattern)

---

State:

```
{
  anchovies: false,
  chicken: true
}
```

---

Rendering:

```
Object.keys(state).map(option => (
  <input
    checked={state[option]}
    onChange={(e) => {
      setState({
        ...state,
        [option]: e.target.checked
      })
    }}
  />
))
```

---

👉 This is called:

```
object-based state pattern
```

---

---

# 10. Why This Pattern?

---

Because:

👉 Multiple independent values  

---

---

# 11. Select (Dropdown)

---

```
<select
  value={age}
  onChange={(e) => setAge(e.target.value)}
>
```

---

👉 Works exactly like text input  

---

---

# Important Gotcha

---

State MUST match option:

```
useState("0-18")
```

---

Must exist in:

```
<option value="0-18">
```

---

---

# Better Approach

---

Single source of truth:

```
const OPTIONS = [...]
```

---

Then:

```
useState(OPTIONS[0].value)
```

---

---

# 12. Specialty Inputs

---

Examples:

- range (slider)
- color picker
- date picker

---

## Example

```
<input
  type="range"
  value={volume}
  onChange={(e) => setVolume(e.target.value)}
/>
```

---

👉 Same pattern again  

---

---

# 13. Why Everything Feels Similar

---

Because React treats inputs uniformly:

---

```
Input = state reflection
```

---

---

# 14. Most Important Pattern (Memorize)

---

| Input Type | Uses         |
|-----------|--------------|
| text      | value        |
| textarea  | value        |
| select    | value        |
| range     | value        |
| radio     | checked      |
| checkbox  | checked      |

---

---

# 15. Common Mistakes

---

## Mistake 1 — Missing initial value

❌

```
useState()
```

---

## Mistake 2 — Mixing controlled/uncontrolled

---

## Mistake 3 — Wrong property

❌

```
value for checkbox
```

---

✔

```
checked
```

---

---

# 16. Why Controlled Inputs Matter

---

## Without React

❌ DOM controls everything  

---

## With React

✔ State controls UI  

---

---

# 17. Flow of Data

---

```
User → Event → State → UI
```

---

---

# 18. Real-World Benefits

---

✔ Validation  
✔ Dynamic UI  
✔ Predictable behavior  
✔ Easy debugging  
✔ Form submission handling  

---

---

# 19. Final Mental Model

---

👉 Inputs do NOT store data  

---

👉 State stores data  

---

👉 Input shows state  

---

---

# 20. Final Summary

---

✔ Controlled inputs = value/checked + onChange  
✔ Text inputs use value  
✔ Radio/checkbox use checked  
✔ State must be initialized correctly  
✔ All inputs follow same pattern  
✔ React state is single source of truth

---

# FINAL ONE-LINE UNDERSTANDING

All React form inputs are just visual representations of state, where user actions update state through onChange, and React re-renders the UI to match that state.
