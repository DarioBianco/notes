

## Section 1: 

#### 2. Install Visual Studio Code Extensions

Extensions are like plugins that extend the functionality of VSCode. Here are the ones that I've installed. Click on the link and then click on the "install" button and it should automatically install it in your VSCode application.

[Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server)

[Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

[vscode-icons](https://marketplace.visualstudio.com/items?itemName=vscode-icons-team.vscode-icons)

[DigitalBrainstem.javascript-ejs-support](https://marketplace.visualstudio.com/items?itemName=DigitalBrainstem.javascript-ejs-support)

## Section 4: Multi-Page Websites

​    To auto generate a boilerplate HTML file in VS Code:
​     - Save a file as an html file
​     - Type "!" at the beginning of the empty file, and VS Code will suggest a boilerplate auto-completion.

## Section 5: Introduction to CSS

#### Inline CSS:

​	        Use for a single element.
​        `<html style="background: blue"></html>`

#### Internal Style Tag:

​    Use for a single webpage.
​    CSS within style tags.
​    html, within the style tags, is called a selector.
​    The style tags may be anywhere in the document and will apply styling to a page regardless of where they are placed

```html
<html>
    <head>
        <style>
            html {
                background: red;
            }
        </style>
    </head>
<html>
```

#### External CSS:

​    Use for an entire website.
​    CSS lives in a separate CSS file.

```html
<html>
    <head>
        <link>
            rel="stylesheet"
            href="./styles.css"
        </link>
    </head>
<html>
```

### Selectors   

#### Class Selector:

​    .<class name>

#### Id Selector:

​    #<Id name>

#### Attribute Selector:

​    Allows you to apply styles to attributes of selectors.

```css
/* Select all paragraph elements with the  attribute "draggable" and apply this CSS style to it*/
p[draggable]{
    color: red;
}

/* Select all paragraph elements with the attribute "draggable", where the draggable values is "false", and apply this CSS style to it.*/
p[draggable="false"]{
    color: red;
}

/* Select the 4th list element in all lists and apply a CSS style to it.*/
li[value="4"]{
    color: red;
}
```

#### Universal Selector:

​    A way to select and apply a style to all elements.

```css
* {
    color:red;
}
```



## Section 6 - CSS Properties: 

ColorHunt.co

An '**em**' is a relative sizing unit (relative to the parent unit's font size)
    1em * 100% of the width of the letter 'm' of the parent tag's font size.
    The letter 'm' is the widest in the alphabet.

​	The h1 font size in the following would be 20 pts:

```html
<body style:"font-size=20pt">
    <h1 style="font-size:1em">hellai</h1>
</body>
```

​	The h1 font size in the following would be 40 px:

```html
<body style:"font-size=20px">
    <h1 style="font-size:2em">hellai</h1>
</body>
```

An '**rem**' is similar to an 'em', but it's size is relative to the 
font-size of the root of the file rather than to a parent tag's font-size.
    The root element is normally the html tag.

font-weight:

- bold
- lighter: Lighter than parent
- bolder: bolder than parent
- number: 100-900

font-family: Some computers don't have certain typefaces (e.g., Helvetica), 
    so a family is specified (e.g., sans-serif, cursive, fantasy).

```css
h1{
    font-family: Helvetica, sans-serif
}
h2{
    font-family: "Times New Roman", sans-serif
}
```

Custom free fonts: 
    [fonts.google.com](fonts.google.com)
    To embed a font from Google Fonts, copy the code into the <head> of your html.

​        E.g.,   For a Regular 400 sized Roboto font:        

```html
<!-- Add to <head> of your html: -->
<head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
</head>
```

```css
/*Add to CSS:*/
font-family: 'Roboto', sans-serif;
```

Box Model


```css
Border: 10px solid black
```

**Pesticide** Chrome Browser Plug-in - Helps visualize div boundaries during development.



------

## Section 7 - Intermediate CSS

### Level of importance of a CSS Rule:

1) Position : Appears higher or lower relative to other rules.

   ```css
   /*Later rules overrule previous rules, so the applied color would be blue.*/
   li {
   	color: red;
   	color: blue;
   }
   ```

2) Specificity: 

   ```css
   <li id="first-id" class="first-class" draggable>
   ```

   ```css
   /* Listed from least to most specific:
   	element, class, attribute, id
   */
   li {color: blue}
   .first-class{color: red}
   /* Attibute rules will usually override class rules, even though they are technically at the same level of specificity.*/
   li[draggable]{color: purple}
   #first-id{color: orange}
   
   /*The li text would be orange.*/
   ```

3) Type:

   1) External Styles (Will be applied first.)
   2) Internal Styles
   3) In-line Styles (Final. Will be applied last.)

   ```css
   /* Will be applied First */
   <link rel="stylesheet" href="./style.css">
   /* Will be applied next. */
   <style></style>
   /* Will be applied last & override previous rules. */
   <h1 style="">Hello</h1>
   ```

4) Importance

   ```css
   /* The important keyword will apply a rule for the property. Position, specificity, and type rules will be overridden for important parameters.
   */
   li {
       color: red;
       color: green !important;
   }
   ```


### Combining CSS Selections

#### Group Selection

```css
#my-id, h2, .my-class {
  color: blueviolet;
}
```

#### Child Selection

Use the right-angle bracket, >, to select a child of another selector. The child must be a **direct** child/descendant.

```css
parent_selector > child_selector {
    color: firebrick;
}
```

#### Descendant Combination Selection

Applies a rule to any descendants that have the specified ancestor, regardless of how many generations/levels removed.

```css
ancestor_selector descendant_selector {
    color: firebrick;
}
```

#### Chaining Selectors

Applies a style where all selectors are true.

```css
selectorselector {
    color:seagreen;
}
```

Example:

```html
<h1 id="title" class="big heading">
    Hello World
</h1>
```

```css
h1#title.big.heading {
    color:seagreen;
}
```

#### All above selection methods may be combined.

Example:

```css
/* Descendant Selection + Chained selection */
selector selectorselector {
    font-size: 2rem;
}
```



### CSS Positioning

**Static Positioning**: Default positioning method. "Elements with position: static are positioned based on the normal flow of the page, as you would expect them to be without any CSS styling" (https://blog.hubspot.com/website/css-position#:~:text=sticky-,static,%2C%20bottom%2C%20or%20left%20properties.)

**Relative positioning**: Positioning relative to where the element would normally have been positioned.

**Absolute Positioning**: Position relative to the nearest *positioned* ancestor or top-left corner of webpage. (The position attribute needs to be specified for the ancestor for absolute positioning to be applied based on that ancestor. Otherwise, the element will be positioned based on the top-left corner of the page.)

​	**Z-index**: Determines which elements go on top of which. A higher indexed element rests above lower indexed elements. The default z-index is 0. Adding absolute positioning moves the element to a different layer, and outside of the page's standard flow. Setting the z-index of an absolutely positioned element allows the element to be positioned behind element having a default position and z-index.

**Fixed Positioning**: Positioning relative to the browser's top-left position, regardless of scrolled position on the page.



------



## Section 8: Advanced CSS

### CSS Display

https://appbrewery.github.io/css-display/

#### Block Display

Block elements will take up the **entire** width of their containers, regardless of the  width to which an element is set.

```html
<!-- 
Each element is displayed on a new line by default
because the default display type is 'block'.
-->
<p>block</p>
<p style="width: 200px;">block</p>
<p>block</p>
```



<p style="background-color:gray; text-align:center">block</p>
<p style="background-color:gray; text-align:center; width: 200px;">block</p>
<p style="background-color:gray; text-align:center">block</p>



#### In-line Display

In-line elements will take up the width of their content.

```html
<!-- 
Setting the display type to 'inline' will shift the next elements to the end of the current element.
-->
<p style="display:inline">block</p>
<p style="display:inline">block</p>
<p style="display:inline">block</p>
```

<p style="background-color:gray; text-align:center; display:inline">block</p>
<p style="background-color:gray; text-align:center; display:inline">block</p>
<p style="background-color:gray; text-align:center; display:inline">block</p>



#### In-line Block Display

Can set height and width and allow elements on the same line.

#### None Display

Elements with display set to 'none' will not be visible to the user.



### CSS Float

Float allows other elements to wrap around floated elements.

The float property isn't set in the elements that wrap around the floated element.

The clear property may be set to left, right, or both to clear both float types.

```html
<div style="float:left">Float me</div>
<p>Shifted content</p>
<p>More Shifted content</p>
<footer style="clear:left">Independently positioned footer</footer>
```

<div style="width:100px; height:100px; float:left; background-color:gray; text-align:center;">Floating</div>
<p>Shifted content</p>
<p>More Shifted content</p>
<footer style="clear:left; background-color:lightgray; text-align:center;">Independently positioned footer</footer>



### How to Create Responsive Websites

Media Queries, CSS Grid, and External Frameworks (e.g., Bootstrap)

#### Media Queries

```css
@media (max-width: 600px) {
    /* CSS that applies to screens <= 600px wide. */
}
```

#### CSS Grid

```html
<style>
    .grid-container {
        display: grid;
/*
'fr' means 'fraction'
The overall width of grid is split into the total number of fr values.
E.g., 
    '1fr 1fr': 2fr, each fr takes 50% of the grid width. 
    '1fr 3fr': 4fr, right column takes 75% of the grid width.
    '1fr 1fr 1fr 1fr': each of the 4 fr takes 25% of the grid width. 
*/
        grid-template-columns: 1fr 1fr;
/*
Each value represents a row height.
May be set by % or other units.
*/        
        grid-template-rows: 50px 100px 100px;
        gap: 5px;
    }
    .first {
        /* Take up 2 columns */
        grid-column: span 2;
    }
    .card {
        background-color: gray;
        width: 50px; height: 50px;
    }
</style>
<div class="grid-container">
    <div class="first card">1</div>
    <div class="card">2</div>
    <div class="card">3</div>
    <div class="card">4</div>  
    <div class="card">5</div>
</div>
```

<div class="grid-container" style="display: grid; grid-template-columns: 1fr 1fr; grid-template-rows: 50px 100px 100px; gap: 5px; text-align:center;">
    <div class="first card" style="grid-column: span 2; background-color: gray;">1</div>
    <div class="card" style="background-color: gray;">2</div>
    <div class="card" style="background-color: gray;">3</div>
    <div class="card" style="background-color: gray;">4</div>
    <div class="card" style="background-color: gray;">5</div>
</div>



#### CSS Flexbox

Allows the creation of **1-dimensional** layouts. Section 9 will delve deeper into how flexbox works.

```html
<style>
    .flex-container {
        display: flex;
    }
    .card {
        background-color: blue;
        border: 30px solid white;
        height: 100px;
        /* Initially give all cards an equal width distribution by setting the fles to 1.
        4 columns --> 1:1:1:1 --> 1/4 : 1/4 : 1/4 : 1/4
        */
        flex: 1;
    }
    .first {
        /*
        This column width will be double others'.
        2:1:1:1
        2/5 : 1/5 : 1/5 : 1/5
        */
        flex: 2;
    }
    .second {
        /*
        This column width will be half others'.
        2:0.5:1:1
        2/4.5 : 0.5/4.5 : 1/4.5 : 1/4.5
        */
        flex: 0.5;
    }
</style>
<div class="flex-container">
    <div class="first card">1</div>
    <div class="second card">2</div>
    <div class="card">3</div>
    <div class="card">4</div>
</div>
```

<div class="flex-container" style="display: flex; text-align:center;">
    <div class="first card" style="background-color: blue; border: 30px solid white; height: 100px; flex: 2;">1</div>
    <div class="second card" style="background-color: blue; border: 30px solid white; height: 100px; flex: 0.5;">2</div>
    <div class="card" style="background-color: blue; border: 30px solid white; height: 100px; flex: 1;">3</div>
    <div class="card" style="background-color: blue; border: 30px solid white; height: 100px; flex: 1;">4</div>
</div>



#### External Frameworks

The **Bootstrap** framework  is used as an example of how frameworks may be used to create responsive sites with sizable sections.

Card widths may be specified. Each row has a maximum of 12 widths, so divide a card's column width by 12 to determine the width of the container that the card will consume. 

```html
<div class="container">
    <div class="row">
        <!--
        This card will take up 1/4th (3/12) of the container
        -->
        <div class="card col-3">
            Card
        </div>
        <!--
        This card will take up 1/12th of the container
        -->
        <div class="card col-1">
            Card
        </div>
    </div>
</div>
```

### Media Queries

```css
/* CSS that applies to screens that are
    [width] > 900px wide.
*/
@media (max-width: 600px) {
    /* CSS that applies to screens that are
    	[width] <= 600px wide.
    */
}
@media (min-width: 600px) and (max-width: 900px) {
    /* CSS that applies to screens that are
    	600px > [width] < 900px wide . 
    */
}
```

```css
/*
'screen' is implied by default.
It's not recommended to add screen for normal media queries.
*/
@media screen(orientation: landscape) {
    /* CSS Code that applies to landscape orientation*/
}
```

```css
@media print(...) {
    /* CSS Code that applies when printing webpage */
}
```

------

## Section 9: Flexbox

### Display Flex

inline, block, inline-block, and none no longer work when display is set to 'flex'.

Setting a container's display property to **flex** will cause the container to take up the width of its container as a block.

Setting a container's display property to **inline-flex** will cause the container to take up the width of its content and allow other elements to take the remainder of the row width.

### Flex Direction

**flex-direction**: sets the main-axis direction that the flexbox grows. 

- **row** (default): the flexbox grows horizontally. 
  - I.e., each element added to the container will be added to the right of the last added element.
  - The cross-axis direction would be vertical.

- **column**: the flexbox grows vertically. I.e., each element added to the container will be added under the last added element.
  - The cross-axis direction would be horizontal.
- **row-reverse**: The flexbox grows from the end to the start along the horizontal axis.
- **column-reverse**: The flexbox grows from the end to the start along the vertical axis.

**flex-basis**: The length of a flex element along the main axis.

### Flex Layout

https://css-tricks.com/snippets/css/a-guide-to-flexbox/

https://appbrewery.github.io/flex-layout/

https://appbrewery.github.io/flexboxfroggy/

The position of child element may be set via the **order** property.

```css
.green {
    order: 1;
}
```

**flex-wrap**: Property used to set whether the flex elements will wrap to the next row or continue off the screen.

- nowrap (default): elements are not wrapped.
- wrap: elements that don't fit on the screen in their entirety are wrapped to the next line.
- wrap-reverse: elements start from the opposite end of the cross-axis and the last elements wrap in the opposite direction they would normally wrap. E.g., up instead of down.

**justify-content** - along the main axis: 

- flex-start
- flex-end
- center
- space-between (first and last elements touch each end of the container)
- space-around (inner gaps are the same size, but outer gaps are 50% smaller)
- space evenly (equal gaps)

**align-items** - alignment along the cross-axis:

- flex-start
- flex-end
- center
- baseline
- stretch (stretch along the cross-axis)

The container height is set so that the vertical stretch and alignment is clear. The container height is set 7vh (7% of the viewport height).

<div style="display:flex; justify-content: space-between; height: 7vh; align-items:stretch;">
    <div style="width:100px; background-color: orange; text-align:center;">stretch</div>
    <div style="height:50px; width:100px; background-color: orange; text-align:center;">height:50px</div>
    <div style="width:100px; background-color: orange; text-align:center;">stretch</div>
    <div style="height:50px; width:100px; background-color: orange; align-self: flex-end; text-align: center;">align-self</div>
</div>

**align-content**: similar to align-items, but only works when flex-wrap is set to **wrap**.

**align-self**: allows alignment of element independent of other elements

### Flex Sizing

Algorithm used to determine each item's size.

For width:

1) Try to the width to the **max-width** and **min-width** value. The min and max values may be manually set.
   1) **max-width**:  (E.g., the width of unwrapped content) Sets the maximum amount the element may grow to. If the max-width is smaller than the flex-basis size, the flex-basis size will be ignored.
   2) **min-width** (E.g., the width of wrapped content) Set the minimum amount the element may shrink to. If the min-width is larger than the flex-basis size, the flex-basis size will be ignored.
