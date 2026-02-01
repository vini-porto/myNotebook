# What is CSS?

**[[CSS]]** (Cascading Style Sheets): The presentation layer of the web.

**The analogy**:

- **HTML** = The Skeleton (Structure)
- **CSS** = The Skin, Clothing, and Makeup (Presentation)

**Purpose**: Transform raw HTML structure into visually appealing designs.

# The Separation of Powers

**[[Separation of Concerns]]**: Keep structure and presentation separate.

- **HTML**: Nouns (Paragraph, Image, Table)

- **CSS**: Adjectives (Red, Big, Centered, Hidden)

>[!NOTE] Rule 
>We try to keep them in separate files

# The Anatomy of a CSS Rule

**[[CSS Rule]]**: The basic building block of CSS.

**Structure**:

```css
selector {
  property: value;
}
```

**Example**:

```css
h1 {
  color: blue;
}
```

## Breakdown of a CSS Rule

**1. [[Selector]]**: Who are we talking to? (`h1`)

**2. [[Property]]**: What do we want to change? (`color`)

**3. [[Value]]**: What is the new look? (`blue`)

**4. The [[Semicolon]]**: **CRITICAL!** It ends the statement.

**Syntax**:

```css
selector {
  property: value;
}
```

# Where Does CSS Go?

### Inline

**[[Inline Styles]]**: CSS written directly in the HTML tag.

```html
<h1 style="color:red">Title</h1>
```

**Assessment**: **BAD** idea. Hard to manage and maintain.

**Problem**: Violates separation of concerns; difficult to update multiple elements.

### Option 2: Internal (The 'Testing' Way)

**[[Internal Styles]]**: CSS written in the `<head>` of your HTML.

```html
<style>
  h1 { color: red; }
</style>
```

**Use case**: Good for testing or single-page sites.

### Option 3: External (The 'Professional' Way)

**[[External Stylesheet]]**: A separate `.css` file linked via HTML.

**This is what we will use** in production.

**Benefits**:

- One stylesheet for multiple pages
- Easier to maintain
- Better organization
- Cacheable (faster page loads)

## The Link Tag

**[[Link Tag]]**: Connects your HTML to your CSS file.

**Placement**: Put this in your `<head>`:

```html
<link rel="stylesheet" href="style.css">
```

**Analogy**: It tells HTML: "Go get the outfit from the closet."

**[[rel Attribute]]**: Defines the relationship (stylesheet)

**[[href Attribute]]**: Specifies the path to the CSS file

## The Big Three Selectors

The three main ways to target HTML elements:

1. **[[Element Selector]]** (The Broad Brush)
2. **[[Class Selector]]** (The Precision Tool)
3. **[[ID Selector]]** (The Nuclear Option)

## 1. Element Selector

**[[Element Selector]]**: Targets ALL tags of that type.

**Example**:

```css
p {
  color: green;
}
```

**Result**: Every single paragraph turns green.

**Use case**: Applying styles to all elements of a specific type.

## 2. Class Selector (The Best One)

**[[Class Selector]]**: Targets specific groups. Starts with a **DOT** (`.`).

**CSS**:

```css
.minion {
  background: yellow;
}
```

**HTML**:

```html
<div class="minion">Kevin</div>
```

**Syntax**: `.className` in CSS, `class="className"` in HTML.

## Why Classes Rule

**Reusability**: You can reuse them!

**Flexibility**: You can have 100 elements with `class="minion"`.

**Analogy**: Think of it like a **Uniform**—many people can wear the same style.

**Best practice**: Classes are the most commonly used selectors in professional CSS.

## 3. ID Selector

**[[ID Selector]]**: Targets ONE unique element. Starts with a **HASH** (`#`).

**CSS**:

```css
#gru {
  height: 200px;
}
```

**HTML**:

```html
<img id="gru" src="gru.jpg">
```

**Syntax**: `#idName` in CSS, `id="idName"` in HTML.

## ID vs Class

**Class** = Minions (There are many)

**ID** = Gru (There is only one)

**Critical rule**: Never use the same ID twice on a page!

**When to use**:

- **IDs**: Unique elements (one navigation, one header)
- **Classes**: Repeated styles (multiple cards, buttons)

## The Cascade (Who Wins?)

**Question**: What if I say Paragraphs are Red, but `.special` is Blue?

```css
p { color: red; }
.special { color: blue; }
```

```html
<p class="special">I am Blue!</p>
```

**Result**: The paragraph is **Blue**.

**Why?**: [[Specificity]] determines which rule wins.

## Specificity Hierarchy

