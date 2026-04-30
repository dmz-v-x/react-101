# React Keys — Gotchas

---

# 0. What This Lesson Is About

You already learned:

👉 Keys must be:
- unique  
- stable  

---

Now this lesson answers:

👉 Why **simple solutions (index, length)** are dangerous  
👉 What **real bugs** they cause  

---

---

# 1. Recap — What Keys Do

---

React uses keys to:

👉 Identify items in a list  

---

When React compares:

```
OLD LIST → NEW LIST
```

It uses:

```
key
```

---

👉 To match elements correctly  

---

---

# 2. The Temptation (Easy Solutions)

---

When you don’t have IDs, you might do:

---

## Option 1 — Index

```
key={index}
```

---

## Option 2 — Length

```
id: stickers.length
```

---

👉 Both seem correct  
👉 Both work in simple cases  

---

---

# 3. Why These Are Dangerous

---

They fail when:

- items are deleted  
- items are reordered  
- items are inserted in middle  
- items are filtered  

---

👉 These are VERY common real-world cases  

---

---

# 4. Problem 1 — Using Index as Key

---

## Example

```
["A", "B", "C"]
```

Keys:

```
0 → A  
1 → B  
2 → C  
```

---

## Now delete first item

```
["B", "C"]
```

New keys:

```
0 → B  
1 → C  
```

---

---

# 5. What React Thinks

---

React compares:

```
Old: 0 → A
New: 0 → B
```

---

👉 React thinks:

```
"A changed into B"
```

---

❌ WRONG  

---

---

# 6. What Actually Happened

---

👉 A was deleted  
👉 B moved up  

---

---

# 7. Resulting Bug

---

React does:

- Updates A → B  
- Updates B → C  
- Deletes last item  

---

👉 Completely wrong operations  

---

---

# 8. Real UI Bug Example

---

Input fields:

```
Alice
Bob
Charlie
```

---

Delete "Alice"

---

Now:

```
Bob
Charlie
```

---

👉 But UI shows:

```
Alice → Bob
Bob → Charlie
```

---

👉 Inputs shift incorrectly  

---

---

# 9. Why This Happens

---

Because:

👉 Index is NOT stable  

---

Indexes change when:

- delete  
- insert  
- reorder  

---

---

# 10. Problem 2 — Using Length as ID

---

```
id: stickers.length
```

---

## Example

Add 3 stickers:

```
0, 1, 2
```

---

Delete one:

```
0, 2
```

---

Add new:

```
length = 2 → id = 2
```

---

Now IDs:

```
0, 2, 2
```

---

❌ Duplicate keys  

---

---

# 11. Why Duplicate Keys Are Bad

---

React uses keys to:

👉 uniquely identify elements  

---

If duplicates:

👉 React gets confused  

---

👉 Updates wrong elements  

---

👉 Leads to unpredictable UI  

---

---

# 12. Important Rule

---

```
Keys must be UNIQUE
AND
Keys must be STABLE
```

---

---

# 13. What is Stable?

---

Stable means:

👉 Value does NOT change across renders  

---

---

# 14. Safe vs Unsafe Keys

---

## SAFE

```
id from database
uuid
email
slug
```

---

## UNSAFE

```
index
length
Math.random() in render
```

---

---

# 15. Special Case — When Index Is OK

---

Index is safe ONLY IF:

✔ List never changes  
✔ No insert/delete/reorder  
✔ Static list  

---

Example:

```
["Mon", "Tue", "Wed"]
```

---

👉 Fixed → safe  

---

---

# 16. Why This Is Still Risky

---

Because later you might:

- add sorting  
- add delete  
- add filter  

---

👉 And break everything  

---

---

# 17. Real Lesson Insight

---

Even experienced devs:

👉 Think index is safe  

---

👉 Later realize it's NOT  

---

---

# 18. Correct Solution (Best Practice)

---

👉 Generate ID when creating data  

---

```
const newItem = {
  ...data,
  id: crypto.randomUUID(),
}
```

---

Then:

```
key={item.id}
```

---

---

# 19. Why This Works

---

✔ Unique  
✔ Stable  
✔ Never changes  
✔ React tracks correctly  

---

---

# 20. Internal React Behavior

---

React builds mapping:

```
key → DOM node
```

---

If key changes:

👉 React destroys node  

---

If key stable:

👉 React reuses node  

---

---

# 21. Performance Impact

---

Bad keys cause:

❌ Full DOM re-creation  
❌ Slower UI  
❌ Flickering  

---

Good keys:

✔ Minimal updates  
✔ Fast UI  

---

---

# 22. Final Mental Model

---

## ❌ Index key

```
position-based identity
```

---

## ✔ ID key

```
identity-based identity
```

---

---

# 23. One-Line Understanding

---

👉 Index tells React "where", but keys should tell React "who".

---

---

# 24. Final Summary

---

✔ Index keys break when list changes  
✔ Length keys create duplicates  
✔ Keys must be unique + stable  
✔ Generate IDs when data is created  
✔ Never generate keys during render  
✔ Keys define identity, not position
