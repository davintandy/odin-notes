# The Cascade

When CSS rules conflict, the browser runs them through four distinct levels of “authority” to pick a winner.

---

## Importance & Origin

Before looking at your classes or IDs, the browser checks **where** the rule came from and its **priority type**.

- **Transitions & Animations:** Rules currently animating take the highest priority to ensure smooth motion.
- `!important`: The “Hail Mary.” It overrides almost everything else. Use it only when fighting third-party libraries you can’t control.
- **Origin:**
    1. **Website (Author):** The CSS you write.
    2. **User:** Custom browser settings set by the person viewing the site.
    3. **Browser (User Agent):** The default styles (why links are blue and buttons have gray borders by default).

---

## Specificity (The Point System)

If the Importance and Origin are a tie, the browser calculates **Specificity**. It’s a point-based system: the more specific the selector, the more weight it carries.

| **Level** | **Selector Type** | **Example** |
| --- | --- | --- |
| **Highest** | **Inline Styles** | `<p style="color: red">` |
| **High** | **ID Selectors** | `#header` |
| **Medium** | **Class / Attribute / Pseudo** | `.btn`, `[checked]`, `:hover` |
| **Low** | **Type / Pseudo-element** | `div`, `p`, `::before` |
| **Zero** | **Universal / Combinators** | `*`, `>`, `+`, `~` |

### Specificity Rules

- **ID beats Class:** One ID (`#title`) beats a thousand classes (`.big.red.bold…`).
- **Quantity Matters:** If the highest-reached levels are the same, the rule with **more** of those selectors wins.
    - `.nav .link` beats `.link`.
- **Combinators don’t count:** `.parent .child` has the same weight as `.parent.child` (both are just 2 classes).

---

## Inheritance (The “DNA” Factor)

Some properties are passed from parent to child automatically.

- **Inherited:** Typography properties (`color`, `font-family`, `text-align`).
- **Not Inherited:** Layout properties (`margin`, `padding`, `border`, `background`).

### Direct Targeting Wins

A direct selector **always** beats an inherited value, regardless of specificity.

```css
#parent {
	color: red;
}

p {
	color: blue;
}

/* Result: The paragraph is BLUE. */
```

---

## Cascade Layers (`@layer`)

Modern CSS allows you to group styles into explicit layers. Layers defined later in the code take precedence over earlier layers, but **unlayered styles** always beat layered styles to maintain backward compatibility.

```css
@layer base, theme;

@layer base {
	h1 {
		color: red;
	}
}

@layer theme {
	h1 {
		color: blue;
	}
}

/* Result: Blue wins (theme is defined after base) */
```