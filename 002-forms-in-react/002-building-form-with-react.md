# Building a Full Advanced Form in React

---

# 0. Goal

We will build a **complete real-world form** step by step, adding features one by one.

This form will include:

- username
- email
- password
- checkbox
- radio buttons
- select (multiple options)
- hidden input
- default values
- form action (handled in React)
- rendering arrays
- key prop
- focus state
- reset
- key reset (force full form reset)

---

# IMPORTANT APPROACH

We will:

1. Start simple  
2. Add one feature at a time  
3. Understand deeply before moving forward  

---

# STEP 1 — Basic Form Structure

---

	function App() {
	  return (
	    <form>
	      <input placeholder="Username" />
	      <button>Submit</button>
	    </form>
	  );
	}

---

## Problem

- React is NOT controlling anything  
- No access to values  

---

# STEP 2 — Add State (Controlled Input)

---

	import { useState } from "react";

	function App() {
	  const [username, setUsername] = useState("");

	  return (
	    <input
	      value={username}
	      onChange={(e) => setUsername(e.target.value)}
	      placeholder="Username"
	    />
	  );
	}

---

# STEP 3 — Expand to Full Form State

---

	const [form, setForm] = useState({
	  username: "",
	  email: "",
	  password: "",
	  gender: "",
	  role: "",
	  skills: [],
	  agree: false
	});

---

# STEP 4 — Universal Change Handler

---

	function handleChange(e) {
	  const { name, value, type, checked } = e.target;

	  setForm({
	    ...form,
	    [name]: type === "checkbox" ? checked : value
	  });
	}

---

# STEP 5 — Add Inputs (Different Types)

---

	<input name="username" value={form.username} onChange={handleChange} />
	<input type="email" name="email" value={form.email} onChange={handleChange} />
	<input type="password" name="password" value={form.password} onChange={handleChange} />

---

# STEP 6 — Radio Buttons

---

	<label>
	  <input
	    type="radio"
	    name="gender"
	    value="male"
	    checked={form.gender === "male"}
	    onChange={handleChange}
	  />
	  Male
	</label>

	<label>
	  <input
	    type="radio"
	    name="gender"
	    value="female"
	    checked={form.gender === "female"}
	    onChange={handleChange}
	  />
	  Female
	</label>

---

# STEP 7 — Select (Dropdown)

---

	<select name="role" value={form.role} onChange={handleChange}>
	  <option value="">Select role</option>
	  <option value="admin">Admin</option>
	  <option value="user">User</option>
	</select>

---

# STEP 8 — Multiple Select (Array Rendering)

---

	const skillsList = ["React", "Node", "CSS"];

---

	<select
	  multiple
	  value={form.skills}
	  onChange={(e) => {
	    const selected = Array.from(e.target.selectedOptions, o => o.value);
	    setForm({ ...form, skills: selected });
	  }}
	>
	  {skillsList.map((skill) => (
	    <option key={skill} value={skill}>
	      {skill}
	    </option>
	  ))}
	</select>

---

## Key Concept

- Rendering array using `.map()`
- Using `key={skill}`

---

# STEP 9 — Checkbox

---

	<input
	  type="checkbox"
	  name="agree"
	  checked={form.agree}
	  onChange={handleChange}
	/>

---

# STEP 10 — Hidden Input

---

	<input type="hidden" name="userId" value="12345" />

---

# STEP 11 — Default Values

---

	const [form, setForm] = useState({
	  username: "guest",
	  email: "",
	  password: "",
	  gender: "male",
	  role: "user",
	  skills: [],
	  agree: false
	});

---

# STEP 12 — Focus State

---

	const [focused, setFocused] = useState("");

---

	<input
	  name="username"
	  onFocus={() => setFocused("username")}
	  onBlur={() => setFocused("")}
	/>

---

## Example UI

	{focused === "username" && <p>Typing username...</p>}

---

# STEP 13 — Form Submission (Form Action)

---

	function handleSubmit(e) {
	  e.preventDefault();
	  console.log("Form Data:", form);
	}

---

	<form onSubmit={handleSubmit}>

---

## Note

React replaces traditional `action=""`

---

# STEP 14 — Reset Form

---

	function handleReset() {
	  setForm({
	    username: "",
	    email: "",
	    password: "",
	    gender: "",
	    role: "",
	    skills: [],
	    agree: false
	  });
	}

---

# STEP 15 — Key Reset (Force Full Reset)

---

	const [formKey, setFormKey] = useState(0);

---

	function forceReset() {
	  setFormKey((prev) => prev + 1);
	}

---

## Usage

	<form key={formKey}>

---

## Why this works

Changing key → React destroys and recreates component

---

# STEP 16 — Full Final Form

---

	import { useState } from "react";

	function App() {
	  const [formKey, setFormKey] = useState(0);

	  const [form, setForm] = useState({
	    username: "guest",
	    email: "",
	    password: "",
	    gender: "",
	    role: "",
	    skills: [],
	    agree: false
	  });

	  const [focused, setFocused] = useState("");

	  function handleChange(e) {
	    const { name, value, type, checked } = e.target;

	    setForm({
	      ...form,
	      [name]: type === "checkbox" ? checked : value
	    });
	  }

	  function handleSubmit(e) {
	    e.preventDefault();
	    console.log(form);
	  }

	  function handleReset() {
	    setForm({
	      username: "",
	      email: "",
	      password: "",
	      gender: "",
	      role: "",
	      skills: [],
	      agree: false
	    });
	  }

	  function forceReset() {
	    setFormKey((prev) => prev + 1);
	  }

	  const skillsList = ["React", "Node", "CSS"];

	  return (
	    <form key={formKey} onSubmit={handleSubmit}>
	      <input
	        name="username"
	        value={form.username}
	        onChange={handleChange}
	        onFocus={() => setFocused("username")}
	        onBlur={() => setFocused("")}
	      />

	      {focused === "username" && <p>Typing username...</p>}

	      <input name="email" value={form.email} onChange={handleChange} />

	      <input type="password" name="password" value={form.password} onChange={handleChange} />

	      <label>
	        <input
	          type="radio"
	          name="gender"
	          value="male"
	          checked={form.gender === "male"}
	          onChange={handleChange}
	        />
	        Male
	      </label>

	      <select name="role" value={form.role} onChange={handleChange}>
	        <option value="">Select role</option>
	        <option value="admin">Admin</option>
	        <option value="user">User</option>
	      </select>

	      <select
	        multiple
	        value={form.skills}
	        onChange={(e) => {
	          const selected = Array.from(e.target.selectedOptions, o => o.value);
	          setForm({ ...form, skills: selected });
	        }}
	      >
	        {skillsList.map((skill) => (
	          <option key={skill} value={skill}>
	            {skill}
	          </option>
	        ))}
	      </select>

	      <input
	        type="checkbox"
	        name="agree"
	        checked={form.agree}
	        onChange={handleChange}
	      />

	      <input type="hidden" name="userId" value="12345" />

	      <button type="submit">Submit</button>
	      <button type="button" onClick={handleReset}>Reset</button>
	      <button type="button" onClick={forceReset}>Force Reset</button>
	    </form>
	  );
	}

	export default App;

---

# FINAL MENTAL MODEL

User Input → onChange → state → UI → submit → reset → re-render  

---

# One-Line Understanding

A full React form is built by controlling every input via state, handling changes with one unified function, rendering dynamic inputs with arrays, and managing behavior like validation, focus, and reset entirely through JavaScript.