2) Try to the width based on the **flex-basis** (tries to be the starting value to grow/shrink from...) property value (assuming it's larger than the width property value).  The width will be ignored if flex-basis is set...
3) If the window shrinks below the size of the flex-basis size, then try to set the width based on the **width** property value (assuming it's larger than the content width).
4) If the window shrinks below the width, it will then try to set the width to the **content width** (the width that allows the content to be aligned next to each other or the width of the longest word.).

**flex-basis**:

- auto (default): Give more flex-basis to the widest elements and less to the elements with less content.
- 0: Gives all elements the same amount of flex-basis.

**flex-grow**: (default *0*) Allows elements to grow (up to the max-width).

**flex-shrink**: (default *1*) Allows elements to shrink (up to the min-width).

Shorthand for setting flex-basis, flex-grow, and flex-shrink:

- flex: <grow> <shrink> <basis>
  - E.g., flex 1 1 0;

The grow and shrink property values are totaled across all flexed elements within a flexbox container. Each element's grow and shrink property value is used to determine the speed to grow and shrink.

<div style="display: flex;">
    <div style="flex: 1 1 0; background-color:grey; text-align:center;">1 [1/6]</div>
    <div style="flex: 2 1 0; background-color:lightgrey; text-align:center;">flex-grow: 2 [2/6]</div>
    <div style="flex: 3 1 0; background-color:grey; text-align:center;">flex-grow: 3 [3/6]</div>
</div>


## Section 10 - CSS Grid

### Display Grid

#### Set row-column proportions

```css
.container {
    display: grid;
    gap: 0;
    grid-template-columns: 1fr 2fr;
    grid-template-rows: 1fr 1fr;
}
```

#### Shorthand for setting row-column proportions

```css
.container {
    display: grid;
    gap: 0;
    /*grid-template: rows / columns;*/
    grid-template: 1fr 1fr / 1fr 2fr;
}
```

### Grid Sizing

- https://appbrewery.github.io/grid-sizing/

#### Auto Sizing

```css
.container {
    display: grid;
    gap: 0;
    /* Fit Content after the 100px on the left */
    grid-template-columns: 100px auto;
    /* 100% of the browser window height under the 100px */
		grid-template-rows: 100px auto;
}
```

### Fractional Sizing

```css
.container {
    display: grid;
    gap: 0;
    /* Grow & shrink proportionally based on window size */
		grid-template-columns: 1fr 2fr;
		grid-template-rows: 1fr 2.5fr;
}
```

### Min-Max Sizing

Defines how a grid is responsive.

```css
.container {
    display: grid;
		grid-template-rows: 200px 400px;
    /*Specify min & max column widths*/
    grid-template-columns: 200px minmax(400px,800px);
}
```

### Repeat

```css
.container {
    display: grid;
    /* Creat an 2x3 grid */
		grid-template-rows: repeat(2, 50px);
    grid-template-columns: repeat(3, 50px);
}
```

If there are fewer grid elements than a grid specifies, the contents will only take up as many grid rows as it needs.

<div style="display: grid; grid-template-rows: repeat(2, 50px); grid-template-columns: repeat(3, 50px); justify-content:center;">
    <div style="background-color:grey; text-align:center;">1</div>
    <div style="background-color:lightgrey; text-align:center;">2</div>
    <div style="background-color:grey; text-align:center;">3</div>
    <div style="background-color:lightgrey; text-align:center;">4</div>
    <div style="background-color:grey; text-align:center;">5</div>
</div>

Any elements that won't fit in the specified grid-size will take up as much height as it needs and while aligning with existing columns.

<div style="display: grid; grid-template-rows: repeat(2, 50px); grid-template-columns: repeat(3, 50px); justify-content:center;">
    <div style="background-color:grey; text-align:center;">1</div>
    <div style="background-color:lightgrey; text-align:center;">2</div>
    <div style="background-color:grey; text-align:center;">3</div>
    <div style="background-color:lightgrey; text-align:center;">4</div>
    <div style="background-color:grey; text-align:center;">5</div>
	<div style="background-color:lightgrey; text-align:center;">6</div>
    <div style="background-color:grey; text-align:center;">7</div>
</div>

To specify height of excess elements, use the grid-auto-height property.

```css
.container {
    display: grid;
    /* Creat an 1x3 grid */
	grid-template-rows: 200px;
    grid-template-columns: repeat(3, 50px);
    grid-auto-rows: 100px;
}
```

<div style="display: grid; grid-template-rows: 50px; grid-template-columns: repeat(3, 50px); justify-content:center; grid-auto-rows: 100px;">
    <div style="background-color:grey; text-align:center;">1</div>
    <div style="background-color:lightgrey; text-align:center;">2</div>
    <div style="background-color:grey; text-align:center;">3</div>
    <div style="background-color:lightgrey; text-align:center;">4</div>
</div>

### Grid Placement

#### Grid Elements:

- Container: The grid container is usually a `<div>` and it contains all grid elements.
- Lines: Grid lines separate grid tracks. They can be horizontal and vertical, but their only parameter is the `gap` property.

- Tracks: Grid rows and columns are tracks.

- Cells: This is the smallest element of a grid. Elements at the intersection of rows and columns.

- Items: Cells in multiple grid columns and rows may be used to create grid items.

To inspect line numbers in Chrome:

​	Inspect Element --> 

Span two columns (using shorthand): `grid-column: span 2;` 

Span two columns (using full form):

​	Note: `start` and `end` values are interchangeable.

```css
.cell {
    grid-column-start: span 2;
	grid-column-end: auto;
}
```

Span columns using Negative Indexing:

​	Spans from the 2nd grid cell to the penultimate cell.

```css
.cell {
    grid-column-start: 2;
	grid-column-end: -2;
}
```

##### Positioning:

##### Order:

- Defaults to 0 for all items.
- Can be set to any value relative to other cells' order to position a cell before or after the other cells.

```css
.cell {
    grid-column: span 2;
    /*
    This cell will be positioned afer all other cells
    having a default order of 0.
    */
	order: 1;
}
```

Setting `grid-column-start`, `grid-column-end`, `grid-row-start`, and `grid-row-end` can be an alternative to using the order.

`grid-area` is shorthand for specifying the column and row start and end positions. All grid cells must be positioned with `grid-area` if for it to be used on any cell.

```css
.cell {
    /*			+-------------- grid-row-start
    			|	+---------- grid-column-start
    			|	|	+------ grid-row-end
    			|	|	|	+--	grid-column-end
    			|	|	|	|	*/
    grid-area:	2 /	1 /	3 / 3
}
```

## Section 11 - Bootstrap

### Breakpoints

| Breakpoint        | Class infix | Dimensions |
| ----------------- | ----------- | ---------- |
| Extra small       | *None*      | <576px     |
| Small             | `sm`        | ≥576px     |
| Medium            | `md`        | ≥768px     |
| Large             | `lg`        | ≥992px     |
| Extra large       | `xl`        | ≥1200px    |
| Extra extra large | `xxl`       | ≥1400px    |



Setting a column size via the class infix sets the column's size at or **above** the window dimensions.

### Spacing

Classes are named using a format `{property}`-`{sides}`-`{size}` for `xs` and `{property}`-`{sides}`-`{breakpoint}`-`{size}` for `sm`, `md`, `lg`, `xl`, and `xxl`.

`property` is one of:

- `m` for classes that set `margin`
- `p` for classes that set `padding`

`sides` is one of:

- `t` for classes that set `margin-top` or `padding-top`
- `b` for classes that set `margin-bottom` or `padding-bottom`
- `s` (start) for classes that set `margin-left` or `padding-left` in LTR,   `margin-right` or `padding-right` in RTL.
- `e` (end) for classes that set `margin-right` or `padding-right` in LTR,   `margin-left` or `padding-left` in RTL.
- `x` for classes that set both `*-left` and `*-right`
- `y` for classes that set both `*-top` and `*-bottom`
- blank - for classes that set a `margin` or `padding` on all 4 sides of the element.

`size` is one of:

- `0` for classes that eliminate the `margin` or `padding` by setting it to 0
- `1` for classes that set the `margin` or `padding` to `$spacer * .25`
- `2` for classes that set the `margin` or `padding` to `$spacer * .5` 
- `3` for classes that set the `margin` or `padding` to `$spacer`
- `4` for classes that set the `margin` or `padding` to `$spacer * 1.5`
- `5` for classes that set the `margin` or `padding` to `$spacer * 3`
- `auto` for classes that set the `margin` to auto

Example:

​	`mt-5`: sets the top margin to $spacer * 3

### Dark Mode

```html
<!-- data-bs-theme="dark" sets the view to dark mode-->
<html lang="en" data-bs-theme="dark">
    
</html>
```

Free Web Templates

​	https://www.w3schools.com/w3css/w3css_templates.asp

Bootstrap Themes

​	https://themes.getbootstrap.com/

## Web Design

### Web Design Principles

- Color Theory
- Typography
- User Interface Design
- User Experience Design

#### Color Theory

Color Palette Mood:

- Red: Conveys Love, Energy, and Intensity
- Yellow: Conveys Joy, Intellect, Attention. (Attention grabbing)
- Green: Conveys Freshness, Safety, Growth
- Blue: Conveys Stability, Trust, Serenity
- Purple: Conveys Royalty, Wealth, Femininity

https://color.adobe.com/create/color-wheel

https://colorhunt.co/

Select two colors that are near each other on a color wheel to create an **Analogous Color Palette**.

- Good for navigation, body of website, or logo and its background.

Select two colors that are opposite of each other on a color wheel to create an **Complementary/Clashing Color Palette**.

- Good to grab attention and make things pop.

#### Typography

Types of Serif typefaces:

- Old Style: 
- Transitional
- Modern
- Slab-Serif

The proportion of the thickest to thinnest becomes more and more exaggerated for more modern typefaces.

To give an authoritative and modern impression, maybe use a modern serif typeface.

Emotions behind fonts:

- Serif: Traditional, Stable, Respectable
- San-serif: Sensible, Simple, Straightforward
- Script: Personal, Creative, Elegant
- Display: Friendly, Loud, Amusing
- Modern: Stylish, Chic, Smart

#### User Interface Design

Information Hierarchy: 

- **Color**: High-contrasting colored fonts are used to draw attention to text rather than surrounding text and graphics.
- **Size**: Larger text is read before smaller fonts. 

Layout

- Aim for about 40-60 characters per line.

Alignment: 

- Use consistent alignment in sections.

![image-20240121180010762](/home/bianco/.var/app/io.typora.Typora/config/Typora/typora-user-images/image-20240121180010762.png)

![image-20240121180158745](/home/bianco/.var/app/io.typora.Typora/config/Typora/typora-user-images/image-20240121180158745.png)

![image-20240121180239806](/home/bianco/.var/app/io.typora.Typora/config/Typora/typora-user-images/image-20240121180239806.png)

