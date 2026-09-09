# Tables

## Core Concept & Usage

HTML table (`<table>`) displays **tabular data** - information structured in a grid of rows and columns where data points cross-reference each other (e.g., financial sheets, product comparisons, schedules).

### Tabular Data vs. Page Layout

| **Feature** | **Tabular Data (`<table>`)** | **Page Layout (Flexbox / CSS Grid)** |
| --- | --- | --- |
| **Primary Purpose** | Displaying relational, multi-variable data | Structural UI layout (sidebars, navbars, cards) |
| **Accessibility** | Screen readers auto-associate cells with headers | Table layouts break accessibility tree traversal |
| **Maintainability** | Clean, semantic data markup | Complex, nested “tag soup” |
| **Responsiveness** | Content-sized; requires scroll wrappers | Fluid, inherently responsive |

> **Anti-Pattern:** Never use `<table>` for page layouts. Use modern CSS (Flexbox and CSS Grid) for layout design.
> 

## Table Elements & Semantic Structure

A fully structured, accessible table uses structural wrappers, header controls, and a caption.

### Element Summary

| **Element** | **Description** |
| --- | --- |
| `<table>` | Container element for all tabular data |
| `<caption>` | Accessible title/description of the table. Must be placed directly after `<table>` |
| `<thead>` | Wraps header row(s) (`<th>`). Essential for styling and multi-page print repeating |
| `<tbody>` | Wraps primary table data rows (`<tr>`). Implicitly added by browser engines if omitted |
| `<tfoot>` | Wraps summary/footer row(s) (e.g., total rows) |
| `<tr>` | Table row container |
| `<th>` | Header cell (bold and centered by default) |
| `<td>` | Standard data cell |

### Complete Semantic Example

```html
<table>
	<caption>Monthly Expense Record</caption>
	<thead>
		<tr>
			<th scope="col">Purchase</th>
			<th scope="col">Location</th>
			<th scope="col">Date</th>
			<th scope="col">Cost ($)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th scope="row">Haircut</th>
			<td>Salon</td>
			<td>12/09</td>
			<td>30</td>
		</tr>
		<tr>
			<th scope="row">Shoes</th>
			<td>Store</td>
			<td>13/09</td>
			<td>65</td>
		</tr>
	</tbody>
	<tfoot>
		<tr>
			<th scope="row" colspan="3">Total</th>
			<td>95</td>
		</tr>
	</tfoot>
</table>
```

## Cell Spanning (`colspan` & `rowspan`)

Attributes used on `<th>` or `<td>` to stretch a single cell across multiple rows or columns.

| **Attribute** | Behavior | **Typical Use Case** |
| --- | --- | --- |
| `colspan="N"` | Merges cell horizontally across N columns | Grouped column headers or summary total cells |
| `rowspan="N"` | Merges cell vertically across N rows | Grouping multiple rows under a single category |

```html
<table>
	<thead>
		<tr>
			<!-- Spans 2 columns -->
			<th colspan="2">Classification</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<!-- Spans 2 rows vertically -->
			<th rowspan="2">Equine</th>
			<td> Mare (Female)</td>
		</tr>
		<tr>
			<td>Stallion (Male)</td>
		</tr>
	</tbody>
</table>
```

## Column Grouping (`<colgroup>` & `<col>`)

Target and style entire vertical columns directly without applying duplicate CSS classes to every single `<td>`. Must be placed before `<thead>` or `<tr>`.

```html
<table>
	<colgroup>
		<col span="2" /> <!-- Columns 1-2: Default style -->
		<col class="col-highlight" /> <!-- Column 3: Custom highlight -->
		<col class="col-accent" /> <!-- Column 4: Custom accent -->
	</colgroup>
	<thead>
		<tr>
			<th>ID</th>
			<th>Item</th>
			<th>Price</th>
			<th>Status</th>
		</tr>
	</thead>
	<!-- Row content -->
</table>
```

```css
.col-highlight {
	background-color: #e6f4ea;
}

.col-accent {
	background-color: #fce8e6;
	border-left: 2px solid #ea4335;
}
```

## Accessibility & Header Associations

Screen readers need explicit associations between headers (`<th>`) and data cells (`<td>`). Choose between two approaches:

### The `scope` Attribute (Recommended)

Simplest and best method for 95% of tables. Use the `scope` attribute on `<th>` elements.

| **`scope` Value** | **Use Case** | **Example** |
| --- | --- | --- |
| `col` | Standard column header | `<th scope="col">Price</th>` |
| `row` | Standard row header | `<th scope="row">Item 1</th>` |
| `colgroup` | Header spanning multiple columns | `<th colspan="3" scope="colgroup">Clothes</th>` |
| `rowgroup` | Header spanning multiple row groups | `<th rowspan="2" scope="rowgroup">Europe</th>` |

### Example: Grouped Headers with `scope`

```jsx
<thead>
	<tr>
		<th colspan="2" scope="colgroup">Clothes</th>
	</tr>
	<tr>
		<th scope="col">Shirts</th>
		<th scope="col">Pants</th>
	</tr>
</thead>
<tbody>
	<tr>
		<th rowspan="2" scope="rowgroup">Store A</th>
		<td>15</td>
		<td>20</td>
	</tr>
</tbody>
```

### `id` and `headers` Attributes (Complex Tables)

Used for multi-level, non-standard matrices where `scope` cannot cleanly define relationships.

1. Assign a unique `id` to every `<th>`.
2. On sub-headers or `<td>` cells, add a space-separated list of corresponding header `id`s in the `headers` attribute.

```jsx
<thead>
	<tr>
		<th id="clothes" colspan="2">Clothes</th>
	</tr>
	<tr>
		<th id="shirts" headers="clothes">Shirts</th>
		<th id="pants" headers="clothes">Pants</th>
	</tr>
</thead>
<tbody>
	<tr>
		<th id="region-a">Region A</th>
		<td headers="region-a clothes shirts">120</td>
		<td headers="region-a clothes pants">85</td>
	</tr>
</tbody>
```

> **Note:** `id` and `headers` require significant manual maintenance and are error-prone. Use `scope` whenever possible.
>