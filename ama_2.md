# HTML & CSS Quick Questions

## 1. What are `<br>` and `<hr>` tags?

    <br> creates a line break (moves content to next line).
    <hr> creates a horizontal line used to separate sections.
    Both are empty/self-closing tags and do not need closing tags.

## 2. Explain the `<style>` tag.

    The <style> tag is used to write CSS directly inside an HTML file.
    It is usually placed inside the <head> section.
    Example:
    <style>
    p { color: red; }
    </style>

## 3. Different ways to select an element in CSS

    1. Element selector → p { }
    2. Class selector → .className { }
    3. ID selector → #idName { }
    4. Attribute selector → input[type="text"] { }
    5. Universal selector → * { }

## 4. Explain `:hover`

    :hover is a CSS pseudo-class.
    It applies styles when the mouse pointer moves over an element.
    Example:
    button:hover { background: blue; }

## 5. Stroke in HTML

    HTML itself does not have stroke for text.
    Stroke is usually applied using CSS or SVG.
    Example:
    -webkit-text-stroke: 1px black;

## 6. Types of CSS

    1. Inline CSS → inside HTML tag
    2. Internal CSS → inside <style> tag
    3. External CSS → separate .css file linked to HTML

## 7. Relative, Absolute, Fixed Position

    relative → positioned relative to its normal position.
    absolute → positioned relative to the nearest positioned parent.
    fixed → positioned relative to the browser window and stays during scroll.

## 8. Translate in HTML/CSS

    translate is a CSS transform function.
    It moves an element from its current position.
    Example:
    transform: translate(50px, 20px);

## 9. Difference between Flexbox and Grid

    Flexbox → one-dimensional layout (row OR column).
    Grid → two-dimensional layout (rows AND columns).
    Flexbox is good for small layouts, Grid for full page layouts.

## 10. What is `justify-content`?

    justify-content aligns items along the main axis.
    Used in flexbox or grid containers.
    Example values:
    center, space-between, space-around, flex-start, flex-end

## 11. Explain CSS Grid

    CSS Grid is a layout system for rows and columns.
    It allows precise placement of elements.
    Example:
    display: grid;
    grid-template-columns: 1fr 1fr;

## 12. Clamp function in CSS

    clamp() sets a value between a minimum and maximum.
    Syntax:
    clamp(min, preferred, max)
    Example:
    font-size: clamp(16px, 2vw, 24px);

## 13. Different types of meta tags

    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="page info">
    <meta name="keywords" content="html, css">

## 14. Link an external CSS file to HTML

    Use the <link> tag inside the <head> section.
    Example:
    <link rel="stylesheet" href="styles.css">

## 15. Change visibility of an image

    Use CSS properties:

    visibility: hidden;  (hides but keeps space)
    display: none;       (removes from layout)

    Example:
    img { visibility: hidden; }