#### White Space

More clutter makes things look cheaper. E.g., Lots of space between products on display at luxury retailers.

#### Audience

Choose color, fonts, text decorations, graphics, etc. that are appropriate for your audience. E.g., children vs. banks.

### User Experience Design

- Simplicity
- Consistency of design and functionality
- Reading Patterns:  User eye-tracking heat-maps. 
  - 'F' pattern - Eye tracks from the top left to the top right before moving to the next line.
    - Keep most important content on the left gutter.
  - 'Z' pattern - Eye tracks from the top left to the top right before zig-zagging to the bottom of the page.
- All platform design - desktop, mobile, etc.

https://www.canva.com/

## Section 14 - JavaScript

Chrome-> Developer Tools -> Console 

​	Type JavaScript commands. E.g., `alert("hello");`

Chrome-> Developer Tools -> Sources  -> Snippets (you may need to click on the '>>'  to see the Snippets menu option.)

​	Click on the **+** to create a new snippet, and give is a name like 'index.js'

​	Enter JavaScript code to run.

​	Click on the Run Snippet button at the bottom right of the window

### Strings

Get a string's length:

​	`string.length`

Slicing Strings

```js
var name = "Angela";
name.slice(0,1) == "A";
// Subtract the upper index from the lower index to get the length of the resulting string.
```

### Comparators and Equality

| Comparator | Meaning                                                     |
| ---------- | ----------------------------------------------------------- |
| `==`       | Is equal to and data types match (E.g., 1 === "1" is false) |
| `===`      | Is equal to. (E.g., 1 == "1" is true)                       |
| `!==`      | Is NOT equal to.                                            |
| `&&`       | AND                                                         |
| `||`       | OR                                                          |
| `!`        | NOT                                                         |

​		

### Working with JavaScript Arrays

Check whether an item is in an array:

​	`arrayName.includes("item");`

Add an item to an array:

​	`arrayName.push("item");`

Remove the last element from the array:

​	`arrayName.pop();`

## Section 16 - The Document Object Model (DOM)

### Ways to add JavaScript to a webpage:

#### In-line

Add JS commands as an attribute in line with an HTML tag.

- Not very modular
- difficult to debug
- not good practice

```html
<body onload="alert('hello');">
  <h1>Hello</h1>
</body>
```

#### Internal JavaScript

Add via a `<script>` tag.

```html
<body>
    <h1>Hello</h1>
    <script type="text/javascript">
        alert('hello');
    </script>
</body>
```

#### External

Incorporate JavaScript as an external file via a script tag that has an external source.

- Placement of the `<script>` tag matters. If a script at the head of an HTML file tries to modify a DOM element, the script will fail because the document will not have been created for the element to be modified.

```html
<body>
    <h1>Hello</h1>
    <script src="index.js" charset="utf-8"></script>
</body>
```

```js
// index.js
alert('hello');
```

### Introduction to the Document Object Model (DOM)

```js
var heading = document.firstElementChild.lastElementChild;
heading.innerHTML = "Good Bye";
heading.style.color = "red";
heading.querySelector("input").click();
```

#### Return an array (even if there's only one item)

```js
document.getElementsByTagName("li")[0].style.color = "red";
document.getElementsByClassName("btn");
```

#### Return a single item

```js
document.getElementById("title").innerHTML = "Good Bye.";
// The 'selector' is the term in CSS before curly braces.
// May select an element, class, or Id
// Only returns element found.
document.querySelector("h1");
document.querySelector("#title");
document.querySelector(".btn");
document.querySelector("li a");
document.querySelector("li.item");
```

#### Return all instances that satisfy a selector

```js
document.querySelectorAll("li.item");
```

### Manipulating HTML Element Styles via JS

Style Object Properties:

- https://www.w3schools.com/jsref/dom_obj_style.asp

### Separation of Concerns: Structures vs Style vs Behavior

1) Use CSS to apply styles by assigning classes, IDs, or tag names to elements.

   To modify element styles,  JS should add/remove CSS selector(s) to elements.

2) Use JS to modify behavior.

Separation of concerns simplifies troubleshooting:

- If an element doesn't look the way it's supposed to, check the CSS.
- If something doesn't behave the way it's supposed to, check the JS.
- If the content isn't correct, check the HTML.

List classes that an element belongs to:

```js
document.querySelector("button").classList;
```

Add/Remove a class to an element

```js
// Where the .invisible CSS class sets visibility to hidden.
document.querySelector(".btn").classList.add("invisible");
document.querySelector(".btn").classList.remove("invisible");
```

```css
/*
CSS applies the style, while JS applies selectors, to HTML
*/
.huge {
    font-size: 10rem;
    color: red;
}
.invisible {
    visibility: hidden;
}
```

### Manipulate Text

```js
// Modify the HTML
// 		<h1 id="title"><strong>Hello</strong></h1>
// becomes
// 		<h1 id="title">Good Bye.</h1>
document.getElementById("title").innerHTML = "Good Bye.";

// Modify the content, not the associated HTML.
// 		<h1 id="title"><strong>Hello</strong></h1>
// becomes
// 		<h1 id="title"><strong>Good Bye.</strong></h1>
document.getElementById("title").textContent = "Good Bye.";
```

### Working with Attributes:

```js
document.querySelector("a").attributes;
document.querySelector("a").getAttribute("href");
document.querySelector("a").setAttribute("href", "https://www.google.com");
```

## Section 18: Advanced Javascript and DOM Manipulation

### Chrome Debugger

1) Chrome -> Developer Tools -> Console.
2) Type `debugger;` in the console and hit <kbd>SHIFT</kbd> + <kbd>ENTER</kbd>.
   1) Note: the combination of keys, <kbd>SHIFT</kbd> + <kbd>ENTER</kbd>, moves to the next line in the console without entering the command.
3) Add a function call in the console and hit <kbd>Enter</kbd>.
   1) The debugger will run the first line of code.
4) Use the 'Step Into Next Function Call' button.

### Trigger Functions Upon Events

```js
function handleClick() {
    alert("clicked");
}
// Add an event listener to each element belonging to the 'drum class' that calls the handleClick functions when a user clicks on the element.
var buttons = document.querySelectorAll(".drum")
for (var i = 0; i < buttons.length; i++) {
  buttons[i].addEventListener("click", handleClick);
}
```

### Trigger Anonymous Function Upon Events

```js
// Add an event listenter to elements 
document.querySelector(".set .a")
    .addEventListener("click", function () {
    alert("clicked");
});
```

### JS Objects

```js
var bellBoy1 = {
    name: "Timmy",
    age: 19,
    hasWorkPermit: true,
    languages: ["French", "English"],
    moveSuitcase: function() {
        alert("May I take your suitcase?");
        pickUpSuitcase();
        move();
    }
}
console.log(bellBoy1.name)
```

### Factory 

```js
// Constructor
function BellBoy (name, age, hasWorkPermit, languages) {
    this.name: name;
    this.age: age;
    this.hasWorkPermit: hasWorkPermit;
    this.languages: languages;
    this.moveSuitcase: function() {
        alert("May I take your suitcase?");
        pickUpSuitcase();
        move();
    }
}

// Initialize Object
var bellBoy1 = new BellBoy("Timmy", 19, true, ["French", "English"]);
```

### Understanding Higher-Order Functions and Callbacks

 Higher-order function: A function that can take functions (I.e., callback functions) as inputs.

```js
// This is a simplified version of how eventListener functions work.
function anotherAddEventListener(typeOfEvent, callback) {
    	// Event detection code...
    
    // When an event happens, create an event object.
    // Assume this object is created upon the event occuring.
    var eventThatHappened = {
        eventType: "keydown",
        key: "p",
        durationOfKeydown: 2
    }
    
    // The event that happened can be passed back via the callback function so that programmer can get the event that happened and use it to determine which event triggered the eventListener.
    // if the event that happened is the event that we're looking to detect, then trigger the callback function. 
    if (eventThatHappened.eventType === typeOfEvent) {
        
        callback(eventThatHappened);
    }
}

// Use the simplified event listener.
anotherAddEventListener("keydown", function(event) {
   console.log(event);
});
```

## Section 19 - jQuery

```js
// Vanilla JS
document.querySelector("h1");

// jQuery equivalent (Selects all h1 elements)
jQuery("h1");
// or simply
$("h1");

```

### Add jQuery to a webpage

#### CDN

jQuery may be added to a page via CDN. The advantage of using a popular CDN is that if a user visited another website that uses the same CDN to fetch the jQuery library, then the user's browser is likely to have jQuery cached and available for reuse. This means the library doesn't need to be downloaded so your page would load faster.

Use the Google CDN found on the jQuery download page:

- https://jquery.com/download/

Check whether the jQuery library is ready for use:

- While jQuery and the JS file are included in the HTML head section, have a condition, in the JS file, that checks whether the jQuery library, *or document*, is ready before running jQuery code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
  <script type="text/javascript" src="index.js"></script>
  <title>Document</title>
</head>
<body>
  <!-- Note: the script tags are in the head section.-->
  <h1>Hello</h1>
</body>
</html>
```

```js
$(document).ready(function() {
   // See jQuery CSS Styling section below.
   $("h1").css("color","red");
});
```

- Alternatively, place the script tags at the end of the HTML body to ensure jQuery is ready before running the JS file.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>Document</title>
</head>
<body>
  <h1>Hello</h1>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
  <script type="text/javascript" src="index.js"></script>
</body>
</html>
```

#### jQuery CSS Styling 

```js
/// NOTE Don't do this. Separate concerns & assign classes, IDs, or tags.
document.querySelector("h1").style.color = "red";
// jQuery equivalent
$("h1").css("color","red");
```

```js
/// NOTE Don't do this. Separate concerns & assign classes, IDs, or tags.
// Log the h1 color.
console.log($("h1").css("color"));
```

```js
// Preferred behavior
$("h1").addClass("big-title");
$("h1").removeClass("big-title");

// Add multiple classes at once.
$("h1").addClass("big-title margin-50");
```

#### Check active styles/attributes

```js
// Returns a boolean
$("h1").hasClass("margin-50");
```

 **Change Content**

```js
// Selects all h1 elements and sets text
// Replaces HTML existing tags.
// HTML tags withing the quotes will show up as content.
$("h1").text("Bye");

// selects all h1 elements and sets the inner HTML.
// Replaces HTML existing tags.
// HTML tags withing the quotes will be applied as HTML.
$("h1").html("<em>Hey</em>");
```

#### Set Attributes

```js
// Get an img's source (or all imgs' sources.)
$("img").attr("src");

// Set anchor tag src
$("a").attr("src", "https://www.yahoo.com");

```

#### Event Listeners

- https://developer.mozilla.org/en-US/docs/Web/Events

```js
// Add a click event listener to h1 tags.
$("h1").click(function () {
  $("h1").css("color", "purple");
});
```

```JS
// Add a click event listener to all buttons.
$("button").click(function () {
  $("h1").css("color", "purple");
});
$("button").on("click", function () {
  $("h1").css("color", "purple");
});

// Add a keypress event listener to all input elements.
$("input").keypress(function(e) {
  console.log(e.key);
});
$("input").on("keypress", function(e) {
  console.log(e.key);
});

// Add a keypress event listener to entire document.
$("body").keypress(function(e) {
  console.log(e.key);
});
$(document).keypress(function(e) {
  console.log(e.key);
});


$("button").on("mouseover", function () {
  $("button").css("color", "purple");
});
```

#### Add HTML Elements

##### Add elements before opening tags or after closing tags (outside the tags):

```js
// Add a new button before opening h1 tag(s).
$("h1").before("<button>New</button>");
// Add a new button after closing h1 tag(s).
$("h1").after("<button>New</button>");
```

##### Add elements after opening tags or before closing tags (inside the tags):

```js
// Add a new button as the first element inside h1 tag(s).
$("h1").prepend("<button>New</button>");
// Add a new button as the last element inside h1 tag(s).
$("h1").after("<button>New</button>");
```

### Animations

- https://www.w3schools.com/jquery/jquery_ref_effects.asp

#### Hide/Show elements

```js
$("h1").hide();
$("h1").show();
// Toggle between hidden and shown.
$("h1").toggle();

// Fade in/out elements to hide/show.
$("h1").fadeOut();
$("h1").fadeIn();
$("h1").fadeToggle();
```

#### Collapse/Expand Elements

- https://api.jquery.com/slideDown/

```js
// Collapse h1 elements
$("h1").slideUp();
// Expand h1 elements
$("h1").slideDown();
// Toggle Collapse/Expansion
$("h1").slideToggle();
```

#### Custom Animations

Any property that may be assigned a numeric value, with or without units (E.g., 20px or 20%), may be set to tween between different values.

```js
// Tween the opacity to 50%
$("h1").animate({
    opacity: 0.5
});
```

#### Chain Animations

```js
// Each animation will occur one after another starting from the slideUp animation.
$("h1").slideUp().slideDown().animate({opacity: 0.5});
```

## Section 21 - Node.js

### Enter the Node Read Eval Print Loop (REPL)

Type the following command in a Linux terminal.

```console
node
```

Node.js is a Javascript runtime, so JS code will execute in the node REPL.

### To run a js file:

```console
node filename.js
```

### Initialize an npm project

Run the following command from the project root folder to open the npm Initialization Utility, which will create the configuration file, package.json.

```console
npm init
```

NOTE: The initialization may be run after npm packages were already installed. Dependencies in a package.json file will not be deleted.

The initialization utility will ask for:

