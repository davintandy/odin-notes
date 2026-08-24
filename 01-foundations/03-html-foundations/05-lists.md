# Lists

Lists are used to group related pieces of info. In HTML, the choice of tag depends on whether the **sequence** of items is important.

---

## Unordered lists (`<ul>`)

Use these for collections where the order is flexible (e.g., a shopping list or a list of hobbies).

- **Tag:** `<ul>` (Unordered List).
- **Marker:** Displays with **bullet points** by default.

```html
<ul>
  <li>Milk</li>
  <li>Eggs</li>
  <li>Bread</li>
</ul>
```

---

## Ordered Lists (`<ol>`)

Use these for items that follow a specific sequence (e.g., recipe steps or a “Top 10” ranking).

- **Tag:** `<ol>` (Ordered List).
- **Marker:** Displays with **numbers** (1, 2, 3…) by default.

```html
<ol>
  <li>Preheat the oven.</li>
  <li>Mix the ingredients.</li>
  <li>Bake for 20 minutes.</li>
</ol>
```

---

## Comparison at a Glance

| **Feature** | **Unordered List (`<ul>`)** | **Ordered List (`<ol>`)** |
| --- | --- | --- |
| **Logic** | Items can be in any order. | Items follow a sequence. |
| **Visual** | Bullet points. | Numbers or Letters. |
| **Child Tag** | Always `<li>`. | Always `<li>`. |