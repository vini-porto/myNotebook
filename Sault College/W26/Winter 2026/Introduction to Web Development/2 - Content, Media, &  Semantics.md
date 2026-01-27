# Tags vs Elements

- [[HTML Tag]]: The code bits (e.g. `<p> </p>`)
- [[HTML Element]]: The complete package consisting (e.g. tag + content)

# Self-Closing Tags
## Container Tags vs Void Elements

[[Container Tags]]: Most elements have an opening and closing tag:

```html
<p>...</p>
<div>...</div>
```
Self-Closing Tags act alone with no closing tag:
- `<br>` - Line break
- `<hr>` - Horizontal rule
- `<img>` - Image
# Organizing Data
## Why does it matter?

The web is mostly lists: almost everything you see online is a list in disguise
 - Search results
- Navigation bars
- Instagram feeds
- Todo lists
- Shopping carts
##  Working With Lists

[[Unordered List]] (`<ul>`): Use when order doesn't matter. (e.g. Bullet points)

```html
<ul>
  <li>Bananas</li>
  <li>Goggles</li>
  <li>Oxygen</li>
  <li>A Despicable Master</li>
</ul>
```

[[Ordered List]] (`<ol>`): Use when sequence matters. (e.g. Numbered list)

```html
<ol>
  <li>Wake up</li>
  <li>Hit Snooze at least 3 times</li>
  <li>Wake up again</li>
  <li>Shower</li>
  <li>Drive to college</li>
</ol>
```

**[[List Item]]** (`<li>`): The actual content of the list.

### Nesting Lists

```html
<ul>
  <li>Beverages
    <ul>
      <li>Coke</li>
      <li>Rum</li>
    </ul>
  </li>
  <li>Snacks
    <ul>
      <li>Chips</li>
      <li>Chocolate Cake</li>
      <li>Limes</li>
    </ul>
  </li>
</ul>
```

The nested list goes INSIDE the `<li>` element, creating a hierarchical structure.

### Description Lists
[[Description List]] (`<dl>`): FAQs, glossaries, dictionaries, key-value pairs

- `<dt>` - Description Term
- `<dd>` - Description Definition

```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language</dd>
  
  <dt>CSS</dt>
  <dd>Cascading Style Sheets</dd>
</dl>
```

# HyperText

**[[Anchor Tag]]** (`<a>`): Creates clickable links.

```html
<a href="http://www.cnn.com">Link Text</a>
```

- `<a>` - The tag
- `href` - The attribute (where to go)
- Link Text - What the user clicks
## Absolute Paths (External Links)

**[[Absolute Paths]]**: Full URLs used for leaving your site.

```html
<a href="https://breakingbad.fandom.com">Wiki</a>
```

> [!NOTE]
> Must include `https://` or `http://`

## Relative Paths (Internal Links)

**[[Relative Paths]]**: Linking to your own files within your website.

```html
<a href="contact.html">Contact Me</a>
<a href="pages/about.html">About Me</a>
<a href="../index.html">Back Home</a>
```

- `contact.html` - Same folder
- `pages/about.html` - Inside "pages" folder
- `../index.html` - Up one folder level

# The target Attribute

[[target Attribute]]: Controls where the link opens.

**Default behavior:** Opens in the same tab

**Opens in a new tab:**`target="_blank"`

```html
<a href="https://longdogechallenge.com/" target="_blank">Open Site</a>
```

> [!NOTE] Obs
> Only use `_blank` for external sites—users expect internal links to stay in the same tab.

# Jump Links
**[[Jump Links]]** (also called **Anchor Links**): Link to a specific section on the same page.

**Step 1**: Create the target with an `id` attribute

```html
<h2 id="bottom">You have arrived!</h2>
```

**Step 2**: Create the link using `#` plus the id

```html
<a href="#bottom">Jump to Bottom</a>
```

**Complete example**:

```html
<a href="#target-section">Click here to Jump Down</a>

<br><br><br><br><br>
<!-- Lots of space here -->

<h2 id="target-section">You have arrived!</h2>
<p>This is the section you linked to.</p>
```

# The 404 Concept

**[[404 Error]]**: What happens when you link to a file that doesn't exist.

**Why it happens**:

- Typo in the filename
- File was moved or deleted
- Wrong folder path

# Images

**[[img Tag]]**: Displays images on a webpage.

**Characteristics**: It's a [[Void Element]]—no closing tag needed.

**Basic syntax**:

```html
<img src="images/cat1.jpg" alt="A grey cat">
```

**Required attributes**:

- `src` - Source (path to the image file)
- `alt` - Alternative text (description) [[alt Attribute]]
## Image Formats

**[[JPG/JPEG]]**:

- Best for: Photos with high detail
- Supports: Millions of colors
- Does NOT support: Transparency
- File size: Compressed, smaller

**[[PNG]]**:

- Best for: Logos, graphics, screenshots
- Supports: Transparency
- File size: Larger than JPG
- Quality: Lossless compression

**[[GIF]]**:

- Best for: Simple animations
- Supports: Animation, transparency
- Limitation: Only 256 colors
- Use case: Memes, simple icons

**[[SVG]]**:

- Best for: Icons, logos, illustrations
- Supports: Infinite scalability (vector-based)
- File size: Very small
- Advantage: Never pixelates when zoomed

# The Figure Element

**[[figure Element]]**: Professional way to add captions to images (e.g. Photo galleries, diagrams, illustrations with explanations).

**Structure**:

```html
<figure>
  <img src="cat1.jpg" alt="Russian Blue cat">
  <figcaption>My Cute Russian Blue</figcaption>
</figure>
```

**Benefits**:

- Semantically associates image with caption
- Better for accessibility
- Easier to style as a unit

# Modern Media

**[[video Element]]**: Embeds video with built-in player.

```html
<video controls src="harvest.mp4"></video>
```

**[[audio Element]]**: Embeds audio with built-in player.

```html
<audio controls src="podcast.mp3"></audio>
```

**[[controls Attribute]]**: Displays play/pause buttons, volume, progress bar.

# Semantic HTML

**[[Semantics]]**: The study of meaning.

**In HTML**: Writing code that explains **WHAT** it is, not just what it looks like.

**Example**:

- `<div class="navigation">` - Not semantic
- `<nav>` - Semantic (clearly indicates navigation)

## `<header>` vs `<head>`

**`<head>`**: Invisible settings for the browser

- Meta tags
- Title
- Stylesheets
- Scripts

**`<header>`**: Visible top of the page

- Logo
- Site title
- Main navigation
## Semantic HTML Elements
### The `<nav>` Element

**[[nav Element]]**: Contains main navigation links.

**Purpose**: Tells screen readers "Here is the menu."

> [!NOTE] Note
> [[aria-label Attribute]] provides additional context for assistive technologies.
### The `<main>` Element

[[main Element]]: The primary content of the page.

> [!NOTE] Rule
> Should only be **one** `<main>` per page.

### `<section> vs <article>`

**[[article Element]]**: Blog posts, news articles, product cards, user comments.

**[[section Element]]**: Chapters, tabbed content sections, grouped features.

### The `<footer>` Element

**[[footer Element]]**: Bottom section of page or article.

**Typical content**:

- Copyright information
- Contact details
- Social media links
- Sitemap
- Legal links

> [!NOTE] Note
> [[address Element]] is for contact information, not physical addresses necessarily.

### The `<aside>` Element
[[aside Element]]: Content tangentially related to the main content.

**Use cases:**

- Sidebars
- Pull quotes
- Related links
- Advertisements
- Author bio boxes

## Reasons to use HTML Semantics
1. [[SEO]] (Search Engine Optimization):
	- Google ranks semantics sites higher.
	- Search engines understand to main content.
2. **Accessibility:** 
	- Screen readers can navigate more effectively.
	- Users can jump directly to main content.
3. **Maintainability:** Code is easier to read, understand and modify.

## Key Concepts to Review
### HTML Fundamentals

- [[Client]]
- [[Server]]
- [[Visual Studio Code]]
- [[Live Server]]
- [[DOCTYPE]]
- [[Standards Mode]]
- [[HTML Tag]]
- [[HTML Element]]
- [[Container Tags]]
- [[Void Elements]]
- [[Self-Closing Tags]]

### List Elements

- [[Unordered List]]
- [[Ordered List]]
- [[List Item]]
- [[Nested Lists]]
- [[Description List]]

### Linking

- [[Anchor Tag]]
- [[href Attribute]]
- [[Absolute Paths]]
- [[Relative Paths]]
- [[target Attribute]]
- [[UX Rule]]
- [[mailto Links]]
- [[Jump Links]]
- [[Anchor Links]]
- [[404 Error]]

### Images and Media