- package name: this is the name of the project/package you're creating.
- the version number: (defaults to 1.0.0).
- description: enter a description for the project.
- entry point: we'll use index.js
- test command: we'll leave empty
- git repository: we'll leave empty
- author: that's you
- license: we'll leave at ISC

### Install npm package

```console
npm install <package name>
npm i <package name>
npm i <package 1 name> <package 2 name> <package 3 name>
```

### Common JavaScript (CJS) vs. ECMAScript Modules(ESM)

```js
// Use either of these after installing packages.

// Old way to add modules to projects with CJS
const fs = require('node:fs/promise');
// Newer way to add modules to projects with ESM
// See next section to use this method.
import * as fs from 'node:fs/promise';
```

#### To add modules via ESM (ES6) rather than using CJS

Modify the package.js file to add a 'type' parameter and value (the default value is 'common' for Common JS:

```json
{
    "name": "package name",
    "version": "1.0.0",
    "type": "module",
    "other keys below": "other assoc. values"
}
```

------

## Section 24 - Express.js with Node.js

### Steps to creating an Express Server

1. Create a directory and navigate to it.
2. Create an index.js file.
3. Initialize NPM.
4. Install the Express package.
5. Write the Server application in the index.js file.
6. Start the server from a terminal with `node index.js`.
7. navigate to http://localhost:3000/ (Or use the port number reported in the Linux terminal after running node in the last step.)

### View open ports

#### Linux/Mac

​	`sudo lsof -i -P -n | grep LISTEN`

#### Windows

​	`netstat -ano | findstr "LISTENING"`

### Bare server

This server will listen for requests on specified port and print a message in a terminal as soon as the index.js file is served by running `node index.js`.

```js
import express from "express";
const app = express();
const port = 3000;

app.listen(port, () => {
  console.log(`Server running on port ${port}.`);
});
```

Navigating a browser to `localhost:3000` will result in an error `Cannot GET /` in the browser window because the server doesn't have a root, `/`, endpoint to connect to via a GET request.

NOTE: Running `console.log()` from the server's index.js file will ouput a log on the server, not the client (e.g., a browser connecting to the server).

### Add a GET Path/Endpoint.

```js
import express from "express";
const app = express();
const port = 3000;

// Root path/endpoint
app.get("/", (req, res) => {
  // Print a list of key-value pairs for the raw request/response headers list that was received.
  console.log(req.rawHeaders);
  res.send("<h1>Hello World</h1>");
});

app.listen(port, () => {
  console.log(`Server running on port ${port}.`);
});
```

### Add Hot Reload via nodemon

nodemon automatically restarts node servers upon detecting changes.

#### Install and Run nodemon without sudo (Hack...)

Install nodemon.

```console
npm i nodemon
```

Run index.js with nodemon using the package's path within the project (so that you don't need to install nodemon globally)

```console
node node_modules/nodemon/bin/nodemon.js index.js
```

#### Install and Run nodemon with sudo

