# Elements and Tags

Most of what you see on a webpage consists of content wrapped in **HTML tags**. These tags act as containers that tell the browser how to format and display your information.

---

## Anatomy of an Element

An **element** is the complete package: the opening tag, the content, and the closing tag.

```html
<p>This is my content!</p>
```

- **Opening Tag (`<p>`):** Tells the browser where the element starts.
- **Content:** The actual text or data being displayed.
- **Closing Tag (`</p>`):** Tells the browser where the element ends (always include a `/`).

**The “Container” Analogy:** Think of tags as a box and the content as the item inside. The tags describe what’s in the box so the browser knows how to handle it.

---

## Semantic HTML

HTML has hundreds of predefined tags. Choosing the **right** one for the job is called **Semantic HTML**.

**Why it matters:**

1. **SEO:** Search engines use tags to understand what your site is about.
2. **Accessibility:** Screen readers rely on correct tags (like `<h1>` for headings or `<button>` for actions) to help visually impaired users navigate.

---

## Void Elements

Some elements are “loners” - they don’t have a closing tag because they don’t wrap any content. These are called **Void Elements** (or sometimes “Self-Closing Tags”).

- **Common Examples:** `<br>` (line break) or `<img>` (image).
- **Note on Syntax:** You might see them written as `<br />`. While browsers still read this, the modern HTML spec prefers the cleaner `<br>` and considers the extra slash unnecessary.