- [[img Tag]]
- [[alt Attribute]]
- [[Screen Readers]]
- [[SEO]]
- [[JPG/JPEG]]
- [[PNG]]
- [[GIF]]
- [[SVG]]
- [[figure Element]]
- [[video Element]]
- [[audio Element]]
- [[controls Attribute]]
- [[Copyright]]
- [[Unsplash]]
- [[Pexels]]

### Semantic HTML

- [[Semantics]]
- [[nav Element]]
- [[aria-label Attribute]]
- [[main Element]]
- [[article Element]]
- [[section Element]]
- [[footer Element]]
- [[address Element]]
- [[aside Element]]
- [[Accessibility]]
- [[Maintainability]]

### Styling

- [[CSS]]

## Review Questions

1. What is the difference between the `<head>` and `<body>` sections of an HTML document? Give three examples of what goes in each.
    
2. Explain the difference between an HTML tag and an HTML element. Provide an example.
    
3. What are void elements (self-closing tags)? List three examples and explain when you'd use each.
    
4. When should you use an unordered list (`<ul>`) versus an ordered list (`<ol>`)? Give a real-world example for each.
    
5. What is the critical rule about putting content inside `<ul>` or `<ol>` tags? What's the correct way to add items?
    
6. Explain nested lists. Write the HTML for a nested list showing "Fruits" with sub-items "Apples" and "Oranges", and "Vegetables" with sub-items "Carrots" and "Broccoli".
    
7. What is a description list (`<dl>`)? When would you use it instead of `<ul>` or `<ol>`?
    
8. What does the anchor tag `<a>` do? What is the purpose of the `href` attribute?
    
9. Explain the difference between absolute paths and relative paths in links. Give an example of each.
    
10. What does `target="_blank"` do? When should you use it, according to UX best practices?
    
11. Find and fix the two errors in this code:
    
    ```html
    <a src="google.com">Click Here</a>
    ```
    
12. How do you create a link that opens an email client? Write an example.
    
13. Explain how jump links (anchor links) work. What are the two steps needed to create a working jump link?
    
14. What is a 404 error? What causes it when working with links?
    
15. Why is the `alt` attribute required on images? List three reasons.
    
16. Compare the four image formats (JPG, PNG, GIF, SVG). When would you use each one?
    
17. What's the safe way to resize an image using HTML attributes? What's the risky way and why is it problematic?
    
18. What is the `<figure>` element used for? Write an example showing proper usage.
    
19. How do you embed a video with controls in HTML5? Write the code.
    
20. Why shouldn't you just take images from Google Images? What are three legal alternatives?
    
21. What does "semantic HTML" mean? Why is it important?
    
22. Explain the difference between `<head>` and `<header>`. This is a common confusion—clarify it.
    
23. What is the `<nav>` element used for? Write an example navigation menu using semantic HTML.
    
24. What's the rule about how many `<main>` elements a page should have?
    
25. Explain the difference between `<article>` and `<section>`. Use the "Beyoncé test" from the lecture to help.
    
26. What goes in a `<footer>` element? Is it only for the bottom of the page?
    
27. What is the `<aside>` element used for? Give three examples of appropriate `<aside>` content.
    
28. List the three major benefits of using semantic HTML (SEO, Accessibility, Maintainability). Explain each.
    
29. Draw or describe the structure of a modern semantic HTML page layout using `<header>`, `<nav>`, `<main>`, `<article>`, `<aside>`, and `<footer>`.

## Common Mistakes to Avoid

1. **Putting text directly in `<ul>` or `<ol>`** - Always use `<li>`
2. **Using `src` instead of `href` in links** - Links use `href`, images use `src`
3. **Forgetting `alt` attribute on images** - Required for accessibility
4. **Confusing `<head>` and `<header>`** - Completely different purposes
5. **Using multiple `<main>` elements** - Only one per page
6. **Forgetting to close tags** - Except for void elements
7. **Not organizing images in folders** - Use `images/` folder structure
8. **Missing protocol in absolute links** - Include `https://`
9. **Setting both width and height on images** - Can distort aspect ratio
10. **Using `<div>` instead of semantic elements** - Use proper semantic tags

---

## Practical Tags for Obsidian

#HTML #WebDevelopment #SemanticHTML #HTMLElements #Lists #Links #Images #Accessibility #WebDesign #Frontend #HTML5 #WebAccessibility #SEO #HTMLBasics #WebStandards #CodingBestPractices #WebContent #StructuredContent #HTMLSyntax #UserExperience 