# Lists

## What Are HTML Lists?

HTML lists organize related items into a structured and readable format. They are commonly used for shopping lists, instructions, rankings, navigation menus, and other collections of information.

HTML provides two main types of lists:

- **Unordered lists**: Used when the order of items does not matter.
- **Ordered lists**: Used when the order of items matters.

## Unordered Lists

An **unordered list** displays items with bullet points. Use it when the items do not need to follow a particular sequence.

### Elements Used

- `<ul>` - Defines an unordered list.
- `<li>` - Defines an individual list item.

### Syntax

```html
<ul>
	<li>Apples</li>
	<li>Bananas</li>
	<li>Oranges</li>
</ul>
```

The browser typically renders this as:

- Apples
- Bananas
- Oranges

### When to Use Unordered Lists

Use unordered lists for collections where changing the order does not affect the meaning, such as:

- Shopping lists.
- Favorite foods.
- Hobbies and interests.
- Places you want to visit.

## Ordered Lists

An **ordered list** displays items in a sequence, typically using numbers. Use it when the order of items is important.

### Elements Used

- `<ol>` - Defines an ordered list.
- `<li>` - Defines an individual list item.

### Syntax

```html
<ol>
	<li>Wake up</li>
	<li>Have breakfast</li>
	<li>Start working</li>
</ol>
```

The browser typically renders this as:

1. Wake up
2. Have breakfast
3. Start working

### When to Use Ordered Lists

Use ordered lists for information that follows a specific sequence or ranking, such as:

- Step-by-step instructions.
- Recipes.
- Daily to-do lists.
- Top-five rankings.

## Understanding `<ul>`, `<ol>`, and `<li>`

| **Element** | **Purpose** |
| --- | --- |
| `<ul>` | Groups items into an unordered list |
| `<ol>` | Groups items into an ordered list |
| `<li>` | Defines an individual item within a list |

Both `<ul>` and `<ol>` contain their list items using `<li>` elements.