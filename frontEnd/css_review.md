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
