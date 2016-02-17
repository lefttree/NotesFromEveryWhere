# CSS Review

## CSS Cascading Priority

1. inline style
2. External and internal style sheets
3. browser default

## Properties

### color

valid color name like "red", rgb(255,0,0), hex value like "#ff0000"

### background

- background-color
- background-image
    + by default if repeated(both vertically and horizontally)
- background-repeat
    + repeat-x: horizontally
    + repeat-y: vertically
- background-attachment
    + fixed, background image will not scroll with the page
- background-position
    + set the position like background image

### border

- border-style
- border-width
- border-color

shorthand property `border: 5px solid red`

### margin

generate space around **elements**, outside the border

top, right, bottom, left ---- clock-wise

### padding

generate space around **content**, between content and border

similar as margin

### dimension

- height
- width

can be `px`, `cm` ... or in `%`

- max-width
- min-width
- max-height
- min-height

### text

- color
- text-align
    + center
    + left
    + right
    + justify(each is stretched so that every line has equal width)
- text-decoration
    + underline
    + overline
    + e.g `none` remove underlines from links
- text-transform
    + uppercase
    + lowercase
- text-indentation(first line)
- letter-spacing
- line-height
- direction
- word-spacing
- vertical-align

### fonts

- font-family
- font-style
- font-size
    +_px
    + em
- font-weight
- font-variant

### links

- a:link
- a:visited
- a:hover
- a:active

`a:hover` must come after `a:link` and `a:visited` to be effective

- text-decoration
- background-color

### lists

- `list-style-type` specifies the type of list item marker
- `list-style-image`
- `list-style-position`
- `list-style` can be none to remove any style

### tables

```
table, th, td {
    border: 1px solid black;
}
```

- `border-collapse` set whether the border should be collapsed into a single border
- width
- height
- text-align
- vertical-align
- padding

#### Horizontal Dividers

```
th, td {
    border-bottom: 1px solid #ddd;
}

```

#### hoverable 

`tr:hover {background-color: #f5f5f5}`

#### striped tables

use `nth-child()`

`tr:nth-child(even) {background:#f2f2f2}`

#### responsive

`overflow-x:auto`

others

- table-layout: auto, fixed(faster), initial, inherit
- empty-cells
- caption-side

## CSS Box Model

All elements can be considered as boxes.

![box-model](http://www.w3schools.com/css/box-model.gif)


- Content - The content of the box, where text and images appear
- Padding - Clears an area around the content. The padding is transparent
- Border - A border that goes around the padding and content
- Margin - Clears an area outside the border. The margin is transparent

The total width of an element should be calculated like this:

Total element width = width + left padding + right padding + left border + right border + left margin + right margin

## CSS Outline

An outline is a line drawn aroudn an element - **outside the border**.

- outline-width
- outline-style
- outline-color
- outline-offset

## display

default value for most elements is `block` or `inline`, depends on what type of 
elment it is.

### block-level elements

always start on a new line and takes up the full width available

### inline elements

only takes up as much width as necessary