**[[Specificity]]**: Determines which CSS rule is applied when multiple rules target the same element.

**Hierarchy** (from strongest to weakest):

1. **ID** (`#`) - Strongest
2. **Class** (`.`) - Medium
3. **Tag** (`p`) - Weakest

**Rule**: ID beats Class. Class beats Tag.

## Pop Quiz: Specificity

**Who wins?**

```css
#header { color: red; }
.header { color: blue; }
header { color: green; }
```

**Answer**: **Red** (The ID wins)

**Reason**: ID has the highest specificity.

## Coloring the Web

**Two main properties**:

**[[color Property]]**: Text color

**[[background-color Property]]**: Box/background color

**Example**:

```css
.minion-box {
  /* TEXT color */
  color: white;
  
  /* BOX color */
  background-color: #444;
}
```

## Color Specification Methods

### Way 1: Keywords

**[[Color Keywords]]**: Named colors like `red`, `blue`, `green`, `papayawhip`, `tomato`.

**Pros**: Easy to read

**Cons**: Limited options (~140 named colors)

### Way 2: Hex Codes

**[[Hex Codes]]**: The computer language for colors.

**Examples**:

- `#FF0000` (Red)
- `#000000` (Black)
- `#FFFFFF` (White)

**Format**: `#RRGGBB` using 0-9 and A-F

**Reality**: You don't memorize these; you use a color picker.

### Way 3: RGB / RGBA

**[[RGB]]**: Red, Green, Blue (values 0-255)

**Example**: `rgb(255, 0, 0)` is Red

**[[RGBA]]**: RGB with Alpha (opacity)

**Example**: `rgba(255, 0, 0, 0.5)` is Red at 50% opacity (see-through!)

**Alpha channel**: 0 = fully transparent, 1 = fully opaque

## Fonts

**[[font-family Property]]**: Specifies which font to use.

**Syntax**:

```css
font-family: 'Arial', sans-serif;
```

**Important**: Always list a **backup font**!

**Why?**: If the user doesn't have the first font, it tries the second.

**[[Font Stack]]**: The list of fallback fonts.

## Serif vs Sans-Serif

**[[Serif Fonts]]**: Have little "feet" (Times New Roman)

- Formal
- Traditional
- Often used in print

**[[Sans-Serif Fonts]]**: No feet (Arial, Roboto)

- Modern
- Clean
- Often used on screens

**Generic families**: Always end with `serif` or `sans-serif` as final fallback.

## Font Size

**[[px Unit]]**: Fixed size (e.g., `font-size: 16px;`)

- Absolute measurement
- Predictable

**[[rem Unit]]**: Relative size (Better for accessibility)

- Scales with user preferences
- More flexible

**Recommendation**: Start with pixels for now, learn rem later.

## Text Alignment

**[[text-align Property]]**: Controls horizontal alignment of text.

**Options**:

- `text-align: left;` (Default)
- `text-align: center;` (Great for titles)
- `text-align: right;` (Rare)
- `text-align: justify;` (Not shown but available)

## The Box Model (Vital Concept)

**[[Box Model]]**: The fundamental concept of CSS layout.

**Key principle**: **EVERYTHING in HTML is a box.**

**Even a circle**: A circle image is technically inside a square box.

## The Layers of the Box

**[[Box Model Layers]]** (from inside to outside):

1. **[[Content]]** (The middle) - The actual content (text, images)
2. **[[Padding]]** (Space inside) - Space between content and border
3. **[[Border]]** (The line) - Edge of the element
4. **[[Margin]]** (Space outside) - Space between elements

## Padding vs Margin

### Padding

**[[Padding]]**: Like wearing a puffy coat. It increases YOUR size.

**Effect**: Makes the element itself bigger

**Inside the box**: Part of the element's background

### Margin

**[[Margin]]**: Like personal space. It pushes OTHERS away.

**Effect**: Creates space around the element

**Outside the box**: Transparent, pushes other elements away

## Visualizing Padding

**CSS**:

```css
.box {
  background: red;
  padding: 20px;
}
```

**HTML**:

```html
<div class="box">
  I am content inside the box! Notice how the padding keeps me away from the edges.
</div>
```

**Result**: The red color grows because padding is INSIDE the box.

**Effect**: Content is pushed away from edges; red background expands.

## Visualizing Margin

**CSS**:

```css
.box {
  background: red;
  margin: 20px;
}
```

**HTML**:

```html
<div class="box">Look – I have a margin</div>
```

**Result**: The red color stays small. The box just moves away from neighbors.

**Effect**: White space appears around the box; background doesn't change size.

## Borders

**[[border Property]]**: Adds an edge to an element.

