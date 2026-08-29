# HTML-CSS 
HTML and CSS are the basic technologies used to create webpages. HTML provides the structure of a webpage, while CSS controls its layout, appearance, and responsiveness.

## BOX-MODEL
Everything in CSS has a box around it, and understanding these boxes is key to being able to create more complex layouts with CSS, or to align items with other items. 

Every element consists of four main parts:
``` 
    Content
    Border
    Margin
    Padding 
```
A simple example:

#### CSS
```
.card {
    width: 200px;
    padding: 20px;
    border: 2px solid black;
    margin: 10px;
}

```
The content is the actual text or other elements inside the box. Padding creates space between the content and border. Border surrounds the content and padding. Margin creates space outside the border.

The default box model is content-box, where width applies to the content area.

If we assume that a box has the following CSS:

#### CSS

```
.box {
  width: 350px;
  height: 150px;
  margin: 10px;
  padding: 25px;
  border: 5px solid black;
}
```
The actual space taken up by the box will be 410px wide (350 + 25 + 25 + 5 + 5) and 210px high (150 + 25 + 25 + 5 + 5).

In the alternative box model, any width is the width of the visible box on the page. The content area width is that width minus the width for the padding and border . This is convenient as there is no need to add up the border and padding to get the real size of the box. Just use this command box-sizing: border-box.

#### CSS

```
.box {
  box-sizing: border-box;
  width: 350px;
  height: 150px;
  margin: 10px;
  padding: 25px;
  border: 5px solid black;
}

```
The actual space taken up by the box will now be 350px in the inline direction and 150px in the block direction.

## Inline and Block Elements
HTML elements have different default display behaviors. The two basic types are block and inline elements.

### Block element
A block element normally starts on a new line and takes the available width of its container.

#### HTML
```
<div>Content</div>
```
#### CSS
```
div {
    display: block;
}
```
Block elements normally respect width and height.

### Inline Elements
An inline element normally stays within the current line of text.

Example:
#### HTML
```
<span>Text</span>
<a href="#">Link</a>
<strong>Important</strong>
<em>Emphasis</em>
```
For an inline element, width and height normally do not apply in the same way as they do to block elements.

### Inline Block
inline-block combines some behavior of both:

#### CSS
```
.box {
    display: inline-block;
    width: 150px;
    height: 100px;
}
```

The elements can remain on the same line while still accepting width and height.

## Positioning: Relative and Absolute
CSS positioning controls where an element is placed.

### Relative positioning

#### CSS
```
.box {
    position: relative;
    top: 10px;
    left: 20px;
}
```
The element is first placed in its normal position and then visually moved from that position.

### Absolute positioning

#### CSS
```
.card {
    position: relative;
}

.icon {
    position: absolute;
    top: 10px;
    right: 10px;
}
```
Here, .icon is positioned relative to the .card because .card establishes the relevant positioning context.

An absolutely positioned element is removed from the normal document flow. Therefore, it can overlap other elements.

Positioning should generally be used when necessary, such as for badges, icons, overlays, and other elements that need to overlap.

## Common CSS structural classes
Structural classes describe the role or layout of an element rather than its visual appearance.

For example:
#### HTML
```
<header class="header">
    ...
</header>

<nav class="navigation">
    ...
</nav>

<main class="main-content">
    ...
</main>

<section class="student-section">
    ...
</section>

<footer class="footer">
    ...
</footer>
```

CSS can then define their layout:

#### CSS
```
.navigation {
    display: flex;
    justify-content: space-between;
}

.student-section {
    display: grid;
    gap: 1rem;
}
```
The idea is to keep layout responsibilities separate from styling where practical.

This makes the CSS easier to reuse and maintain.

## Common Styling Classes
Styling classes are used to control the appearance of elements.

For example:
#### CSS
```
.text-center {
    text-align: center;
}

.rounded {
    border-radius: 10px;
}

.highlight {
    background-color: yellow;
}

.text-white {
    color: white;
}
```

They can be applied to different elements:

#### HTML
```
<p class="text-center">Hello</p>

<div class="rounded highlight">
    Important information
</div>
```

## CSS Specificity
Sometimes multiple CSS rules target the same element. CSS specificity determines which rule has priority when declarations conflict.

For example:
#### HTML
```
<p id="message" class="text">Hello</p>
```

#### CSS
```
p {
    color: black;
}

.text {
    color: blue;
}

#message {
    color: red;
}
```
The ID selector has higher specificity than the class and element selectors, so the text becomes red.

A simple order to remember is:
- Inline style
- ID selector 
- Class  or Attribute or Pseudo class
- Element selector


## CSS Responsive Queries
A responsive webpage changes its layout according to the available screen size or other device conditions.

CSS media queries are used for this purpose.
#### CSS

```
.students {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
}

@media (max-width: 600px) {
    .students {
        grid-template-columns: 1fr;
    }
}
```
A common approach is to design for smaller screens first and then add styles for larger screens.

## CSS Flexbox
Flexbox is mainly used for arranging elements in one dimension: either a row or a column.

#### CSS
```
.navigation {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
```
#### HTML
```
<nav class="navigation">
    <h2>Logo</h2>

    <div class="menu">
        <a href="#">Home</a>
        <a href="#">About</a>
        <a href="#">Profile</a>
    </div>
</nav>
```
Flexbox is useful for navigation bars, menus, rows of cards, and aligning items.

## CSS GRID
Grid is useful for two-dimensional layouts involving rows and columns.

#### CSS
```
.students {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
}
```
Important Grid properties include:
```
display: grid
grid-template-columns
grid-template-rows
gap
grid-column
grid-row
```
Grid is useful for page layouts, galleries, dashboards, and card collections.

## In-flow and Out-of-flow Elements
In normal document flow, elements take their normal space and affect the position of other elements.

#### HTML
```
<div>Box 1</div>
<div>Box 2</div>
```
If Box 1 becomes taller, Box 2 is moved down.

Elements using normal flow, Flexbox, and Grid generally participate in the page's layout.

Some positioning methods remove elements from normal flow.Example absolute,fixed positioning.

## Common Meta Tags in HTML
Metadata is placed inside the <head> element. It provides information about the document to the browser and other software.

#### HTML
```
<meta charset="UTF-8">
```
It specifies the character encoding used by the document.

#### HTML
```
<meta
    name="viewport"
    content="width=device-width, initial-scale=1.0"
>
```
This is important for responsive webpages because it sets the viewport behavior on mobile devices.

In this way other metatag like title,description.The title identifies the webpage and is commonly displayed in the browser tab and used in search results.

## CSS Units
CSS units are used to specify sizes such as font size, padding, margin, and width.

Common units include:
```
px
%
em
rem
vh
vw
```
Within these some are absolute unit and some are relative units. Absolute unit like px and relative units like %,em,rem,vh,vw. Relative units are help to achieve responsive page.


## References
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Display/Block_and_inline_layout

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Display/Visual_formatting_model
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Flexible_box_layout

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Media_queries

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/meta

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Values_and_units


