# Introduction to Flexbox

## The Core Hierarchy

Flexbox logic relies on a parent-child relationship.

### The Flex Container

Any HTML element becomes a **Flex Container** as soon as you apply `display: flex;` to it. This “unlocks” Flexbox properties for that specific section of the page.

### The Flex Items

Any elements that is a **direct child** of a Flex Container automatically becomes a **Flex Item**.

Only the immediate children are affected. Grandchildren are not “flexed” unless their parent is also turned into a container.

---

## Flexbox “Inception” (Nesting)

A single element is not restricted to one role. You can turn a **Flex Item** into a **Flex Container** by adding `display: flex;` to it.

This allows you to use Flexbox to position a component on the page, and then use Flexbox again to arrange the contents inside that component.