# Module Systems 

## 1. What Is a Module System?

A **module system** answers one simple question:

> How does one piece of code use another piece of code?

In other words:
- How do files share code?
- How do variables stay separate?
- How does JavaScript know what depends on what?

A module system defines:
- How code is loaded
- How code is isolated
- How code is reused

---

## 2. JavaScript Before Modules (The Old World)

Originally, JavaScript had **no module system**.

There was:
- No import
- No export
- No file boundaries

Everything lived in **one global space**.

---

## 3. Why Scripts Used to Be Global

### 3.1 How Scripts Worked

Old HTML looked like this:

    <script src="file1.js"></script>
    <script src="file2.js"></script>

What happened:
- file1.js runs
- file2.js runs
- Both share the same global scope

---

### 3.2 The Global Scope Problem

Because everything was global:
- Variables could overwrite each other
- Functions could collide
- Load order mattered a lot

Example problem:
- file1 defines `app`
- file2 also defines `app`
- One silently replaces the other

This caused:
- Random bugs
- Fragile code
- Fear of renaming variables

---

## 4. The Need for Modules

As apps grew larger, developers needed:
- Isolation
- Reusability
- Clear dependencies
- Predictable loading

So module systems were invented to:
- Avoid globals
- Control scope
- Explicitly share code

---

## 5. What Is UMD?

UMD stands for:

> Universal Module Definition

UMD was created to solve a **compatibility problem**.

---

### 5.1 The Problem UMD Solved

Different environments existed:
- Browsers
- Node.js
- Bundlers

Each used **different module formats**.

UMD tried to support **all of them** with one file.

---

### 5.2 How UMD Works (Conceptually)

A UMD file:
- Checks the environment
- Decides how to expose itself
- Falls back to globals if needed

In browsers:
- Libraries attach themselves to the window object

Example idea:

    window.React
    window.ReactDOM

This is how React worked for many years.

---

### 5.3 Characteristics of UMD

UMD:
- Uses script tags
- Exposes globals
- Does not use import/export
- Works almost everywhere

This made UMD very popular in the past.

---

## 6. The Limits of UMD

UMD solved compatibility, but:
- Polluted the global scope
- Had no static dependency graph
- Was hard to optimize
- Did not scale well for large apps

Developers wanted something better.

---

## 7. What Is ESM?

ESM stands for:

> ECMAScript Modules

This is the **official module system** built into JavaScript.

---

### 7.1 ESM Syntax

ESM introduces:
- import
- export

Example:

    import { something } from "./file.js";

Key difference:
- This is part of the JavaScript language itself

---

### 7.2 How ESM Changes Everything

With ESM:
- Each file has its own scope
- Nothing is global by default
- Dependencies are explicit
- Loading order is handled automatically

This is a **huge improvement**.

---

## 8. Why Browsers Needed type="module"

Browsers needed a way to:
- Distinguish old scripts
- Enable ESM behavior

That is why this exists:

    <script type="module" src="index.js"></script>

This tells the browser:
- Treat this file as a module
- Enable import/export
- Use strict mode automatically

---

## 9. What type="module" Changes

When you use type="module":
- Variables are scoped to the file
- import/export is allowed
- Code runs in strict mode
- Scripts load asynchronously by default

This is **not optional** for ESM in browsers.

---

## 10. UMD vs ESM (Simple Comparison)

UMD:
- Older
- Uses globals
- Script-tag based
- Compatibility-focused

ESM:
- Modern
- Uses import/export
- File-based
- Built into JavaScript

Both still exist, but ESM is the future.

---

## 11. Why React Supports Both

React provides:
- UMD builds for legacy usage
- ESM builds for modern usage

This allows:
- Old projects to keep working
- New projects to use modern tooling

You choose based on your setup.
