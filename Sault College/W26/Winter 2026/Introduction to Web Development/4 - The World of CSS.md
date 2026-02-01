# What is CSS?

**[[CSS]]** (Cascading Style Sheets): The presentation layer of the web.

- **HTML** = The Skeleton (Structure)

- **CSS** = The Skin, Clothing, and Makeup (Presentation)

>[!NOTE] Purpose 
>Transform raw HTML structure into visually appealing designs.

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

## Inline

**[[Inline Styles]]**: CSS written directly in the HTML tag.

```html
<h1 style="color:red">Title</h1>
```

**Assessment**: **BAD** idea. Hard to manage and maintain.

>[!NOTE] Problem 
Violates separation of concerns; difficult to update multiple elements.

## Internal

**[[Internal Styles]]**: CSS written in the `<head>` of your HTML.

```html
<style>
  h1 { color: red; }
</style>
```

>[!NOTE] Use case 
Good for testing or single-page sites.

## External

**[[External Stylesheet]]**: A separate `.css` file linked via HTML.

>**This is what we will use** in production.

**Benefits**:

- One stylesheet for multiple pages
- Easier to maintain
- Better organization
- Cacheable (faster page loads)

# The Link Tag

**[[Link Tag]]**: Connects your HTML to your CSS file.

**Placement**: Put this in your `<head>`:

```html
<link rel="stylesheet" href="style.css">
```

- **[[rel Attribute]]**: Defines the relationship (stylesheet)

- **[[href Attribute]]**: Specifies the path to the CSS file

# The Big Three Selectors

The three main ways to target HTML elements:

1. **[[Element Selector]]** (The Broad Brush)
2. **[[Class Selector]]** (The Precision Tool)
3. **[[ID Selector]]** (The Nuclear Option)

## Element Selector

**[[Element Selector]]**: Targets ALL tags of that type.

```css
p {
  color: green;
}
``` 

**Result**: Every single paragraph turns green.

>[!NOTE] Use case
>Applying styles to all elements of a specific type.

## Class Selector

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

### Why Classes Rule

**Reusability**: You can reuse them!

**Flexibility**: You can have 100 elements with `class="minion"`.

>[!NOTE] Best practice 
>Classes are the most commonly used selectors in professional CSS.

## ID Selector

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

>[!NOTE] Critical rule 
>Never use the same ID twice on a page!

**When to use**:

- **IDs**: Unique elements (one navigation, one header)
- **Classes**: Repeated styles (multiple cards, buttons)

# The Cascade

```css
p { color: red; }
.special { color: blue; }
```

```html
<p class="special">I am Blue!</p>
```

**Result**: The paragraph is **Blue**.

>[!NOTE]
>[[Specificity]] determines which rule wins.

# Specificity Hierarchy

**[[Specificity]]**: Determines which CSS rule is applied when multiple rules target the same element.

>[!NOTE] Hierarchy 
>1. **ID** (`#`) - Strongest
>2. **Class** (`.`) - Medium
>3. **Tag** (`p`) - Weakest

# Coloring the Web

**Two main properties**:

- **[[color Property]]**: Text color

- **[[background-color Property]]**: Box/background color

**Example**:

```css
.minion-box {
  /* TEXT color */
  color: white;
  
  /* BOX color */
  background-color: #444;
}
```

# Color Specification Methods

## Keywords

**[[Color Keywords]]**: Named colors like `red`, `blue`, `green`, `papayawhip`, `tomato`.

>[!NOTE]
>- **Pros**: Easy to read
>- **Cons**: Limited options (~140 named colors)

## Hex Codes

**[[Hex Codes]]**: The computer language for colors.

**Examples**:

- `#FF0000` (Red)
- `#000000` (Black)
- `#FFFFFF` (White)

**Format**: `#RRGGBB` using 0-9 and A-F

## RGB / RGBA

**[[RGB]]**: Red, Green, Blue (values 0-255)

**Example**: `rgb(255, 0, 0)` is Red

