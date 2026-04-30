# Dynamic Key Generation in React

---

# 0. What This Lesson Is About

This lesson teaches:

👉 How to generate **unique keys when your data DOES NOT have IDs**

This is a **real-world problem** — happens very often.

---

# 1. First: Why Do We Even Need Keys?

Whenever you do:

```
items.map(item => <Component />)
```

React needs:

```
<Component key="something" />
```

---

## Why?

Because React must:

- Track items
- Compare old vs new
- Update efficiently

---

👉 Without keys → React gets confused  
👉 With keys → React works correctly  

---

---

# 2. The Problem Situation

---

You have:

```
const [stickers, setStickers] = useState([]);
```

---

When user clicks:

👉 A new sticker is created and added

---

```
const nextStickers = [...stickers, newSticker];
setStickers(nextStickers);
```

---

Then you render:

```
{stickers.map(sticker => (
  <img src={sticker.src} />
))}
```

---

❌ ERROR:

```
Warning: Each child in a list should have a unique "key"
```

---

---

# 3. Why This Is Hard

---

Normally:

```
item.id → use as key
```

---

But here:

❌ No id exists  
❌ Data is random  
❌ Items can repeat  

---

---

# 4. First Wrong Idea

---

## Using src as key

```
key={sticker.src}
```

---

❌ Problem:

Multiple stickers can have same image  

---

👉 Not unique → BAD  

---

---

# 5. Second Wrong Idea

---

## Using index

```
key={index}
```

---

❌ Problem:

- Index changes
- Causes bugs
- Breaks reconciliation

---

---

# 6. Third Wrong Idea (VERY COMMON)

---

## Using Math.random() inside render

```
key={Math.random()}
```

---

---

# 7. Why This Is VERY BAD

---

Every render:

👉 Math.random() gives new value  

---

So React sees:

```
Old keys: [0.1, 0.5, 0.9]
New keys: [0.7, 0.2, 0.3]
```

---

👉 React thinks EVERYTHING changed  

---

So it:

❌ Deletes all DOM nodes  
❌ Recreates all DOM nodes  

---

---

# 8. Why This Is a Big Problem

---

DOM operations are:

👉 VERY slow  

---

Instead of:

✔ Adding 1 element  

React does:

❌ Remove 10  
❌ Add 11  

---

---

# 9. The Core Idea (Correct Approach)

---

👉 Generate ID **once when item is created**

NOT during render  

---

---

# 10. Step-by-Step Fix

---

## Step 1 — Inside click handler

```
onClick={(event) => {
```

---

## Step 2 — Create new sticker

```
const newSticker = {
  ...stickerData,
  x: event.clientX,
  y: event.clientY,
```

---

## Step 3 — Add unique ID

```
  id: crypto.randomUUID(),
};
```

---

👉 This happens ONLY ONCE  

---

---

## Step 4 — Save in state

```
setStickers([...stickers, newSticker]);
```

---

---

## Step 5 — Use key

```
{stickers.map(sticker => (
  <img key={sticker.id} ... />
))}
```

---

---

# 11. Why This Works Perfectly

---

Now:

✔ Each sticker has stable ID  
✔ ID never changes  
✔ React can track items  

---

👉 Efficient updates  

---

---

# 12. Important Concept: “Stable Keys”

---

A key must be:

✔ Unique  
✔ Stable (does NOT change)  

---

---

# 13. What is “Stable”?

---

❌ Changes every render → BAD  
✔ Same across renders → GOOD  

---

---

# 14. Alternative ID Methods

---

## Option 1 — crypto.randomUUID()

✔ Best  
✔ Unique  
✔ Modern  

---

## Option 2 — Math.random() (ONLY ONCE)

```
id: Math.random()
```

✔ Works  
❌ Less reliable  

---

## Option 3 — Counter

```
let id = 0;
id++;
```

✔ Works  
✔ Simple  

---

---

# 15. Full Final Code (Clean)

---

```
function StickerPad() {
  const [stickers, setStickers] = React.useState([]);

  return (
    <button
      onClick={(event) => {
        const stickerData = getSticker();

        const newSticker = {
          ...stickerData,
          x: event.clientX,
          y: event.clientY,
          id: crypto.randomUUID(),
        };

        setStickers([...stickers, newSticker]);
      }}
    >
      {stickers.map((sticker) => (
        <img
          key={sticker.id}
          src={sticker.src}
          alt={sticker.alt}
          style={{
            left: sticker.x,
            top: sticker.y,
          }}
        />
      ))}
    </button>
  );
}
```

---

---

# 16. Deep Internal Understanding

---

React does:

```
oldList vs newList
```

---

Using keys:

```
key → match items
```

---

Without keys:

👉 React guesses → WRONG  

---

With stable keys:

👉 React matches correctly  

---

---

# 17. What This Lesson Teaches

---

✔ Keys must be unique  
✔ Keys must be stable  
✔ Never generate keys during render  
✔ Generate keys when creating data  

---

---

# 18. Final Mental Model

---

Think:

---

## ❌ Wrong

```
key = random every render
```

👉 React: “Everything changed!”

---

## ✔ Correct

```
key = fixed ID stored in data
```

👉 React: “Only new item added”

---

---

# 19. One-Line Summary

---

👉 Keys should be generated once when data is created, not during rendering, so React can correctly track and update elements efficiently. 