Install nodemon (I couldn't install nodemon globally without sudo)

```console
sudo npm i -g nodemon
```

Run index.js with nodemon.

```console
nodemon index.js
```

When opening a project you've cloned, NPM can automatically install all packages with the following Linux terminal command  from the project's roon directory (no need to add anything after the word 'install'):

```console
npm install
```

### Postman

Status Codes: 

- 1XX: "Hold on"
- 2XX: "Here you go"
- 3XX: "Go away!"
- 4XX: "You fucked up. For example, wrong address or invalid endpoint."
- 5XX: "We fucked up"

#### Requests: GET, POST, PUT, PATCH, and DELETE

```js
import express from "express";
const app = express();
// GET
app.get("/", (req, res) => {
  res.send("<h1>Hello World</h1>");
});
// POST
app.post("/register", (req, res) => {
  res.sendStatus(201);
});
// PUT (send the entire record)
app.put("/user/angela", (req, res) => {
  res.sendStatus(200);
});
// PATCH (Just send the record portion that's needed)
app.patch("/user/angela", (req, res) => {
  res.sendStatus(200);
});
// DELETE
app.delete("/user/angela", (req, res) => {
  res.sendStatus(200);
});
```

### Middlewares

The following lines are needed to retrieve the full path of the current working directory.

```js
import { dirname } from "path";
import { fileURLToPath } from "url";
const __dirname = dirname(fileURLToPath(import.meta.url));

app.get("/", (req, res) => {
    // Static files, files that don't chage, should be placed in the public folder within projects.
    // The full path is needed to send files as responses to requests, and __dirname provides the path to the current working directory, shich should be the root directory.
  res.sendFile(__dirname + "/public/index.html");
});
```

```js
import { dirname } from "path";
import { morgan } from "morgan";

const app = express();
const port = 3000;
var logger = app.use(morgan("tiny"));

app.get("/", (req, res) => {
	res.send("Hello");
});

app.listen(port, () => {
  console.log(`Listening on port ${port}`);
});
```

#### DIY Middleware

The next function is called to carry on with handling an incoming request after activating our middleware/function (E.g., proceed to another middleware function that may be installed/the next app.use()). Our middleware only logs a message including the request method. 

<u>If you want requests to be authenticated, you'll need to consider the order of running middleware.</u>

```js
import { dirname } from "path";
const app = express();
const port = 3000;

app.use((req, res, next) => {
	console.log("Request method: ", req.method);
    // Your server will hang without the next() function.
    next();
});

app.get("/", (req, res) => {
	res.send("Hello"");
});

app.listen(port, () => {
  console.log(`Listening on port ${port}`);
});
```

```js
import express from "express";

const app = express();
const port = 3000;

function logger(req, res, next) {
  console.log(req.method, req.url);
  next();
}

app.use(logger);

app.get("/", (req, res) => {
  res.send(`The date and time is ${new Date()}.`);
});

app.listen(port, () => {
  console.log(`Listening on port ${port}`);
});
```

#### Project 4

1. Serve the website when a GET request is made to '/'.
2. Parse the incoming data with a middleware component
3. Send back the result with a re.send() function.

```js
import express from "express";
// body-parser is now incorporated into Express, so we don't need to import it. To use body-parser, use its methods against the express module.
// E.g., express.urlencoded() or express.redirect() instead of bodyParser.urlencoded() or bodyParser.redirect()
//import bodyParser from "body-parser";

import { dirname } from "path";
import { fileURLToPath } from "url";
const __dirname = dirname(fileURLToPath(import.meta.url));

const app = express();
const port = 3000;
var bandName = "";

function dumbNameGenerator(req, res, next) {
  console.log("NameGenerator: ", req);
  next();
}

// This code will fail if the bodyparser is called after the dumbNameGenerator function because the function needs the street and pet names from the parser.
app.use(bodyParser.urlencoded({extended: true}));
app.use(dumbNameGenerator);

app.get("/", (req, res) => {
  res.sendFile(__dirname + "/public/index.html");
});

app.post("/submit", (req, res) => {
  console.log("Submit: ", req.body);
  bandName = req.body["street"]+req.body["pet"];
  res.send("Your band name is " + bandName);
});

app.listen(port, () => {
  console.log(`Listening on port ${port}`);
});
```

## Section 25 - EJS

HTML templates that are **rendered** with JS.

To use this on VS Code, install the "EJS Language Support" plugin in VS Code...

- The plugin from DigitalBrainstem is currently the most popular EJS plugin for VS Code.

#### Create a project with express and ejs in a new project folder.

To use EJS templates, the EJS files must be placed in a views directory within a project's root folder.

```console
mkdir project_folder
cd project_folder
npm init
npm i express ejs
mkdir views; touch index.js views/index.ejs
```

Open package.json and add a key-value pair of `"type":"module"` in the root level of the JSON object.

index.js

```index.js
app.post("/submit", (req, res) => {
    res.render(
        "index.ejs", 
	      { name:req.body["name"] }
	  );
});
```

index.ejs

```ejs
<body>
    <h1>
        Hello <%= name %>
    </h1>
</body>
```



### Sending Data to an EJS file with **locals**

If you try to access a variable that doesn't exist, for whatever reason (e.g., bug in code of forgot to send to ejs file), the page will not render!!!

Simply checking whether the value exists in JS, (e.g., with `<% if (variable1) { %>`) won't help because EJS tries to use variables before checking.

To get around this, use `locals`, because the locals variable will always exist.

```ejs
<% if (locals.variable1) { %>
	Do stuff here...
<% } %>
```



| Tag                          | Meaning                                      | Example Output                             |
| ---------------------------- | -------------------------------------------- | ------------------------------------------ |
| <%= variable %>              | JS Output                                    | *variable value*                           |
| <% console.log("hello") %>   | JS Execute                                   | output "hello" to browser console          |
| <%- <h1>Hello</h1> %>        | Render HTML                                  | "Hello" will be displayed as H1 HTML text. |
| <%% variable %%>             | Literal                                      | show "<%" or "%>"                          |
| <%# This is a comment %>     | Comment                                      |                                            |
| <%- include("*filename*") %> | Insert another EJS file in place of the tag. |                                            |

NOTE: When EJS does templating, it's inserting a template string for arrays, so you may need to split the arrays.

```ejs
<script>
  // The countries array will be received as a string, not an array. 
	const country_code = "<%= countries %>".split(",");
  console.log(typeof ("<%= countries %>"));
</script>

```



### EJS For loops

```ejs
<body>
	<ul>
        <% for (let i=0; i<items.length; i++) { %>
            <li>	
                <%= items[i] %>
            </li>
        <% } %>
        <% items.forEach(element => { %>
        	<li>
        		<%= element %>
        	</li>
        <% }); %>
    </ul>    
</body>
```





### Static Files

For CSS and other frameworks, that were added to static EJS files, to work, add the following to your JS to point to the static files, which should be in the `public` directory.

```js
// 'public' would be changed to whatever it needs to be if the name of your public folder isn't 'public'.
// This tells EJS where our static files are located.
app.use(express.static("public"));
```

After the last line, everything inside the `public` directory will be treated as a static file and the `hrefs` in EJS files' headers will refer to subdirectories of the `public` directory.

```ejs
<head>
    <!-- If we use app.use(express.static("public")), this will point to /public/styles/layout.css -->
    <!-- We link to the stylesheet relative to the location of the public folder -->
    <link rel="stylesheet" href="/styles/layout.css">
</head>
```



## Sections 27 - Git, GitHub, and Version Control

### Roll back a file to the last committed version.

​	`git checkout <file name>`

### Remote Repositories

Tell the system we've created a remote repository at the specified URL, and we want to transfer our commits to the repository.

​	`git remote add <name> <url>`

​	By convention the name of the remote is 'origin'. 

​	`git remote add origin <url>`

​	Then **push** the local code to the remote (the 'u' flag links the remote and local repositories):

​	`git push -u <remote name> <branch name>`

​	E.g., Link the remote, origin, and 'main' branch and push local code to the main branch on the remote:

​	`git push -u origin main`

## .gitignore

- May add comments with "#"

Pre-made .gitignore templates from the Node.js team:

​	https://github.com/github/gitignore/blob/main/Node.gitignore

​	- Automatically ignores env settings and dependency directories.



## Git Merge

Add a branch's changes to the main branch by merging the branch back into main:

1. Checkout the main branch

   `git checkout main`

2. merge the branch into main

   `git merge <branchname>`

   This may open an editor that allows you to enter a merge message.

Learn and Experiment with Branching at: https://learngitbranching.js.org/



## Forking and Pull Requests

Forking copies a repo without keeping permissions of original directory.

Changes can be added to the original repo via a pull request.

The person that owns the original repo has the final say about whether to ***pull*** the changes to the original repository.



## Section 28: APIs

### Parameters

**Query Parameter** - Filters results

​	e.g., base_url/{endpoint}**?{query-parameter}={query-parameter value}**

​	e.g., bored-api.com/filter**?type=social&participants=2**

**Path Parameter** - Identify a specific resource based on a parameter, such as an ID or user name.

​	e.g., base_url/endpoint/**{path-parameter}**

​	e.g., bored-api.com/endpoint/**1**	(Where 1 is the key parameter's value)



### JSON

JSON Visualizer - [jsonviewer.stack.hu](jsonviewer.stack.hu)

To send a JavaScript object over the Internet, you'll need to serialize the object into JSON (i.e., into a flatpack).

**JavaScript Serialization** - JavaScript object to a JSON Object

​	`const jsonData = JSON.stringify(data);`

**JavaScript Parsing** - Unpack a JSON Object into a JavaScript object

​	`const data = JSON.parse(jsonData)`



### MISC

Customizable SVG patterns for your projects

https://pattern.monster/

![image-20240329211211006](/home/bianco/.var/app/io.typora.Typora/config/Typora/typora-user-images/image-20240329211211006.png)



## Making Server-Side Requests

#### Using the Node's native module, the https module, for Requests.

```js
import https from "https";

app.get("/", (req, res) => {
  const options = {
  	hostname: "bored-api.appbrewery.com",
    path:"/random",
    method: "GET"
  };
  
  const request = https.request(options, (response) => {
  	let data = "";
  	response.on("data", (chunk) => {
      data += chunk;
    });
    
    response.on("end", () => {
      try {
        const result = JSON.parse(data);
        res.render("index.ejs", {activity: data});
      } catch (error) {
        console.error("Failed to parse response:", error.message);
        res.status(500).send("Failed to fetch activity. Please try again.")
      }
    })
	});
  
  request.on("error", (error) => {
    console.log("Failed to make request:", error.message);
    res.status(500).send("Failed to fetch activity. Please try again.")
  });

	request.end();
});
```



### Using Axios for Requests

- Unlike the https package, Axios automatically waits to receive all chunks from a GET request before continuing.
- Is promise-based, so we may use `await` or `.then()`.
- Returns a JSON object, so you don't need to use `JSON.parse()`

```js
import axios from "axios";
app.get("/", async (req, res) => {
  try {
    const response = await axios.get("https://bored-api.appbrewery.com/random");
    res.render("index.ejs", {activity: response.data});
  } catch (error) {
    console.error("Failed to make requests:", error.message);
    res.status(500).send("Failed to fetch activity. Please try again.");
  }
});
```



### API Authentication

#### Types of Authentication Used:

0. #### No Authentication

   1. Allows anyone to access the API
   2. API providers may specify a **rate limit** as a safety measure. E.g., 15 requests per minute.

1. #### Basic Authentication

   1. Provide a **username** and **password** when making each request.
   2. Normally done by using a **Base64** encoded string in the request's **header**.
   3. In the class example, the username and password were added to the body to register the redentials.
      1. Xx-www-form-urlencoded
   4. Add the username and password to the authorization header when using the credentials to make requests.
      1. Select "Basic Auth" using Postman. Postman will encode the credentials together and add the result to the request header.
      2. The Axios package will also encode and decode credentials for basic authentication for you.

```console
curl -H 'Content-Type: application/json' \
   -d '{ "username":"foo", "password": "1"}' \
   -X POST \
   https://secrets-api.appbrewery.com/register
```

3. #### API Key Authorisation

   1. In the class example, the key was passed as a parameter.

4. #### Token-based Authentication

   1. More secrure than passing credentials, which may be intercepted, in requests.
   2. Tokens may expire to increase account security.
   3. Each token may be rate-limited or have other restrictions.
   4. May be used in combination with an API key rather than usernames and passwords.

```console
curl -H 'Content-Type: application/json' \
   -d '{ "username":"foo", "password": "1"}' \
   -X POST \
   https://secrets-api.appbrewery.com/get-auth-token
```



### Public APIs

https://github.com/appbrewery/public-api-lists?tab=readme-ov-file

https://rapidapi.com/collection/list-of-free-apis



## Section 30: Build Your Own API

#### RapidAPI - Curates a list of APIs

### Attributes of a RESTful API (A REpresentationsal State Transfer API):

- It supports HTTP requests (e.g., GET, POST, PUT, PATCH, and DELETE)
- It responds with a standard data format (e.g., JSON, XML, etc.) 
  - This is "Representational" part of the Representational State Transfer
- Clients and Servers are on separate systems
- Statelessness. The server shall not store client data from previous requests.)
- Resource-based. Uses a URI or URL



### Automatically generate API Documentation with Postman

Example:

1. Create a new collection in Postman.

2. Create a new HTTP request.

3. Enter a method type (e.g., GET, POST, etc.) and URL for the new HTTP request.

4. Send the request.

5. You should be able to save the request to the new collection.

6. Click on the kebob menu on the right of the collection's dropdown menu title.

7. Select "View documentation".

   This should show auto-generated API Definition Documentation including your requests as examples.

   **Ensure the examples don't contain sensitive information**



### Sample API Implementation

```js
import express from "express";
// NOTE (2024-05-17):	body-parser is built into express now.
import bodyParser from "body-parser";

const app = express();
const port = 3000;
const masterKey = "4VGP2DN-6EWM4SJ-N6FGRHV-Z3PR3TT";

app.use(bodyParser.urlencoded({ extended: true }));
app.listen(port, () => {
  console.log(`Successfully started server on port ${port}.`);
});

var jokes = [
  {
    id: 1,
    jokeText:
      "Why don't some couples go to the gym? Because some relationships don't work out.",
    jokeType: "Science",
  },
  {
    id: 2,
    jokeText:
      "Why did the scarecrow win an award? Because he was outstanding in his field.",
    jokeType: "Puns",
  },

  ...
  
];
```



#### GET

```js
//1. GET a random joke
app.get("/jokes/random", async (req, res) => {
  const randomIndex = Math.floor(Math.random() * jokes.length + 1);
  res.json(jokes[randomIndex]);
});
```



#### GET (one)

```js
//2. GET a specific joke
app.get(`/jokes/:id`, async (req, res) => {
  // Access path parameter having the name "id".
  // NOTE: Path parameters are returned as strings, so
  // we need to convert the value for id to an integer.
  const id = parseInt(req.params.id);
  // Iterate through the joke array and return all
  // jokes where joke.id === id is true.
  // Type and value must match.
  // Get a joke(s) having the specified ID, if any exist.
  const foundJoke = jokes.find((joke) => joke.id === id);
  if (!foundJoke) return res.sendStatus(404).json({message: "Joke not found."});
  res.json(foundJoke);
});
```



#### GET (based on query parameter(s))

```js
//3. GET a jokes by filtering on the joke type
app.get(`/filter`, async (req, res) => {
  const type = req.query.type;
  const filteredJokes = jokes.filter(function (joke) {
    return joke.jokeType === type;
  });
  // Equivalent to filteredJokes
  const altFilteredJokes = jokes.filter((joke) => joke.jokeType === type);
  res.json(filteredJokes);
});
```



#### POST

```js
//4. POST a new joke
// NOTE:
//  Set the Body's 'Content-Type' to 'x-www-form-urlencoded' in Postman
//  or to 'application/x-www-form-urlencoded' via cURL, Python, etc. when
//  making the POST request.
app.post(`/jokes`, async (req, res) => {
  // The ID is calculated while text and type are
  // extracted from the POST request body via
  // body-parser.
  const newJoke = {
    id: jokes.length + 1,
    jokeText: req.body.text,
    jokeType: req.body.type
  };
  jokes.push(newJoke);
  const lastJoke = jokes.slice(-1);
  console.log(lastJoke);
  res.json(newJoke);
});
```



#### PUT

```js
//5. PUT a joke
app.put(`/jokes/:id`, async (req, res) => {
  const id = parseInt(req.params.id);
  console.log(id);
  const replacementJoke = {
    id: id,
    jokeText: req.body.text,
    jokeType: req.body.type
  };
  // Get the index(es) of a joke(s) having the specified ID, if any exist.
  const searchIndex = jokes.findIndex((joke) => joke.id === id);
  // TODO Return error if not found.
  jokes[searchIndex] = replacementJoke;
  console.log(`Updated joke ${id}`)
  res.json(replacementJoke);
});
```



#### PATCH

```js
//6a. PATCH a joke
app.patch(`/jokes/:id`, async (req, res) => {
  const id = parseInt(req.params.id);
  // Return true when the joke id 
  // matches the received id parameter.
  function isIdInJoke(joke) {
    return joke.id === id;
  }
  const existingJoke = jokes.find(isIdInJoke);
  const replacementJoke = {
    id: id,
    jokeText: req.body.text || existingJoke.jokeText,
    jokeType: req.body.type || existingJoke.jokeType,
  };
  const searchIndex = jokes.findIndex(isIdInJoke);
  jokes[searchIndex] = replacementJoke;
  console.log(replacementJoke);
  res.json(replacementJoke);
});
```



#### PATCH (Alternative method using spread syntax)

##### NOTE:  THIS IS DANGEROUS!!! Check received values' types, ranges, and content before using them!

```js
//6b. PATCH a joke
app.patch(`/jokes/alt-patch/:id`, async (req, res) => {
  const id = parseInt(req.params.id);
  const searchIndex = jokes.findIndex((joke) => joke.id === id);
  // Use spread syntax to override only the
  // values that are listed as body parameters.
  jokes[searchIndex] = {
    ...jokes[searchIndex], ...req.body
  };
  res.json(jokes[searchIndex]);
});
```



#### DELETE (one)

```js
//7. DELETE Specific joke
app.delete(`/jokes/:id`, async (req, res) => {
  const id = parseInt(req.params.id);
  const searchIndex = jokes.findIndex((joke) => joke.id === id);
  if (searchIndex > -1 ) {
    jokes.splice(searchIndex, 1);
		res.json({message: "Joke deleted."});
    return;
  } else {
    res
    .status(404)
    .json({ error:  `Joke with id: ${id} not found. ` +
    ` No jokes were deleted.`});
  }
});
```



#### DELETE (all)

##### NOTE: DON'T PASS AN API KEY AS A QUERY PARAM AS SHOWN!!! Authorization will be elaborated on later in the course.
```js
//8. DELETE All jokes
app.delete(`/all`, async (req, res) => {
  // NOTE: DON'T PASS AN API KEY AS A QUERY PARAM AS SHOWN!!!
  // Authorization will be elaborated on later in the course.
  const userKey = req.query.key;
  console.log(userKey);
  if (userKey === masterKey) {
    jokes = [];
    res.sendStatus(200);
    console.log("jokes =", jokes);
  } else {
    res
    .status(404)
    .json({ error:  "You are not authorized to perform this action."});
  }
});
```



## Section 32: SQL

- https://www.w3schools.com/sql/
- https://www.w3schools.com/sql/sql_datatypes.asp
- https://www.w3schools.com/sql/sql_primarykey.asp
- https://sqliteonline.com/
- https://www.mycompiler.io/view/08q0XDT7TFp

### CRUD

#### CREATE

```sql
-- create customers table
CREATE TABLE customers (
  id INT,
  first_name STRING,
  last_name STRING,
  address STRING,
  PRIMARY KEY (id)
);
-- insert some values
INSERT INTO customers VALUES (1, 'John', 'Doe', '32 Cherry Blvd');
INSERT INTO customers VALUES (2, 'Angela', 'Yu', '12 Sunset Drive');
-- fetch some values
SELECT * FROM customers WHERE first_name = 'John';


-- create the products table
-- 'NOT NULL' indicates values are not optional and must be entered.
CREATE TABLE products (
    id INT NOT NULL,
    name STRING,
    price MONEY,
    PRIMARY KEY (id)
);

-- Show all records in the customers table
SELECT * FROM Customers

-- insert a product into products table
-- DON'T USE DOUBLE_QUOTES
INSERT INTO products
VALUES (1, 'Pen', 1.20);

-- select a product with id = 1
SELECT * FROM products WHERE id = 1;

-- insert a product with no price into products table
INSERT INTO products (id, name) VALUES (2, 'Pencil');

-- select a product with id = 2
SELECT * FROM products WHERE id = 2;
```



#### UPDATE (A value)

```sql
UPDATE products
SET price = 0.80
-- IF YOU DON'T ADD THE NEXT LINE, YOU'LL CHANGE ALL VALUES IN YOUR TABLE TO 0.80!!!
WHERE id=2
```

##### ALTER (add a column)

```sql
ALTER TABLE products
-- ADD Column_Name Data_Type  
ADD stock INT
```

### Understanding SQL Relationships, Foreign Keys, and Inner Joins

- https://www.w3schools.com/sql/sql_foreignkey.asp
- https://www.w3schools.com/sql/sql_join_inner.asp

```SQL
CREATE TABLE orders (
  id INT NOT NULL,
  order_number INT,
  customer_id INT,
  product_id INT,
  PRIMARY KEY (id),
  -- Create relationships between this order table
  -- and the customers and product tables.
  -- id is the Foreign ID within the customers table
  -- that is referenced in this orders table.
  FOREIGN KEY (customer_id) REFERENCES customers(id)
  FOREIGN KEY (product_id) REFERENCES product(id)
);
```









```sql
-- create customers table
CREATE TABLE customers (
  id INT,
  first_name STRING,
  last_name STRING,
  address STRING,
  PRIMARY KEY (id)
);
-- insert some values
INSERT INTO customers VALUES (1, 'John', 'Doe', '32 Cherry Blvd');
INSERT INTO customers VALUES (2, 'Angela', 'Yu', '12 Sunset Drive');
-- fetch some values
SELECT * FROM customers WHERE first_name = 'John';


-- create the products table
CREATE TABLE products (
    id INT NOT NULL,
    name STRING,
    price MONEY,
    PRIMARY KEY (id)
);

-- insert a product into products table
INSERT INTO products VALUES (1, 'Pen', 1.20);

-- select a product with id = 1
SELECT * FROM products WHERE id = 1;

-- insert a product with no price into products table
INSERT INTO products (id, name) VALUES (2, 'Pencil');

-- select a product with id = 2
SELECT * FROM products WHERE id = 2;

-- update a row in products table
UPDATE products SET price=0.8 WHERE id = 2;

-- select all records from products table
SELECT * FROM products;

-- add a new column - stock to the products table
ALTER TABLE products ADD stock INT;

-- update a row in products table
UPDATE products SET stock=32 WHERE id = 1;

-- select all records from products table
SELECT * FROM products;

-- update a row in products table
UPDATE products SET stock=12 WHERE id = 2;

-- select all records from products table
SELECT * FROM products;

-- delete a row from products table
DELETE FROM products WHERE id = 2;

-- insert back the deleted row into products table
INSERT INTO products VALUES (2, 'Pencil', 0.8, 12);

-- create the orders table
CREATE TABLE orders (
  id INT NOT NULL,
  order_number INT,
  customer_id INT,
  product_id INT,
  PRIMARY KEY (id),
  FOREIGN KEY (customer_id) REFERENCES customers(id),
  FOREIGN KEY (product_id) REFERENCES products(id)
);

-- insert an order into orders table
INSERT INTO orders VALUES (1, 4362, 2, 1);

-- join orders and customers table
-- We want to create a new table having a combination of fields from different tables.
-- We specify the <table>.<feild> to retrieve.
SELECT orders.order_number, customers.first_name, customers.last_name, customers.address
FROM orders
-- From the orders table, you will find the particular foreign key match below for joining.
INNER JOIN customers 
-- The fields that must be matched on for joining are listed 
ON orders.customer_id = customers.id;

-- join orders and products table
SELECT orders.order_number, products.name, products.price, products.stock
FROM orders
INNER JOIN products ON product_id = products.id;
```



## Section 33: PostgreSQL

- Install the Postgres Server (if running locally)
- Install pgAdmin - GUI for Postgres

```postgresql
CREATE TABLE friends (
	id SERIAL PRIMARY KEY,
  -- VARCHAR Variable Character
  --   Limit data size to 50 characters
  --   If sata size is less than 50, unused
  --   char space will be truncated.
  --   CHAR would not truncate unused space.
  name VARCHAR(50),
  age INT,
  -- TEXT
  --   Auto-truncates to data size (i.e., it's variable), but doesn't require you to specify a maximum size.
  is_cool BOOLEAN
);
```



##### NOTE!!! Sometimes Postgres will not start auto-indexing id values from the correct number.

Here’s how you can check and fix the sequence alignment issue:

### Checking Sequence Value

You can check the current value of the sequence associated with your primary key using:

```postgresql
-- Get the last id value
SELECT last_value FROM your_sequence_name;
```

Replace `your_sequence_name` with the actual name of your sequence. Often, the sequence name is `<table_name>_<column_name>_seq`.

### Adjusting the Sequence Value

If you find that the sequence value is out of sync, you can adjust it. For example, if the highest `id` in your table is 2, you should set the sequence to start from 3:

```postgresql
SELECT setval('your_sequence_name', (SELECT MAX(id) FROM your_table_name) + 1);
```

### Example Fix

Let's say your table is `users` and the primary key column is `id`. The sequence might be named `users_id_seq`. Here’s how you can adjust it:

1. Check the highest `id` value:

   ```postgresql
   SELECT MAX(id) FROM users;
   ```

2. Adjust the sequence:

   ```postgresql
   SELECT setval('users_id_seq', (SELECT MAX(id) FROM users) + 1);
   ```

This ensures the next inserted row will have a unique `id`.

### Preventing Future Issues

- **Avoid Manual Inserts with IDs**: Try to avoid inserting rows with explicit `id` values unless absolutely necessary.
- **Use Transactions**: When modifying sequences or performing bulk inserts, use transactions to ensure consistency.
- **Regular Maintenance**: Periodically check and maintain sequence values, especially after major data migrations or imports.



#### Postgres Setup

You may be asked to set a global password. This is a password used to access pgAdmin, and it is separate from the password that was set when installing PostgreSQL.

- When selecting a server within pgAdmin, use the PostgreSQL password. The default username is `Postgres`.

#### Create a new database within pgAdmin.

1. From the left pane, expand Servers, PostgreSQL, and Databases.
   1. There will be a default database called `postgres`. 
2. Right-click on the 'Databases' dropdown title 
3. Select `Create` from the popup menu.
4. Select `Database...` from the menu.
5. Enter a name for the database in the first field of the window that opens.
6. Click `Save` to complete the process of creating a database.

#### Create a Table via Query

The last field line cannot include a comma to indicate the end of the line.

```postgresql
CREATE TABLE capitals (
  id SERIAL PRIMARY KEY,
  country VARCHAR(45),
  capital VARCHAR(45)
);

CREATE TABLE visited_countries (
	id SERIAL PRIMARY KEY,
	country_code CHAR(2) NOT NULL UNIQUE
);
```

#### Read From a Table via Query

```postgresql
SELECT * FROM public.capitals
ORDER BY id ASC LIMIT 100;
```

#### Import Data into a Table with pgAdmin

- Right-click on a table name from the left pane.
- Select an option for importing.
- Select the file to import.
- In the `Options` tab, make sure the `Header` option is enabled. 
  - This option tells pgAdmin that the first row contains a header, not data.
  - NOTE: If the `Header` option was enabled, the `Columns` tab should show the column names of the file to be imported.
  - If the source file doesn't include an ID, remove the ID column name from the `Columns to Import` list.
- Click `OK` to import the file.

#### Rename Fields in pgAdmin

- Right-click on a table name from the left pane.
- Select `Properties...`
-  Navigate to the `Columns` tab.
- Replace the field name to rename.
- Click `Save`.

#### Reading PostgreSQL DB Data from NodeJS-Express Backend

The following instruction will be used to read data from the databse.

```postgresql
SELECT * FROM <Name of Table>
```

```js
import express from "express";
import bodyParser from "body-parser";
// Import Postgres Package
import pg from "pg";

const app = express();
const port = 3000;

// Create and configure an instance of a Postgres client.
const db = new pg.Client({
  user: "postgres",
  host: "localhost",
  database: "world",
  password: "123456", // Password used when installing Postgres.
  port: 5432,
});

// Connect to the Postgres database
db.connect();

let quiz = [];

// Run the query against the database.
db.query("SELECT * FROM flags", (err, res) => {
  if (err) {
    console.error("Error executing query", err.stack);
  } else {
    // Save the result of the query if no error.
    quiz = res.rows;
  }
  // Disconnect from the database
  db.end();
});
```

#### Get a Column's Data from a Table

```postgresql
-- Retrieve a single column.
SELECT <column name> FROM <table name>;

-- Retrieve multiple columns.
SELECT <column 1 name>, <column 2 name> 
FROM <table name>;
```

#### Filter Column Data

```postgresql
SELECT <column name>
FROM <table name>
WHERE <condition>;

-- Example 1 (Exact Match)
SELECT rice_production
FROM world_food
WHERE country = 'United States';

-- Example 2 (Similar)
-- To use a pattern to look for within a field 
-- instead of requiring an exact match.
-- E.g. Accept 'United States' as 'United States of America'.
SELECT rice_production
FROM world_food
WHERE country LIKE 'United States'

-- Example 3 (Similar)
-- To use the concatenate operator, ||, and
-- a wildcard, %, in place of a word.
-- E.g. 'United" || '%' can be used to 
--      return 'United States', `United Kingdom`, etc.
SELECT country
FROM world_food
WHERE country LIKE 'United' || '%';

-- Example 4 (Similar)
-- Use a wildcard, %, to get words that
-- start with a pattern.
-- E.g., Countries that start with 'U'.
SELECT country
FROM world_food
WHERE LOWER country LIKE 'U' || '%';
-- WHERE country LIKE 'U%';
```



```js
// GET home page
app.get("/", async (req, res) => {
  const result = await db.query("SELECT country_code FROM visited_countries");
  // TODO handle errors.
  let countries = [];
  result.rows.forEach((country) => {
    countries.push(country.country_code);
  });
  console.log(result.rows);
  res.render("index.ejs", { countries: countries, total: countries.length });
  // db.end(); // Don't close the connection...
});
```



```postgresql
INSERT INTO <table_name> (<column_name_1>, <column_name_n>)
VALUES 
	(<value_1>, <value_n>),
	(<value_1>, <value_n>);
```



```js
try {
  const query = `
    INSERT INTO world_food
    (country, rice_production, wheat_production)
    VALUES ($1, $2, $3)
  `;
  db.query(
    query, 
    ["Italy", 1.46, 7.3]
  );
} catch (err) {
  console.log(err);
  const countries = await checkVisited();
  res.render("index.ejs", {
    countries: countries,
    error: err
  });
}
```

#### One to One Relationships & Inner Joins

- This is a way to modularize a database because data associated with an ID in a main table, but that doesn't need to be accessed as frequently, doesn't need to be in the main table. Splitting less frequently accessed data in a main table into smaller table(s) can result in faster response times and makes them easier to search.
- [Draw.io](Draw.io)

##### student(id) is linked to contact_detail(id) in the following:

- E.g., once in a while, you may need to contact a student's parents.

```postgresql
CREATE TABLE student (
  id SERIAL PRIMARY KEY,
  first_name TEXT,
  last_name TEXT
);

CREATE TABLE contact_detail (
  id INTEGER REFERENCES student(id) UNIQUE,
  tel TEXT,
  address TEXT
);
```

##### Inner Join

```postgresql
-- Get the combined record data from `student` and `contact_details` for a given `id`. 
SELECT *
FROM student
-- This is an Inner Join that combines tables base on the `ON` criteria below.
JOIN contact_detail	
ON student.id = contact_detail.id
ORDER BY last_name ASC; -- ORDER BY id DESC
```

#### One-to-Many Relationships

- This is the most common relationship.
- E.g., In a class, there is one student, but the student will have many homework submissions.
  - Each homework submission is associated with a single student (No group assignments in this example).
  - In UML, the foreign key will have crow's feet near its label to indicate there's a many-to-one relationship back to a student.
  - The `homework submissions` table would need an ID to identify each homework submission in addition to a foreign key that links it back to the `student` table.

```postgresql
CREATE TABLE student (
  id SERIAL PRIMARY KEY,
  first_name TEXT,
  last_name TEXT
);

-- Many to One --
-- NOTE: It's probably better to pluralize the table name
--   to indicate a many-to-one relation back to `students`.
--   e.g., `homework_submissions` 
CREATE TABLE homework_submission (
  id SERIAL PRIMARY KEY,
  mark INTEGER, -- homework score
  -- Look for the student table,
  -- find the `id` field within the table,
  -- and set it as a relation to the
  -- `student_id` field in this table.
  student_id INTEGER REFERENCES student(id)
);
```

##### JOIN

```postgresql
-- Join --
SELECT student.id, first_name, last_name, mark
FROM student
JOIN homework_submission
ON student.id = student_id
-- more verbose, but also works
ON student.id = homework_submission.student_id
```

#### Many-to-Many Relationsship

- Least-use kind of relationship
- In UML, a many-to-may relationship may be represented as two tables with crow's feet on both ends. The relationship may also be represented with an intermediary table, where crow's feet come out of the main tables that connect to the intermediary table. The intermediary table would contain an id for the intermediary table and a foreign key to each table in the relationship.
- Makes it possible to make queries that return the number of classes a student is taking, the number of students in a class, and the names of classes that students are taking together. 

```postgresql
-- Many students may enroll in many classes.
-- Many classes will have many enrolled students.
CREATE TABLE student (
  id SERIAL PRIMARY KEY,
  first_name TEXT,
  last_name TEXT
);
-- Many to Many --
CREATE TABLE class (
  id SERIAL PRIMARY KEY,
  title VARCHAR(45)
);

-- The REFERENCES keywords indicate the fields are foreign keys.
CREATE TABLE enrollment (
  student_id INTEGER REFERENCES student(id),
  class_id INTEGER REFERENCES class(id),
  -- The primary key is set to a combination of the two primary keys.
  -- Each of the primary keys should be unique.
  -- The primary key must be unique, and using a combination of
  -- the two primary keys ensures that each combination is unique.
  PRIMARY KEY (student_id, class_id)
);
```

##### Inserting Data into Tables (for reference):

```postgresql
-- Data --
INSERT INTO student (first_name, last_name)
VALUES ('Jack', 'Bauer');

INSERT INTO class (title)
VALUES ('English Literature'), ('Maths'), ('Physics');

INSERT INTO enrollment (student_id, class_id ) VALUES (1, 1), (1, 2);
INSERT INTO enrollment (student_id ,class_id) VALUES (2, 2), (2, 3);
```

##### Fetching Data from the Many-to-Many Relationship Tables:

```postgresql
-- Get everything from the combination of tables.
SELECT *
FROM enrollment 
JOIN student ON student.id = enrollment.student_id
JOIN class ON class.id = enrollment.class_id;
```

```postgresql
-- Get student.id, first_name, last_name, title from the combination of tables.
-- Use the `student.id` as the `stud` in the returned data.
-- Setting an alias with 'AS' helps us disambiguate between fields with similar names.
-- Aliases also allows us to use shorthand for fields.
SELECT student.id AS stud, first_name, last_name, title
FROM enrollment AS e
-- `FROM enrollment e` is equivalent to `FROM enrollment AS e`.
JOIN student ON stud = e.student_id
JOIN class AS c ON c.id = e.class_id;
```



### How to Update and Delete Data & Tables

`ALTER` Is often used to change the schema of a table.

```postgresql
ALTER TABLE <table to alter>
	<do something>;

-- Rename Table
ALTER TABLE student
	RENAME TO user;

-- Change Column Datatype
ALTER TABLE student
	ALTER COLUMN first_name TYPE VARCHAR(20);
	
-- Add a Column
ALTER TABLE contact_details
	ADD email TEXT
```



##### Unique Constraint across fields
As an example of where this is useful: If tracking countries user's have visited with the fields country_code and user_id, the constraint UNIQUE (country_code,  user_id) would prevent a country code from being repeated for each user. Different users could list the same country code to indicate they also visited the same country.

```postgresql
-- E.g., a and c cannon both be set to 1.
CREATE TABLE example (
	a integer,
	b integer,
  c integer,
  UNIQUE (a, c) -- a & c must be unique WHEN COMBINED TOGETHER.
);
-- If the table already exists without UNIQUE (a, c)
ALTER TABLE example
	ADD UNIQUE (a, c);
```



```postgresql
UPDATE <table to update>
	SET <column to update> = <value, ...>
	-- e.g., WHERE name = 'Angela';
	WHERE <some condition>;
```



```postgresql
DELETE FROM <table to delete>
WHERE <condition> AND <condition>;


```





"Use of `RETURNING` avoids performing an extra database query to collect the data, and is especially valuable when it would otherwise be difficult to identify the modified rows reliably." - [Postgres Docs](https://www.postgresql.org/docs/current/dml-returning.html)



## Section 35: Authentication & Security: Handling Credentials and Designing a Secure Login

The fastest systems can compute:

- 20,000,000,000 MD5 Hashes/second (Hashed Passwords), or
- 17,000 bcrypt Hashes/second (Salted Passwords)

https://encode-decode.com/aes256-encrypt-online/

### Level 3 - How to Salt Passwords for Improved Encryption

#### Password Hashing

```js
import bcrypt from 'bcrypt";'
const saltRounds = 10; // at least 10 is recommended

app.post("/register", async (req, res) => {
  const email = req.body.username;
  const password = req.body.password;
  try {
    const checkResult = await db.query("SELECT * FROM users WHERE email = $1", [
      email,
    ]);
    if (checkResult.rows.length > 0) {
      res.send("Email already exists. Try logging in.");
    } else {
      // Password hashing
      // After passing a password and a number of salt rounds,
      // bcrypt.hash() will return either an error or a hash and
      // cause a callback function to execute.
      bcrypt.hash(password, saltRounds, async (err, hash) => {
        if (err) {
          console.log("Error message:", err);
        } else {
          const result = await db.query(
            "INSERT INTO users (email, password) VALUES ($1, $2)",
            // [email, password]
            [email, hash] // We pass the salted password as the password.
          );
          console.log(result);
        }
      });
      res.render("secrets.ejs");
    }
  } catch (err) {
    console.log(err);
  }
});

```



#### Use `bcrypt.compare()` to compare a user-entered password to a hashed password that is stored in a database:

```js
app.post("/login", async (req, res) => {
  const email = req.body.username;
  const loginPassword = req.body.password;

  try {
    const result = await db.query("SELECT * FROM users WHERE email = $1", [
      email,
    ]);
    if (result.rows.length > 0) {
      const user = result.rows[0];
      const storedHashedPassword = user.password;
      bcrypt.compare(loginPassword, storedHashedPassword, (err, result) => {
        if (err) {
          console.log("Error comparing password.", err);
        } else {
          if (result) {
            // Result was true, so render the secret page.
            res.render("secrets.ejs");
          } else {
            // Result was false, so indicate incorrect password.
            res.send("Incorrect Password");
          }
        }
      });
    } else {
      res.send("User not found");
    }
  } catch (err) {
    console.log(err);
  }
});
```

### Managing Cookies and Sessions

- The `passport` Node module manages cookies and sessions.
  - https://www.passportjs.org/
  - Includes 'strategies' that allow people to , for example, login with Twitter, Facebook, Apple, etc.  
- `passport` requires the following Node modules:
  - `express-session` enables session persistence by saving the cookie to the user's browser.
  - `passport`
  - `passport-local` enables username and password to your local database.



```js
import express from "express";
import bodyParser from "body-parser";
import pg from "pg";
import bcrypt from "bcrypt";
// Allows us to set up a new session to start saving user login sessions.
import session from "express-session";
import passport from "passport";
// Use a local Passport 'stategy' to authenticate locally
// (i.e., with our database rather than an external service). 
// This is also know as a local strategy.
import { Strategy } from "passport-local";

const app = express();
const port = 3000;
const saltRounds = 10;

app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static("public"));

/*
  Use session as a middleware, create a new instance, and pass in some options.
  Options we're configuring:
  secret: a secret used to sign the session cookie.
    This is used as the key to keep the session secret.
    Because we're bypassing the usename and password, we
    need to make sure we're protecting the user's login information.
  resave: a setting that allows us to save a session to a database.
    E.g., even if server restarts, sessions can be restored from Postgres.
  saveUninitialized: do we want to save the session to the server's memory
*/
app.use(session({
  // TODO See next section about using environmental variables.
  secret: "TOPSECRETWORD",
  resave: false,
  saveUninitialized: true,
  // cookie can be omitted if you want the session to
  // end once the browser is closed.
  cookie: {
    // number of milliseconds a cookie should persist
    // (even after closing a browser)
    maxAge: 1000 * 60 * 60 * 24, // Persist for 1 day (86400000 ms).
  }
}));

// Passport configuration must occur AFTER establishing
// the session initialization above.
app.use(passport.initialize());
app.use(passport.session());

// TODO These values should be stored as environmental variables.
const db = new pg.Client({
  user: "postgres",
  host: "localhost",
  database: "secrets",
  password: "123456",
  port: 5432,
});
db.connect();

app.get("/", (req, res) => {
  res.render("home.ejs");
});

app.get("/login", (req, res) => {
  res.render("login.ejs");
});

app.get("/register", (req, res) => {
  res.render("register.ejs");
});

app.post("/register", async (req, res) => {
  const email = req.body.username;
  const password = req.body.password;

  // try {
  //   const checkResult = await db.query("SELECT * FROM users WHERE email = $1", [
  //     email,
  //   ]);
  //   if (checkResult.rows.length > 0) {
  //     res.send("Email already exists. Try logging in.");
  //   } else {
  //     //hashing the password and saving it in the database
  //     bcrypt.hash(password, saltRounds, async (err, hash) => {
  //       if (err) {
  //         console.error("Error hashing password:", err);
  //       } else {
  //         console.log("Hashed Password:", hash);
  //         await db.query(
  //           "INSERT INTO users (email, password) VALUES ($1, $2)",
  //           [email, hash]
  //         );
  //         res.render("secrets.ejs");
  //       }
  //     });
  //   }
  // } catch (err) {
  //   console.log(err);
  // }

  // Updated to use Passport
  try {
    const checkResult = await db.query(
      "SELECT * FROM users WHERE email = $1", 
      [email,]
    );
    if (checkResult.rows.length > 0) {
      res.send("Email already exists. Try logging in.");
    } else {
      // Hashing the password and saving it in the database
      bcrypt.hash(password, saltRounds, async (err, hash) => {
        if (err) {
          console.error("Error hashing password:", err);
        } else {
          console.log("Hashed Password:", hash);
          const result = await db.query(`
            INSERT INTO users (email, password)
            VALUES ($1, $2)
            RETURNING *
            `,
            [email, hash]
          );
          const user = result.rows[0];
          // This print the hashed password to the console, so it's acceptable.
          console.log("Registered User:", user);
          // Use req.login() from Passport, not req.logIn().
          req.login(user, (err) => {
            if (err) {
              console.log(err);
            } else {
              res.redirect("/secrets");
            }
          });
        }
      });
    }
  } catch (err) {
    console.log(err);
  }
});

app.get("/secrets", (req, res) => {
  // We added this user with Passport when verifying.
  console.log(req.user);
  
  // isAuthenticated() comes from the Passport module,
  // which allows the user to access a page if they already
  // logged in and have an active session.
  if (req.isAuthenticated()) {
    res.render("secrets.ejs");
  } else {
    // You may see a cookie for 'http://localhost:3000' under
    // Chrome developer tools > Application (tab) > Cookies (left pane)
    res.redirect("/login");
  }
});

app.post(
  "/login", 
  // async (req, res) => {
  //   /*
  //     We don't need to get req.body form data when using Passport.
  //     Passport automatically grabs this 
  //     content from HTML form submissions.
  //   */
  //   // const email = req.body.username;
  //   // const loginPassword = req.body.password;
  //
  //   // -- MOVED TO THE NEW Passport Strategy DEFINITION. -- 
  //   // try {
  //   //   const result = await db.query("SELECT * FROM users WHERE email = $1", [
  //   //     email,
  //   //   ]);
  //   //   if (result.rows.length > 0) {
  //   //     const user = result.rows[0];
  //   //     const storedHashedPassword = user.password;
  //   //     bcrypt.compare(loginPassword, storedHashedPassword, (err, result) => {
  //   //       if (err) {
  //   //         console.error("Error comparing passwords:", err);
  //   //       } else {
  //   //         if (result) {
  //   //           res.render("secrets.ejs");
  //   //         } else {
  //   //           res.send("Incorrect Password");
  //   //         }
  //   //       }
  //   //     });
  //   //   } else {
  //   //     res.send("User not found");
  //   //   }
  //   // } catch (err) {
  //   //   console.log(err);
  //   // }
  // }
  /// Use Passport as middleware instead of using a callback.
  /// This will trigger the strategy used to authenticate users.
  passport.authenticate("local", { // Specifies which strategy to use, in case you have > 1
    successRedirect: "/secrets",
    failureRedirect: "/login"
  })
);

app.get("/logout", (req, res) => {
  // Use req.logout() for use with Passport, not req.logOut().
  req.logout((err) => {
    if (err) console.log(err);
      res.redirect("/");
  });
});

// Place this just above our app.listen() method.
// Register a new strategy.
// Note: in the Passport world, `cb` is used as shorthand for callback.
// Note: the `verify` funciton argument names need to match the names from
//  the form that submits the login request.
// NOTE: Passport is triggered whenever we try to authenticate a new user,
//  so we'll end up in our `verify` function. 
passport.use(
  "local", // Gives the strategy a name
  new Strategy(async function verify(username, loginPassword, cb) {
    /// DON'T CONSOLE LOG PASSWORDS AS PLAIN TEXT!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    console.log(
      "Local Strategy's verify function arguments from HTML form:", 
      username,
      loginPassword
    );

    try {
      const result = await db.query("SELECT * FROM users WHERE email = $1", [
        // email,  // changed to username to match the HTML form.
        username,
      ]);
      if (result.rows.length > 0) {
        const user = result.rows[0];
        const storedHashedPassword = user.password;
        bcrypt.compare(loginPassword, storedHashedPassword, (err, result) => {
          if (err) {
            console.error("Error comparing passwords:", err);
            return cb(err);
          } else {
            if (result) {
              // res.render("secrets.ejs");
              // When using Passport, instead of res.rendering secrets.ejs,
              // we'll pass a callback here.
              // 
              // `cb` will recieve either an error or user data when
              // called from the verify function.
              // 
              // Note: the error value is set to null because no
              //  error occurred if the bcrypt.compare result was true.
              return cb(null, user);
            } else {
              // res.send("Incorrect Password");
              // The user entered an incorrect password, so set
              // isAuthenticated() to false.
              return cb(null, false);
            }
          }
        });
      } else {
        // res.send("User not found");
        return cb("User not found");
      }
    } catch (err) {
      console.log(err);
      return cb(err);
    }
  }
));

