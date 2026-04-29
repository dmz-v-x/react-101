# Working with Forms in React

---

# Introduction

Forms are one of the most important parts of any application.

They allow users to:

- Enter data
- Submit information
- Interact with your app

Examples:

- Login forms
- Signup forms
- Search inputs
- Checkout forms

---

# Mental Model (Very Important)

In React:

HTML form → becomes controlled by JavaScript

This means:

👉 React controls the data  
👉 Not the DOM  

---

# 1. Basic HTML Form (Before React)

Example:

<form>
  <input type="text" />
  <button>Submit</button>
</form>

---

## Problem with HTML forms

- Browser handles everything
- Page refreshes on submit
- Hard to control behavior

---

# 2. React Approach to Forms

React gives you control over:

- Input values
- Submission
- Validation
- Behavior

---

# 3. Controlled Components (Core Concept)

---

## Definition

A controlled component is:

👉 An input whose value is controlled by React state

---

## Example

import { useState } from "react";

function Form() {
  const [name, setName] = useState("");

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}

---

## What’s happening

- value={name} → React controls input value
- onChange → updates state
- state → updates UI

---

## Data Flow

User types → onChange → state updates → UI updates

---

# 4. Why Controlled Components?

---

## Benefits

- Single source of truth
- Easy validation
- Easy debugging
- Predictable behavior

---

# 5. Handling Input Change

---

## Example

function Form() {
  const [email, setEmail] = useState("");

  function handleChange(e) {
    setEmail(e.target.value);
  }

  return (
    <input value={email} onChange={handleChange} />
  );
}

---

## Important

e.target.value → gives current input value

---

# 6. Handling Form Submission

---

## Problem

Forms reload page by default

---

## Solution

Use preventDefault()

---

## Example

function Form() {
  const [name, setName] = useState("");

  function handleSubmit(e) {
    e.preventDefault();
    console.log(name);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <button type="submit">Submit</button>
    </form>
  );
}

---

## Key Points

- onSubmit handles form submission
- preventDefault stops page reload

---

# 7. Multiple Inputs (Important Pattern)

---

## Problem

Handling many inputs separately is repetitive

---

## Solution

Use one state object

---

## Example

function Form() {
  const [formData, setFormData] = useState({
    name: "",
    email: ""
  });

  function handleChange(e) {
    const { name, value } = e.target;

    setFormData({
      ...formData,
      [name]: value
    });
  }

  return (
    <>
      <input name="name" value={formData.name} onChange={handleChange} />
      <input name="email" value={formData.email} onChange={handleChange} />
    </>
  );
}

---

## Key Idea

name attribute links input to state

---

# 8. Different Input Types

---

## Text Input

<input type="text" />

---

## Password

<input type="password" />

---

## Checkbox

<input
  type="checkbox"
  checked={isChecked}
  onChange={(e) => setIsChecked(e.target.checked)}
/>

---

## Radio Buttons

<input
  type="radio"
  value="male"
  checked={gender === "male"}
  onChange={(e) => setGender(e.target.value)}
/>

---

## Select Dropdown

<select value={value} onChange={(e) => setValue(e.target.value)}>
  <option value="A">A</option>
  <option value="B">B</option>
</select>

---

## Textarea

<textarea value={text} onChange={(e) => setText(e.target.value)} />

---

# 9. Controlled vs Uncontrolled Components

---

## Controlled

React controls input

value={state}

---

## Uncontrolled

DOM controls input

Use ref

---

## Example (Uncontrolled)

import { useRef } from "react";

function Form() {
  const inputRef = useRef();

  function handleSubmit() {
    console.log(inputRef.current.value);
  }

  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}

---

## When to use uncontrolled

- Simple forms
- Quick prototypes

---

# 10. Form Validation

---

## Example

function Form() {
  const [email, setEmail] = useState("");
  const [error, setError] = useState("");

  function handleSubmit(e) {
    e.preventDefault();

    if (!email.includes("@")) {
      setError("Invalid email");
      return;
    }

    setError("");
    console.log("Submitted");
  }

  return (
    <form onSubmit={handleSubmit}>
      <input value={email} onChange={(e) => setEmail(e.target.value)} />
      {error && <p>{error}</p>}
      <button>Submit</button>
    </form>
  );
}

---

# 11. Handling Multiple Fields with Validation

---

function Form() {
  const [data, setData] = useState({
    email: "",
    password: ""
  });

  const [errors, setErrors] = useState({});

  function handleSubmit(e) {
    e.preventDefault();

    let newErrors = {};

    if (!data.email.includes("@")) {
      newErrors.email = "Invalid email";
    }

    if (data.password.length < 6) {
      newErrors.password = "Too short";
    }

    setErrors(newErrors);
  }
}

---

# 12. Resetting a Form

---

function handleReset() {
  setFormData({
    name: "",
    email: ""
  });
}

---

# 13. Disabling Submit Button

---

<button disabled={!email}>
  Submit
</button>

---

# 14. Best Practices

---

- Always use controlled components for complex forms  
- Use one handler for multiple inputs  
- Validate before submission  
- Use meaningful state names  
- Avoid unnecessary re-renders  

---

# 15. Common Mistakes

---

## Mistake 1

Not using value → uncontrolled input

---

## Mistake 2

Forgetting preventDefault()

---

## Mistake 3

Using wrong property

Use:

e.target.value  
e.target.checked  

---

## Mistake 4

Mutating state directly

---

# 16. Advanced Concepts

---

## Debouncing input

Avoid too many updates

---

## Form libraries

- Formik
- React Hook Form

---

## Why use libraries?

- Less boilerplate
- Built-in validation
- Better performance

---

# 17. Final Summary

---

- Forms in React are controlled by state  
- Inputs use value + onChange  
- Forms use onSubmit + preventDefault  
- Use one state object for multiple inputs  
- Validate before submitting  

---

# Final Mental Model

User input → React state → UI updates → submit handled by React  

---

# One-Line Understanding

Forms in React are controlled components where React manages input values through state, giving you full control over behavior, validation, and submission.