**Syntax**: `border: width style color;`

**Example**:

```css
border: 5px solid black;
```

**Components**:

- **Width**: Thickness (e.g., `5px`)
- **Style**: `solid`, `dashed`, `dotted`, `double`
- **Color**: Any valid color value

**Example**:

```css
.solid-box {
  border: 5px solid black;
}
```

## Centering Things

### Centering Text

**To center text**: `text-align: center;`

**Example**:

```css
.center-text {
  text-align: center;
  background: lightyellow;
}
```

### Centering a Block

**To center a Block** (like an image or div):

```css
margin: 0 auto;
```

**Meaning**:

- `0` = top/bottom margin
- `auto` = automatic left/right margin (centers the element)

**Requirement**: Element must have a specified width.

## Styling Images

**Make them responsive!**

**[[Responsive Images]]**: Images that scale with their container.

**CSS**:

```css
.responsive-img {
  max-width: 100%; 
  height: auto; 
  display: block;
}
```

**HTML**:

```html
<img class="responsive-img" src="horse.jpg" alt="Horse Riding">
```

**Result**: Images won't overflow on mobile phones.

**Explanation**:

- `max-width: 100%`: Never wider than container
- `height: auto`: Maintains aspect ratio
- `display: block`: Prevents extra space below image

## The Developer Tools

**[[Developer Tools]]**: Built-in browser tool for inspecting and testing CSS.

**How to access**: Right Click → Inspect

**Key feature**: Look at the **Styles** pane

**Live editing**: You can edit CSS live to test ideas!

**Your best friend**: This is the most powerful tool for learning and debugging CSS.

**VS Code alternative**: Live Preview in VS Code provides similar testing environment.

## Common Mistakes

1. **Forgetting the semicolon** (`;`)
2. **Forgetting the curly braces** (`{}`)
3. **Typos** (`colr` instead of `color`)
4. **Editing the CSS file but forgetting to `<link>` it** in HTML
5. **Using wrong selector syntax** (forgetting `.` for classes or `#` for IDs)

## Lab #4 Preview

**Project**: The 'Wanted' Poster

**Goal**: Create a Wanted Poster for a Minion.

**Required elements**:

- Custom Fonts
- Borders (Dashed?)
- Background Colors
- Text Alignment

**Purpose**: Practice basic CSS styling techniques.

## Final Thought

**Reality**: CSS is **huge**. We are just scratching the surface.

**Expectation**: Don't panic if it doesn't look perfect yet.

**Goal**: Just make it colorful.

**Approach**: Experiment, test, and iterate.

---

## Review Questions

1. What is CSS and what does it stand for?
    
2. Using the body analogy, explain the difference between HTML and CSS.
    
3. Why is it important to keep HTML and CSS in separate files?
    
4. List at least 5 reasons why we need CSS.
    
5. What are the four parts of a CSS rule? Describe each.
    
6. What are the three ways to include CSS in an HTML document? Which is best and why?
    
7. Write the `<link>` tag to connect an external stylesheet called "styles.css" to your HTML.
    
8. What are the three main types of CSS selectors? How do you write each in CSS?
    
9. How many times can you use the same class on a single HTML page? How many times can you use the same ID?
    
10. What is specificity? Which selector type is strongest: ID, class, or element?
    
11. Given these rules, what color will the `<h1>` be?
    
    ```css
    h1 { color: green; }
    .title { color: blue; }
    #main-title { color: red; }
    ```
    
    ```html
    <h1 id="main-title" class="title">Hello</h1>
    ```
    
12. What is the difference between the `color` property and the `background-color` property?
    
13. Name three ways to specify colors in CSS. Give an example of each.
    
14. What is RGBA and how is it different from RGB?
    
15. Why should you always include a backup font in your `font-family` declaration?
    
16. What's the difference between serif and sans-serif fonts? Give an example of each type.
    
17. What is the Box Model? List the four layers from inside to outside.
    
18. Explain the difference between padding and margin using the analogies from the lecture.
    
19. If an element has `background: red; padding: 20px;`, what color is the padding area?
    
20. Write CSS to create a border that is 3 pixels wide, dashed style, and black color.
    
21. How do you center text inside an element? How do you center a block element (like a div or image)?
    
22. What CSS would you use to make an image responsive (not overflow on mobile)?
    
23. What are the Developer Tools and how do you access them in a browser?
    
24. Fix this broken CSS:
    
    ```css
    p {
      colr: blue
      background-color: yellow;
    }
    ```
    
25. You created a CSS file called "style.css" but the styles aren't showing up on your webpage. What are three possible reasons why?
    
