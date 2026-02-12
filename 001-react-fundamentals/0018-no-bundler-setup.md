# JSX with CDN 

## 1. The Core Problem (Restated Clearly)

You want to:
- Write JSX
- Keep index.html and index.js separate
- Avoid bundlers (Vite, Webpack, etc.)
- Still run everything in the browser

The problem is:

> Browsers cannot execute JSX.

So we need **one extra step** before JavaScript runs.

That step is **Babel**.

---

## 2. The Critical Rule You Must Remember

> JSX must be transformed **before** the browser executes the JavaScript.

If JSX reaches the JavaScript engine:
- The browser crashes
- Execution stops
- Nothing renders

So:
- Babel must run first
- JavaScript runs second

Order matters.

---

## 3. What Babel Does in This Setup

In a no-bundler setup, Babel runs:
- In the browser
- At runtime
- Before JavaScript executes

Babel:
- Reads JSX
- Converts it to React.createElement
- Hands plain JavaScript to the browser

This is slower, but perfect for learning.

---

## 4. The Correct File Structure

You will have exactly two files:

- index.html
- index.js

No build folder.  
No config files.  
No installation.

---

## 5. index.html (The Controller File)

index.html controls:
- Script loading order
- Which tools run first

Here is the **correct index.html**:

    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="UTF-8" />
        <title>React JSX with CDN</title>
      </head>
      <body>
        <div id="root"></div>

        <!-- React -->
        <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
        <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>

        <!-- Babel -->
        <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

        <!-- Your JSX file -->
        <script type="text/babel" src="index.js"></script>
      </body>
    </html>

---

## 6. Why This Works (Very Important)

Let’s go line by line conceptually.

- React UMD loads first
- ReactDOM UMD loads next
- Babel loads next
- Babel intercepts index.js
- Babel transforms JSX
- Browser executes transformed JavaScript

The browser **never sees JSX**.

---

## 7. index.js (JSX Lives Here)

Now your JavaScript file can contain JSX.

index.js:

    const App = () => {
      return <h1>Hello JSX</h1>;
    };

    const root = ReactDOM.createRoot(
      document.getElementById("root")
    );

    root.render(<App />);

This works because:
- Babel transforms JSX
- React receives React elements
- ReactDOM renders to the DOM

---

## 8. Why JSX Cannot Live in a Normal .js File

If you wrote this instead:

    <script type="module" src="index.js"></script>

And index.js contained JSX:
- Browser tries to parse JSX
- Browser fails immediately
- Babel never runs

Because:
- type="module" means “execute immediately”
- Babel does not intercept module scripts

This is why JSX + ESM + no bundler is tricky.

---

## 9. Why We Did NOT Use ESM Here

In this setup:
- Babel needs control
- Babel only works with non-module scripts
- ESM bypasses Babel

So we temporarily sacrifice:
- import/export

To gain:
- JSX support
- Simplicity
- Learning clarity

---

## 10. Important Limitation of This Setup

This setup is for:
- Learning
- Experiments
- Understanding React

It is NOT for:
- Production apps
- Performance-sensitive apps
- Large codebases

Later, bundlers replace this runtime Babel step.

---

## 11. Mental Model to Lock In

Think of it like this:

- JSX is a **writing convenience**
- Babel is the **translator**
- React is the **UI engine**
- ReactDOM is the **browser renderer**

Without Babel:
- JSX cannot exist
