# Nested Ternaries and Best Practices

---

# 1. Question

Understand:

- How nested ternaries work  
- When they are acceptable  
- When they become harmful  
- How to refactor complex ternaries into cleaner code  

---

# 2. Intuition (Core Idea)

Ternary is just a compact form of `if/else`.

---

## Basic form

	condition ? A : B

---

## But sometimes you need more than one condition

Example:

- If logged in → show dashboard  
- Else if signup allowed → show signup  
- Else → show access denied  

---

# 3. Nested Ternary (How It Works)

---

## Code

	{isLoggedIn
	  ? <Dashboard />
	  : signupAllowed
	    ? <Signup />
	    : <AccessDenied />
	}

---

## Equivalent Logic

	if (isLoggedIn) {
	  return <Dashboard />;
	} else {
	  if (signupAllowed) {
	    return <Signup />;
	  } else {
	    return <AccessDenied />;
	  }
	}

---

## Mental Model

Think top-down:

- First condition  
- If false → move to next condition  

---

# 4. When Nested Ternaries Are OK

---

Use them when:

- Logic is small  
- Only 2–3 conditions  
- JSX is short  
- Easy to read at a glance  

---

## Example (acceptable)

	{status === "loading"
	  ? "Loading..."
	  : status === "error"
	    ? "Error"
	    : "Done"
	}

---

# 5. When NOT to Use Nested Ternaries

---

## Case 1 — Large JSX blocks

---

### Bad

	{isLoggedIn ? (
	  <div className="header">
	    <Profile />
	    <Notifications />
	  </div>
	) : (
	  <LoginForm />
	)}

---

### Why bad

- Hard to read  
- Hard to maintain  

---

### Better

	let content;

	if (isLoggedIn) {
	  content = <LoggedInHeader />;
	} else {
	  content = <LoginForm />;
	}

	return <div>{content}</div>;

---

## Case 2 — Multiple conditions

---

### Bad

	{user
	  ? user.isAdmin
	    ? <AdminPanel />
	    : <UserPanel />
	  : <LoginPrompt />
	}

---

### Better

	if (!user) return <LoginPrompt />;
	if (user.isAdmin) return <AdminPanel />;
	return <UserPanel />;

---

## Case 3 — Complex logic inside ternary

---

### Bad

	{isReady ? doSomethingComplicated() : doSomethingElse()}

---

### Better

	if (isReady) {
	  return doSomethingComplicated();
	}
	return doSomethingElse();

---

## Case 4 — Long unreadable lines

---

If ternary spans many lines and becomes hard to scan → refactor.

---

# 6. Clean Ways to Write Ternaries

---

## Method 1 — Proper formatting

	{condition ? (
	  <LongComponent
	    title="Hello"
	    subtitle="World"
	    count={10}
	  />
	) : (
	  <AnotherLongComponent
	    theme="dark"
	    isVisible={true}
	  />
	)}

---

## Method 2 — Extract condition

	const showDashboard = user && user.role === "admin";

	return (
	  <>
	    {showDashboard ? <Dashboard /> : <Login />}
	  </>
	);

---

## Method 3 — Extract components

	return (
	  <>
	    {isDark ? <DarkThemePanel /> : <LightThemePanel />}
	  </>
	);

---

## Method 4 — Use variables

	const dashboardUI = (
	  <div>
	    <Header />
	    <Charts />
	  </div>
	);

	const loginUI = <LoginForm />;

	return <main>{isLoggedIn ? dashboardUI : loginUI}</main>;

---

# 7. Approach (How to Decide)

---

## Step 1

Is the condition simple?

- Yes → ternary is fine  

---

## Step 2

Is JSX small?

- Yes → ternary is fine  

---

## Step 3

Is logic complex or nested?

- Yes → use `if`  

---

## Step 4

Is readability decreasing?

- Yes → refactor  

---

# 8. Final Summary

---

| Situation              | Use Ternary? |
|------------------------|--------------|
| Simple yes/no          | Yes          |
| One-line UI            | Yes          |
| Nested logic           | No           |
| Many conditions        | No           |
| Large JSX blocks       | No           |
| Poor readability       | No           |
| Need fallback UI       | Yes          |

---

# 9. Final Mental Model

Ternary = short decision tool  
If it stops being simple → stop using it  

---

# One-Line Understanding

> Ternaries are great for small, simple UI decisions, but should be avoided when logic becomes complex, nested, or hard to read—use `if` statements or variables instead.