// Save the data of the user that's logged in to local storage.
// We can use the callback to pass over any information of the user.
passport.serializeUser((user, cb) => {
  cb(null, user);
});

// Saves users information (e.g., id, email) to the local session, and
// deserializes it into a usable form.
passport.deserializeUser((user, cb) => {
  cb(null, user);
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

### Level 5 - Hide your Secrets with Environment Variables

- https://www.npmjs.com/package/dotenv

#### How to use the Dotenv module:

1. Create a `.env` file in the root of your project folder.
2. Add the `.env` file to a `.gitignore` file.
   1. GitHub's list of files you probably want to ignore:
      1. https://github.com/github/gitignore/blob/main/Node.gitignore
3. Give your variable a name and assign a value (See example below).
   1. The name is in all caps by convention.
   2. Don't add spaces on either side of the equal sign. 
4. Import the dotenv module in all JS files that need to access environmental variables.
   1. `import env from "dotenv";`
5. Initialize env
   1. `env.config();`

#### .env file

```.env
SESSION_SECRET="TOPSECRETWORD"
PG_USER="postgres"
PG_HOST="localhost"
PG_DATABASE="secrets"
PG_PASSWORD="123456"
PG_PORT="5432"
```

#### index.js file

```js
app.use(
  session({
    secret: "TOPSECRETWORD",
    resave: false,
    saveUninitialized: true,
  })
);
// Becomes
app.use(
  session({
    secret: process.env.SESSION_SECRET,
    resave: false,
    saveUninitialized: true,
  })
);
```



### Use OAuth to Sign in with Google:

- "Scopes are the fields that you will receive once the user logs in through google. We're just interested in the email so click on "Add Or Remove Scopes". And add a checkmark:"
  - Select ".../auth/userinfo.email" "See your primary Google Account email address" to receive the user's email address.

#### Create an OAuth Client ID for the Secrets project:

- Navigate to https://console.cloud.google.com/ and sign in with your Google/gmail account.
- Create a new Project
- Go to the "API & Services" page.
- You need to create an OAuth Client ID in the "Credential" tab by clicking on the "Create Credentials" button.
- Select "Web Application" as the application type.
- Set the "Authorized JavaScript origins" to `http://localhost:3000` for local development.
- Set the "Authorized redirect URIs" to `http://localhost:3000/auth/google/secrets`.
  - This is the path where your users are redirected to after they have authenticated with google. You basically want to show your logged in users the secret page, so that's what you need to configure here.
- Click 'Create'.
- Copy the Client ID and Secret Key ("Client Secret") and save it (securely).



Auth Code: One time access

Access Token: Extended access (E.g., one year)

## Section 36 - React.js

This HTML template below is all that's needed for a React App. All of the UI development is handled through the index.js script, which will replace elements on the page.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>React App</title>
    <link rel="stylesheet" href="styles.css" />
  </head>

  <body>
    <div id="root"></div>
    <script src="../src/index.js" type="text/javascript"></script>
  </body>
</html>
```



React requires the following npm packages:

- `react`
- `react-dom`

The following code will replace the div, having an ID of "root", in the HTML template above with **Hello World!**.

 ```react
 //var React = require("react");
 //var ReactDOM = require("react-dom");
 import React from "react";
 import ReactDOM from "react-dom";
 
 // NOTE: HTML is NOT to be placed in quotes. 
 //       This file is parsed and the HTML is compiled/converted into JavaScript.
 //       The react modules, imported above, are what allows this functionality.
 // ReactDOM.render(<What to show>, <where to show it>);
 ReactDOM.render(<h1>Hello World!</h1>, document.querySelector("#root"));
 // ReactDOM.render(<h1>Hello World!</h1>, root); // Simply entering the element ID seems to work too...
 ```



React uses **Babel**, a JavaScript compiler that takes more modern versions of JS code and compiles it into a more universally compatible version.

https://babeljs.io/



The `render` method can only accept a single root tag. For example, `<h1>text</h1>` includes a single root tag, the h1 tag, and is acceptable, but `<h1>text</h1><p>text</p>` has two root tags, the h1 tag and p tag, so the render method won't work.



Populate HTML template content with JS variables:

```react
const fName = "Angela";
const lName = "Yu";
ReactDOM.render(
  <h1>
    Hello {fName} {lName}!
  </h1>,
  document.getElementById("root")
);
```



```react
import React from "react";
import ReactDOM from "react-dom";

const name = "Dario Bianco";
const currentYear = new Date().getFullYear();

ReactDOM.render(
  <div>
    <p>Created by {name}.</p>
    <p>© {currentYear} {name}</p>
  </div>,
  root
);
```



### Section 284 - JSX Attributes and Styling React Elements

The hardcoding the attribute `class` in an HTML element in `<h1 class="heading">My Favourite Foods</h1>`, will throw a warning because the proper attribute name for `class` is `className`. Replacing `class` with `className` will clear the warning.

```react
import React from "react";
import ReactDOM from "react-dom";

ReactDOM.render(
  <div>
    <h1 className="heading"  contentEditable="true" spellCheck="false" >My Favourite Foods</h1>
  </div>,
  document.getElementById("root")
);
```

HTML Global Attributes - https://www.w3schools.com/tags/ref_standardattributes.asp

When setting HTML elements' HTML Global Attributes in React JSX files, use camelcase for the attribute names even though the HTML Global Attribute names are all lowercase. E..g., `contenteditable` becomes `contentEditable` and `font-size` become `fontSize`.

RECOMMENDATION

- Apply styling for HTML elements **through classes**, that are defined in CSS files.
- Use **kabob-case** for class names.

#### JSX vs JavaScript

The error, `Uncaught SyntaxError: Unexpected token '<'`, in the browser console results from the browser not recognizing the '<' symbol in the index.js file. The browser doesn't know that the JS file is a JSX file that includes HTML elements.

Change "text/javascript" in the script tag to "text/JSX" to clear the error.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>React App</title>
    <link rel="stylesheet" href="styles.css" />
  </head>

  <body>
    <div id="root"></div>
    <script src="../src/index.js" type="text/JSX"></script>
  </body>
</html>
```



### Section 285 - Inline Styling for React Elements

```react
ReactDOM.render(
  <h1 style={{ color: "red" }}>Hello World!</h1>,
  document.getElementById("root")
);
```

CSS style values need to be strings and spaces need to be preserved between colons and the value strings.

```react
import React from "react";
import ReactDOM from "react-dom";

const customStyle = {
  color: "red",
  fontSize: "20px",
  border: "1px solid black",
};

customStyle.color = "blue";
customStyle.textDecoration = "underline";

ReactDOM.render(
  <h1 style={customStyle}>Hello World!</h1>,
  document.getElementById("root")
);
```



### Section 287 - React Components

Airbnb React/JSX Style Guide - https://github.com/airbnb/javascript/tree/master/react

React functions names should be in Pascal Case.

```console
project-root/
│
├── src/
    ├── index.js
    ├── components/
        ├── App.jsx
        ├── List.jsx
        └── Heading.jsx
```

index.js

```react
import React from "react";
import ReactDOM from "react-dom";
import App from "./components/App";

ReactDOM.render(<App />, document.getElementById("root"));

```

App.jsx

```jsx
import React from "react";
import Heading from "./Heading";
import List from "./List";

function App() {
  return (
    <div>
      <Heading />
      <List />
    </div>
  );
}

export default App;

```

Heading.jsx

```JSX
import React from "react";

function Heading() {
  return <h1>My Favourite Foods</h1>;
}

export default Heading;
```

List.jsx

```jsx
import React from "react";

function List() {
  return (
    <ul>
      <li>Bacon</li>
      <li>Jamon</li>
      <li>Noodles</li>
    </ul>
  );
}

export default List;
```



### Section 288 - React Components Practice

projectRoot/public/index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>JSX</title>
    <link rel="stylesheet" href="styles.css" />
  </head>

  <body>
    <div id="root"></div>
    <script src="../src/index.js" type="text/JSX"></script>
  </body>
</html>

```

projectRoot/src/style.css

```css
.heading {
  border: 5px solid black;
}
```

projectRoot/src/index.js

```jsx
//Create a React app from scratch.
import React from "react";
import reactDom from "react-dom";
import App from "./components/App";
// This styles.css import is redundant because
// the public style.css file is linked to in
// the index.html file header.
// import "./../public/styles.css";

reactDom.render(<App />, root);
// reactDom.render(<App />, document.getElementById("root"));
```

projectRoot/src/components/App.jsx

```jsx
//Create a React app from scratch.
import React from "react";
import Heading from "./Heading";

function App() {
  return (
    <div>
      <Heading />
    </div>
  );
}

export default App;
```

projectRoot/src/components/Heading.jsx

```jsx
//Create a React app from scratch.
import React from "react";

function Heading() {
  const now = new Date();
  // now.setHours(11);
  // now.setHours(13);

  const startOfDay = new Date();
  startOfDay.setHours(0, 0, 0, 0);

  const noon = new Date();
  noon.setHours(12, 0, 0, 0);

  const sixPM = new Date();
  sixPM.setHours(18, 0, 0, 0);

  let greeting;
  const customStyle = {};

  if (now.getTime() < noon.getTime()) {
    //Show a single h1 that says "Good morning" if between midnight and 12PM.
    greeting = "Good Morning";
    customStyle.color = "red";
  } else if (now.getTime() < sixPM.getTime()) {
    //or "Good Afternoon" if between 12PM and 6PM.
    greeting = "Good Afternoon";
    customStyle.color = "green";
  } else {
    //or "Good evening" if between 6PM and midnight.
    greeting = "Good evening";
    customStyle.color = "blue";
  }

  //Apply the "heading" style in the styles.css
  //Dynamically change the color of the h1 using inline css styles.
  //Morning = red, Afternoon = green, Night = blue.

  return (
    <h1 className="heading" style={customStyle}>
      {greeting}
    </h1>
  );
}

export default Heading;

```



### 293 - React Props

Properties, or props, are like function attributes, but for React components.

You can't define custom props, you're limited to HTML element attributes. 

- E.g., some attributes can be found here: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attributes

```jsx
<div>
  <Card
    className="my-style-APPLYING A CLASS HERE (DIRECTLY) WON'T WORK BECAUSE CLASSNAME IS ACCESED VIA PROPS.CLASSNAME"
    name="Beyonce"
    src="https://..."
    tel="+123 456 789"
    email="b@beyonce.com"
  />
</div>
```

```jsx
import React from "react";

function Card(props) {
  console.log(props); // prints `Object {name: "Beyonce"}` in browser console.
  
  return (
    <div className="my-style">
      <h2>{props.name}</h2>
      <img src={props.src} alt="avatar image" />
      <p>{props.tel}</p>
      <p>{props.email}</p>
    </div>
  );
}
```



### 298 - Javascript ES6 Map/Filter/Reduce



```js
var numbers = [ 3, 56, 2, 48, 5];
// Find the first item that matches from an array
const newNumber = numbers.find(function (num) {
  return number > 3;
})
console.log(newNumber); // logs 56
```



```js
var numbers = [ 3, 56, 2, 48, 5];
// Find the first item that matches from an array
const findIndex = numbers.findIndex(function (num) {
  return number > 3;
})
console.log(findIndex); // logs index 1
```



> Single Responsibility Principle

### 306 React Hooks - useState

```jsx
//import React from "react";
import React, { useState } from "react";

function App() {
  //const state = React.useState(0);
  //const state = useState(0);	// The value in the parenthasis is the default value for the state.
  //console.log(state[0]);
  
  // Destructuring useState will automatically get the first element.
  // count, the first element, is the variable that we set.
  // setCount is a callback, called a stateful setter, that sets the
  // state of the variable, count.
  const [count, setCount] = useState(0);
  
  // Destructuring Example
  const [red, green, blue] = [9, 132, 227];
  
  function increase() {
    setCount(count + 1);
  }
  return (
    <div className="container">
    	<!--<h1>{state[0]}</h1>-->
      <h1>{count}</h1>
      <button onClick={increase}>+</button>
    </div>
  );
}

export default App;
```



### 309 React Forms

```jsx
import React, { useState } from "react";

function App() {
  const [name, setName] = useState("");
  const [heading, setHeading] = useState("");

  function handleChange(event) {
    // event is the event that triggered the onChange event.
    // target is the elements that triggered the event.
    // value is a property of the target.
    setName(event.target.value);
    console.log(event.target.value);
  }

  function handleClick(event) {
    event.preventDefault();
    setHeading(name);
  }

  // We make the React state be the “single source of truth”
  // by setting value={name} in the input element.
  // Because the value attribute is set on our form
  // element, the displayed value will always be this.state.value
  return (
    <div className="container">
      <h1>Hello {name}</h1>
      <input
        onChange={handleChange}
        type="text"
        placeholder="What's your name?"
        value={name}
      />
      <button>Submit</button>

      <hr/>
      <form onSubmit={handleClick}>
        <h1>Hello {heading}</h1>
        <input
          onChange={handleChange}
          type="text"
          placeholder="What's your name?"
          value={name}
        />
        <button type="submit">Submit</button>
      </form>
    </div>
  );
}
export default App;

```



https://legacy.reactjs.org/docs/forms.html#controlled-components

> In HTML, form elements such as `<input>`, `<textarea>`, and `<select>` typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, and only updated with [`setState()`](https://legacy.reactjs.org/docs/react-component.html#setstate).
>
>  We can combine the two by making the React state be the “single source of truth”. Then the React component that renders a form also controls what happens in that form on subsequent user input. An input form element whose value is controlled by React in this way is called a “controlled component”.

 

### 311 Changing Complex State

```jsx
import React, { useState } from "react";

function App() {
  const [fullName, setFullName] = useState({
    fName: "",
    lName: ""
  });

  function handleChange(event) {
    const { value, name } = event.target;

    // Don't try to access the event object within a stateful setter
    setFullName(prevValue => {
      if (name === "fName") {
        return {
          fName: value,
          lName: prevValue.lName
        };
      } else if (name === "lName") {
        return {
          fName: prevValue.fName,
          lname: value
        };
      }
    });
  }

  return (
    <div className="container">
      <h1>
        Hello {fullName.fName} {fullName.lName}
      </h1>
      <form>
        <input
          name="fName"
          onChange={handleChange}
          placeholder="First Name"
          value={fullName.fName}
        />
        <input
          name="lName"
          onChange={handleChange}
          placeholder="Last Name"
          value={fullName.lName}
        />
        <button>Submit</button>
      </form>
    </div>
  );
}

export default App;

```



### 312 Changing Complex State Practice

```jsx
import React, { useState } from "react";
function App() {
  const [contact, setContact] = useState({
    fName: "",
    lName: "",
    email: "",
  });

  function updateContact(event) {
    console.log(event.target.value);

    const { value, name } = event.target;

    setContact((prevValue) => {
      //return {
      //  fName: name == "fName" ? value : prevValue.fName,
      //  lName: name == "lName" ? value : prevValue.lName,
      //  email: name == "email" ? value : prevValue.email,
      //};
      return {
        ...prevValue,
        [name]: value // You need the backets or the key name will be 'name' rather than 'fName', 'lName', or 'email'.
      }
    });
  }

  return (
    <div className="container">
      <h1>
        Hello {contact.fName} {contact.lName}
      </h1>
      <p>{contact.email}</p>
      <form>
        <input
          name="fName"
          placeholder="First Name"
          onChange={updateContact}
          value={contact.fName}
        />
        <input
          name="lName"
          placeholder="Last Name"
          onChange={updateContact}
          value={contact.lName}
        />
        <input
          name="email"
          placeholder="Email"
          onChange={updateContact}
          value={contact.email}
        />
        <button>Submit</button>
      </form>
    </div>
  );
}
export default App;

```



> ==**Parallel Typing**==
>
> To type the same thing on separate lines simultaneously:
>
> - Hold down the option key (Mac) or the ALT key (Windows) in VS Code,
> - Click on the locations you would like to start typing, and
> - Type. **Characters will be added in all the locations you clicked as you type.**





https://stackoverflow.com/questions/11508463/javascript-set-object-key-by-variable?noredirect=1&lq=1

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax



```js
const citrus = ["Lime", "Lemon", "Orange"];
const fruits = ["Apple", ...citrus, "Banana", "Coconut"];

const fullName = {
  fName: "James",
  lName: "Bond"
};

const user = {
  ...fullName,
  id: 1,
  username: "jamesbond007"
};

console.log(user);
```