**[[RGBA]]**: RGB with Alpha (opacity)

**Example**: `rgba(255, 0, 0, 0.5)` is Red at 50% opacity (see-through!)

**Alpha channel**: 0 = fully transparent, 1 = fully opaque

# Fonts

**[[font-family Property]]**: Specifies which font to use.

**Syntax**:

```css
font-family: 'Arial', sans-serif;
```

>[!NOTE] Important 
>Always list a **backup font**!

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

>**Generic families**: Always end with `serif` or `sans-serif` as final fallback.

## Font Size

**[[px Unit]]**: Fixed size (e.g., `font-size: 16px;`)

- Absolute measurement
- Predictable

**[[rem Unit]]**: Relative size (Better for accessibility)

- Scales with user preferences
- More flexible

# Text Alignment

**[[text-align Property]]**: Controls horizontal alignment of text.

**Options**:

- `text-align: left;` (Default)
- `text-align: center;` (Great for titles)
- `text-align: right;` (Rare)
- `text-align: justify;` (Not shown but available)

# The Box Model

**[[Box Model]]**: The fundamental concept of CSS layout.

>[!NOTE] Key principle 
>**EVERYTHING in HTML is a box.**



## The Layers of the Box

**[[Box Model Layers]]** (from inside to outside):

1. **[[Content]]** (The middle) - The actual content (text, images)
2. **[[Padding]]** (Space inside) - Space between content and border
3. **[[Border]]** (The line) - Edge of the element
4. **[[Margin]]** (Space outside) - Space between elements

# Padding vs Margin

## Padding

**[[Padding]]**: Like wearing a puffy coat. It increases YOUR size.

**Effect**: Makes the element itself bigger

**Inside the box**: Part of the element's background

## Margin

**[[Margin]]**: Like personal space. It pushes OTHERS away.

**Effect**: Creates space around the element

**Outside the box**: Transparent, pushes other elements away

# Borders

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

# Centering Things

## Centering Text

**To center text**: `text-align: center;`

**Example**:

```css
.center-text {
  text-align: center;
  background: lightyellow;
}
```

## Centering a Block

**To center a Block** (like an image or div):

```css
margin: 0 auto;
```

**Meaning**:

- `0` = top/bottom margin
- `auto` = automatic left/right margin (centers the element)

>**Requirement**: Element must have a specified width.

# Styling Images

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

>**Result**: Images won't overflow on mobile phones.

**Explanation**:

- `max-width: 100%`: Never wider than container
- `height: auto`: Maintains aspect ratio
- `display: block`: Prevents extra space below image

# The Developer Tools

**[[Developer Tools]]**: Built-in browser tool for inspecting and testing CSS.

**How to access**: Right Click > Inspect

**Key feature**: Look at the **Styles** pane

# Review Questions

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
# CSS Quick Reference

## Selectors

```css
p { }              /* Element selector */
.className { }     /* Class selector */
#idName { }        /* ID selector */
```

## Colors

```css
color: red;                    /* Named color */
color: #ff0000;               /* Hex code */
color: rgb(255, 0, 0);        /* RGB */
color: rgba(255, 0, 0, 0.5);  /* RGBA with transparency */
```

## Text

```css
font-family: Arial, sans-serif;
font-size: 16px;
text-align: center;
```

## Box Model

```css
padding: 20px;              /* All sides */
padding: 10px 20px;         /* Vertical | Horizontal */
margin: 0 auto;             /* Centers block element */
border: 1px solid black;    /* Width | Style | Color */
```

## Common Properties

```css
background-color: #f0f0f0;
max-width: 100%;
height: auto;
display: block;
```

---

# Tags

#CSS #WebDesign #Styling #Frontend #CascadingStyleSheets #WebDevelopment #BoxModel #CSSSelectors #Typography #ColorTheory #ResponsiveDesign #WebStyling #HTMLCSS #CSSBasics #VisualDesign #UserInterface #WebLayout #CSSProperties #Specificity #DeveloperTools

[^1]: 