26. Write CSS using a class selector to:
    
    - Set text color to white
    - Set background color to navy blue
    - Add 15px of padding
    - Center the text
27. Write CSS using an ID selector for an element called "header" that:
    
    - Has a solid black border, 2px wide
    - Has a light gray background (#f0f0f0)
    - Centers its text
28. What's wrong with this HTML?
    
    ```html
    <div id="special">First</div>
    <div id="special">Second</div>
    ```
    
29. Create a responsive image class that ensures images never exceed their container width and maintain their aspect ratio.
    
30. Using the box model, explain what happens to an element's total width when you add padding and borders.
    

---

## Practical Exercises

### Exercise 1: Basic Selectors

Create CSS rules to: a) Make all paragraphs have blue text b) Make all elements with class "highlight" have yellow background c) Make the element with id "logo" be 200px wide

### Exercise 2: The Box Model

Create a class called "card" that has:

- Light blue background (#e3f2fd)
- 20px padding on all sides
- 1px solid border in gray
- 10px margin on all sides

### Exercise 3: Typography

Style a page with:

- Headings in Arial, bold, 32px
- Paragraphs in Georgia, 16px
- A class "special" that centers text and makes it red

### Exercise 4: Color Experimentation

Create three boxes using different color methods:

- One with named colors
- One with hex codes
- One with RGBA (include some transparency)

### Exercise 5: Specificity Challenge

Predict what color each element will be:

```css
p { color: green; }
.intro { color: blue; }
#main { color: red; }
```

```html
<p>Normal paragraph</p>
<p class="intro">Intro paragraph</p>
<p id="main">Main paragraph</p>
<p class="intro" id="main">Both paragraph</p>
```

### Exercise 6: Complete Page Styling

Create a simple webpage with:

- External stylesheet
- Custom background color
- Centered heading with custom font
- Paragraphs with readable text color
- A responsive image
- At least 3 different classes applied

### Exercise 7: Border Styles

Create four boxes, each with different border styles:

- Solid
- Dashed
- Dotted
- Double

All borders should be 3px and colored differently.

### Exercise 8: Responsive Design

Create a class for images that:

- Never exceeds 100% of container width
- Maintains aspect ratio
- Centers on the page
- Has 10px margin on all sides

---

## Common Mistakes to Avoid

1. **Forgetting semicolons** - Every CSS declaration must end with `;`
2. **Missing curly braces** - Rules must be wrapped in `{ }`
3. **Typos in property names** - `colr` vs `color`, `backgrond` vs `background`
4. **Not linking the stylesheet** - Forgetting the `<link>` tag in HTML
5. **Wrong path in href** - `href="style.css"` when file is in `css/style.css`
6. **Using same ID multiple times** - IDs must be unique on a page
7. **Forgetting the dot for classes** - `.className` not `className`
8. **Forgetting the hash for IDs** - `#idName` not `idName`
9. **Inline styles everywhere** - Hard to maintain; use external stylesheet
10. **Not using browser DevTools** - Missing the best debugging tool
11. **Confusing padding and margin** - Padding inside, margin outside
12. **Not specifying units** - `padding: 20` should be `padding: 20px`
13. **Overusing IDs for styling** - Classes are more flexible
14. **Not testing on different browsers** - What works in Chrome may look different in Safari
15. **Making images too large** - Use `max-width: 100%` for responsiveness

---

## CSS Quick Reference

### Selectors

```css
p { }              /* Element selector */
.className { }     /* Class selector */
#idName { }        /* ID selector */
```

### Colors

```css
color: red;                    /* Named color */
color: #ff0000;               /* Hex code */
color: rgb(255, 0, 0);        /* RGB */
color: rgba(255, 0, 0, 0.5);  /* RGBA with transparency */
```

### Text

```css
font-family: Arial, sans-serif;
font-size: 16px;
text-align: center;
```

### Box Model

```css
padding: 20px;              /* All sides */
padding: 10px 20px;         /* Vertical | Horizontal */
margin: 0 auto;             /* Centers block element */
border: 1px solid black;    /* Width | Style | Color */
```

### Common Properties

```css
background-color: #f0f0f0;
max-width: 100%;
height: auto;
display: block;
```

---

## Practical Tags for Obsidian

#CSS #WebDesign #Styling #Frontend #CascadingStyleSheets #WebDevelopment #BoxModel #CSSSelectors #Typography #ColorTheory #ResponsiveDesign #WebStyling #HTMLCSS #CSSBasics #VisualDesign #UserInterface #WebLayout #CSSProperties #Specificity #DeveloperTools