# Complete Working Example Exercise — Accessibility + Conditional Rendering

---

# 1. Question

You are given a list of friends.

Some are online, some are offline.

Currently:

- Online users show a green dot  
- Offline users show nothing  

---

## Problem

Screen readers cannot understand the green dot.

So visually impaired users **won’t know who is online**.

---

## Task

- Add text “(Online)” for online users  
- This text should NOT be visible on screen  
- But it MUST be read by screen readers  

---

## Constraint

Use a `VisuallyHidden` component.

---

# 2. Intuition (Core Idea)

---

## Problem Breakdown

We currently have:

- Visual indicator → green dot  
- But no semantic meaning  

---

## Screen reader behavior

Screen readers:

- Read text  
- Ignore meaningless `<div>` elements  

---

## Solution Idea

Add hidden text:

- Visible → No  
- Accessible → Yes  

---

## Mental Model

Visual UI + Hidden semantic text = Accessible UI  

---

# 3. Approach (Step-by-Step)

---

## Step 1 — Identify condition

We only want this for:

	isOnline === true

---

## Step 2 — Add conditional rendering

Use:

	isOnline && (...)

---

## Step 3 — Add hidden text

Use:

	<VisuallyHidden>(Online)</VisuallyHidden>

---

## Step 4 — Place it after name

So screen readers read:

	"Beatrice (Online)"

---

# 4. Final Working Code

---

## App.js

	import VisuallyHidden from "./VisuallyHidden";

	function Friend({ name, isOnline }) {
	  return (
	    <li className="friend">
	      {isOnline && <div className="green-dot" />}
	      {name}
	      {isOnline && (
	        <VisuallyHidden> (Online)</VisuallyHidden>
	      )}
	    </li>
	  );
	}

	function App() {
	  return (
	    <ul className="friend-list">
	      <Friend name="Andrew" isOnline={false} />
	      <Friend name="Beatrice" isOnline={true} />
	      <Friend name="Chen" isOnline={true} />
	    </ul>
	  );
	}

	export default App;

---

## VisuallyHidden.js

	function VisuallyHidden({ children }) {
	  return (
	    <span
	      style={{
	        position: "absolute",
	        width: "1px",
	        height: "1px",
	        padding: 0,
	        margin: "-1px",
	        overflow: "hidden",
	        clip: "rect(0, 0, 0, 0)",
	        whiteSpace: "nowrap",
	        border: 0,
	      }}
	    >
	      {children}
	    </span>
	  );
	}

	export default VisuallyHidden;

---

# 5. What’s Happening

---

## Visual Output

- Online → green dot + name  
- Offline → just name  

---

## Screen Reader Output

- "Andrew"  
- "Beatrice (Online)"  
- "Chen (Online)"  

---

## Key Insight

We improved accessibility **without changing UI**.

---

# 6. Why Not Use aria-label?

---

## Alternative (NOT ideal here)

	<div className="green-dot" aria-label="(Online)" />

---

## Problem

- Works only for interactive elements  
- Harder to control reading order  
- Less flexible  

---

## Better approach

Use actual hidden text.

---

# 7. Key Learning

---

- Visual UI ≠ Accessible UI  
- Screen readers need meaningful text  
- Conditional rendering works for accessibility too  
- Hidden content can still be read  

---

# 8. Real-World Concept

---

This pattern is used in:

- Notifications  
- Status indicators  
- Form errors  
- Icons without text  

---

# 9. Summary

---

- Use conditional rendering for logic  
- Use VisuallyHidden for accessibility  
- Combine both for better UX  

---

# One-Line Understanding

> Always pair visual indicators with hidden semantic text so assistive technologies can understand your UI correctly.
