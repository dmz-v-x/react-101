# Component Card Exercise

---

# STEP 0 — What is the Problem?

You are given this repeated UI:

	<li className="contact-card">
	  <h2>Sunita Kumar</h2>
	  <dl>
	    <dt>Job</dt>
	    <dd>Electrical Engineer</dd>
	    <dt>Email</dt>
	    <dd>sunita.kumar@acme.co</dd>
	  </dl>
	</li>

…and it is repeated 3 times with different data. :contentReference[oaicite:0]{index=0}

---

## Problem Observation (VERY IMPORTANT)

Look carefully:

### What is SAME?

- `<li className="contact-card">`
- `<h2>...</h2>`
- `<dl> ... </dl>`
- Structure/layout

---

### What is DIFFERENT?

- Name  
- Job  
- Email  

---

## Core Idea (INTUITION)

This problem is testing:

> **Component Reusability + Props**

---

### Mental Model

Instead of writing UI 3 times:

Extract the repeated structure  
Replace changing parts with props  

---

# STEP 1 — Identify Pattern

We find a repeated pattern:

	<li className="contact-card">
	  <h2>NAME</h2>
	  <dl>
	    <dt>Job</dt>
	    <dd>JOB</dd>
	    <dt>Email</dt>
	    <dd>EMAIL</dd>
	  </dl>
	</li>

---

### Replace dynamic values with variables

	NAME → name  
	JOB → job  
	EMAIL → email  

---

# STEP 2 — Create a Component

Now convert this into a reusable function:

	function ContactCard({ name, job, email }) {
	  return (
	    <li className="contact-card">
	      <h2>{name}</h2>
	      <dl>
	        <dt>Job</dt>
	        <dd>{job}</dd>

	        <dt>Email</dt>
	        <dd>{email}</dd>
	      </dl>
	    </li>
	  );
	}

---

## What just happened?

You:

- Extracted repeated UI  
- Converted it into a function  
- Used props for dynamic values  

---

# STEP 3 — Use the Component

Now instead of repeating JSX, we reuse the component:

	function App() {
	  return (
	    <ul>
	      <ContactCard
	        name="Sunita Kumar"
	        job="Electrical Engineer"
	        email="sunita.kumar@acme.co"
	      />

	      <ContactCard
	        name="Henderson G. Sterling II"
	        job="Receptionist"
	        email="henderson-the-second@acme.co"
	      />

	      <ContactCard
	        name="Aoi Kobayashi"
	        job="President"
	        email="kobayashi.aoi@acme.co"
	      />
	    </ul>
	  );
	}

---

## What improved?

### Before

- Repeated 30+ lines  
- Hard to maintain  

---

### After

- Clean  
- Reusable  
- Easy to scale  

---

# STEP 4 — Understand What Concept This Uses

This exercise uses:

---

## 1. Component Extraction

Breaking UI into reusable pieces.

---

## 2. Props

Passing dynamic data:

	name → string  
	job → string  
	email → string  

---

## 3. Composition

	App
	  → ContactCard
	    → DOM

---

# STEP 5 — Why `<dl>` is used?

`<dl>` = Description List

Used for key-value pairs:

	Job → Electrical Engineer  
	Email → address  

Perfect semantic HTML choice.

---

# STEP 6 — General Problem-Solving Pattern (IMPORTANT)

Whenever you see repeated JSX:

---

## Ask 3 questions:

### 1. What is repeating?

Structure/layout

---

### 2. What is changing?

Dynamic data

---

### 3. Can I turn this into a component?

YES → extract it  

---

# STEP 7 — Button Exercise (Second Part)

---

## Step 1 — Identify repetition

Two buttons:

- Same styles  
- Different text  
- Different color  

---

## Step 2 — Extract component

	function Button({ color, children }) {
	  return (
	    <button
	      style={{
	        border: '2px solid',
	        color: color,
	        borderColor: color,
	        background: 'white',
	        borderRadius: 4,
	        padding: 16,
	        margin: 8,
	      }}
	    >
	      {children}
	    </button>
	  );
	}

---

## Step 3 — Use component

	<Button color="red">Cancel</Button>
	<Button color="black">Confirm</Button>

---

## What concept is used?

- Props → color  
- Children → button text  

---

# STEP 8 — Important Concepts Learned

---

## 1. Props = dynamic data

Passed from parent → child

---

## 2. Children = content inside component

	Button text comes from children

---

## 3. Reusability

Write once → use multiple times

---

## 4. DRY Principle

Don’t Repeat Yourself

---

# STEP 9 — Common Mistakes

---

## Mistake 1: Not extracting component

Still repeating code manually

---

## Mistake 2: Hardcoding values

	function ContactCard() {
	  return <h2>Sunita</h2> // wrong
	}

---

## Mistake 3: Not using props

Dynamic data must come via props

---

# STEP 10 — Final Mental Model

Whenever you see repeated UI:

Extract it  
Replace changing parts with props  
Reuse it  

---

# FINAL ONE-LINE UNDERSTANDING

> This problem teaches you how to convert repeated JSX into reusable components using props, which is the foundation of building scalable React apps.
