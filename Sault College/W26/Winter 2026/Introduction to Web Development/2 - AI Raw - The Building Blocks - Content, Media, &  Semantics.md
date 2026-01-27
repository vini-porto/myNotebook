## Week 1 Recap

### Client vs. Server

**The Restaurant Model**: Remember the client-server relationship:

- **[[Client]]** (You): The browser that makes requests
- **[[Server]]** (The kitchen): Prepares and serves the content
- **Network** (The waiter): Delivers the information

### VS Code and Live Server

**[[Visual Studio Code]]**: Your code editor—the "kitchen" where you prepare your website.

**[[Live Server]]**: Automatically refreshes your browser when you save—eliminates manual refreshing.

### The Boilerplate

**[[DOCTYPE]]**: `<!DOCTYPE html>` triggers [[Standards Mode]] in the browser, ensuring modern rendering behavior.

## The Anatomy Review

### Head vs. Body

**`<head>` section**: For the browser

- Meta information
- Title
- Settings
- Stylesheets
- Not visible to users

**`<body>` section**: For the user

- Text content
- Images
- Buttons
- Everything visible on the page

## Tags vs. Elements

### Understanding the Terminology

**[[HTML Tag]]**: The code bits—`<p>` and `</p>`

**[[HTML Element]]**: The complete package consisting of:

- Opening tag
- Content
- Closing tag

**Example**:

```html
<p>Hello World</p>
```

- Tags: `<p>` and `</p>`
- Element: The entire `<p>Hello World</p>`

## Void Elements (Self-Closing Tags)

### Container Tags vs. Void Elements

**[[Container Tags]]**: Most elements have an opening and closing tag:

```html
<p>...</p>
<div>...</div>
```

**[[Void Elements]]** (also called [[Self-Closing Tags]]): Act alone with no closing tag:

- `<br>` - Line break
- `<hr>` - Horizontal rule
- `<img>` - Image

**Minion Analogy**: Some Minions hold hands (container tags); some work alone (void elements).

## Lists: Organizing Data

### Why Lists Matter

**The web is mostly lists**: Almost everything you see online is a list in disguise:

- Search results
- Navigation bars
- Instagram feeds
- Todo lists
- Shopping carts

## The Unordered List

**[[Unordered List]]** (`<ul>`): Use when order doesn't matter.

**Appearance**: Standard bullet points

**Example**:

```html
<ul>
  <li>Bananas</li>
  <li>Goggles</li>
  <li>Oxygen</li>
  <li>A Despicable Master</li>
</ul>
```

**Use cases**: Shopping lists, feature lists, navigation menus

## The Ordered List

**[[Ordered List]]** (`<ol>`): Use when sequence matters.

**Appearance**: Numbered list (1, 2, 3...)

**Example**:

```html
<ol>
  <li>Wake up</li>
  <li>Hit Snooze at least 3 times</li>
  <li>Wake up again</li>
  <li>Shower</li>
  <li>Drive to college</li>
</ol>
```

**Use cases**: Instructions, rankings, step-by-step guides, recipes

## The List Item Tag

**[[List Item]]** (`<li>`): The actual content of the list.

**Important relationship**:

- `<ul>` and `<ol>` are the wrappers (the bread)
- `<li>` is the actual item (the meat)

**Critical Rule**: You can NEVER put text directly inside a `<ul>` or `<ol>`. Text MUST go inside an `<li>`.

**Wrong**:

```html
<ul>
  Bananas
  Goggles
</ul>
```

**Correct**:

```html
<ul>
  <li>Bananas</li>
  <li>Goggles</li>
</ul>
```

## Nesting Lists

**[[Nested Lists]]**: Putting a list inside a list item—"Inception" style.

**Example**:

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

**Key point**: The nested list goes INSIDE the `<li>` element, creating a hierarchical structure.

**Use cases**: Multi-level navigation, category trees, organizational charts

## Description Lists

**[[Description List]]** (`<dl>`): The "forgotten list type."

**Components**:

- `<dt>` - Description Term
- `<dd>` - Description Definition

**Example**:

```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language</dd>
  
  <dt>CSS</dt>
  <dd>Cascading Style Sheets</dd>
</dl>
```

**Use cases**: FAQs, glossaries, dictionaries, key-value pairs

## Styling Teaser

**Common questions**:

- "Can we change the bullets to squares?"
- "Can we change the bullets to pictures of cats?"
- "Can we build animated scenes?"

**Answer**: Yes! But that's [[CSS]]. HTML is for **structure only**—CSS handles visual presentation.

## HyperText: Connecting the Web

### Why Links Matter

**Without links, the web is just a pile of Word documents.** Links are what make the web "web-like"—they connect everything together.

### The Anchor Tag

**[[Anchor Tag]]** (`<a>`): Creates clickable links.

**Basic syntax**:

```html
<a href="http://www.cnn.com">Link Text</a>
```

**Components**:

- `<a>` - The tag
- `href` - The attribute (where to go)
- Link Text - What the user clicks

## The href Attribute

**[[href Attribute]]**: Stands for "Hypertext REFerence"—tells the browser where to navigate.

**Syntax**:

```html
<a href="https://theuselessweb.com/">Click Here</a>
```

**Minion Analogy**: The Minion Portal Gun—you need to dial in coordinates before you jump.

## Absolute Paths (External Links)

**[[Absolute Paths]]**: Full URLs used for leaving your site.

**Rule**: Must include `https://` or `http://`

**Example**:

```html
<a href="https://breakingbad.fandom.com">Wiki</a>
```

**Use case**: Linking to external websites, social media, resources on other domains

## Relative Paths (Internal Links)

**[[Relative Paths]]**: Linking to your own files within your website.

**Examples**:

```html
<a href="contact.html">Contact Me</a>
<a href="pages/about.html">About Me</a>
<a href="../index.html">Back Home</a>
```

**How they work**:

- `contact.html` - Same folder
- `pages/about.html` - Inside "pages" folder
- `../index.html` - Up one folder level

## The target Attribute

**[[target Attribute]]**: Controls where the link opens.

**Default behavior**: Opens in the same tab

**`target="_blank"`**: Opens in a new tab

**Example**:

```html
<a href="https://longdogechallenge.com/" target="_blank">Open Site</a>
```

**[[UX Rule]]**: Only use `_blank` for external sites—users expect internal links to stay in the same tab.

## Anchor Tag Common Errors

**Quiz**: Find the 2 errors:

```html
<a src="google.com">Go</a>
```

**Errors**:

1. It's `href`, not `src` (src is for images)
2. Missing `https://` protocol

**Correct version**:

```html
<a href="https://google.com">Go</a>
```

## Email Links

**[[mailto Links]]**: Opens the user's default mail application.

**Syntax**:

```html
<a href="mailto:sam.laitinen@saultcollege.ca">Email Me Anytime</a>
```

**What happens**: When clicked, opens email client with the recipient pre-filled.

**Use case**: Contact pages, support links, "Report a problem" buttons

## Jump Links (Anchor Links to IDs)

**[[Jump Links]]** (also called [[Anchor Links]]): Link to a specific section on the same page.

**Process**:

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

**Use cases**: Table of contents, "Back to top" links, single-page websites

## The 404 Concept

**[[404 Error]]**: What happens when you link to a file that doesn't exist.

**Browser displays**: "404 Not Found"

**Why it happens**:

- Typo in the filename
- File was moved or deleted
- Wrong folder path

**Prevention**: Always test your links!

## Images: Adding Visuals

### The Image Tag

**[[img Tag]]**: Displays images on a webpage.

**Characteristics**: It's a [[Void Element]]—no closing tag needed.

**Basic syntax**:

```html
<img src="images/cat1.jpg" alt="A grey cat">
```

**Required attributes**:

- `src` - Source (path to the image file)
- `alt` - Alternative text (description)

## Accessibility and Alt Text

**[[alt Attribute]]**: Critical for accessibility and SEO.

**Why use alt text?**

1. **[[Screen Readers]]** read it aloud for users with vision impairments
2. **Fallback**: Shows if the image fails to load
3. **[[SEO]]**: Google uses it to understand image content for search rankings

**Good alt text**:

```html
<img src="cat.jpg" alt="Grey Russian Blue cat sitting on a windowsill">
```

**Bad alt text**:

```html
<img src="cat.jpg" alt="image123">
```

## Image Formats

### Choosing the Right Format

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

## Image File Organization

**Best practice**: Always keep images in an organized folder structure.

**Standard approach**:

```
project/
├── index.html
├── images/
│   ├── cat1.jpg
│   ├── cat2.jpg
│   └── logo.png
```

**Correct path**:

```html
<img src="images/cat2.jpg" alt="Cute cat">
```

## Sizing Images

### Width and Height Attributes

**Safe approach**: Set only width—browser calculates height proportionally.

```html
<img src="cat1.jpg" width="500" alt="Cat">
```

**Risky approach**: Setting both can squash or stretch the image.

```html
<img src="cat1.jpg" width="500" height="500" alt="Cat">
<!-- Don't do this unless you're sure of the aspect ratio! -->
```

**Best practice**: Use CSS for responsive image sizing, not HTML attributes.

## The Figure Element

**[[figure Element]]**: Professional way to add captions to images.

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

**Use cases**: Photo galleries, diagrams, illustrations with explanations

## Modern Media: Video and Audio

**[[video Element]]**: Embeds video with built-in player.

```html
<video controls src="harvest.mp4"></video>
```

**[[audio Element]]**: Embeds audio with built-in player.

```html
<audio controls src="podcast.mp3"></audio>
```

**[[controls Attribute]]**: Displays play/pause buttons, volume, progress bar.

## Copyright and Image Sources

### Pro Tip: Don't Steal Images

**Problem**: Just taking images from Google Images violates [[Copyright]].

**Legal alternatives**:

- **[[Unsplash]]**: Free high-quality photos
- **[[Pexels]]**: Royalty-free images and videos
- **Create your own**: Photography, illustrations, AI-generated images

**Why it matters**: Copyright infringement can lead to legal trouble and fines.

## Semantic HTML: Writing Meaningful Code

### The 'Div Soup' Problem

**Old approach**: Using `<div>` for everything.

```html
<div id="header">...</div>
<div id="main">...</div>
<div id="footer">...</div>
```

**Problem**: It meant nothing—just generic boxes with no inherent meaning.

## What is Semantics?

**[[Semantics]]**: The study of meaning.

**In HTML**: Writing code that explains **WHAT** it is, not just what it looks like.

**Definition**: Semantics is the branch of linguistics and logic concerned with the relationship between signs (words, phrases, symbols) and what they represent in the real world.

**Example**:

- `<div class="navigation">` - Not semantic
- `<nav>` - Semantic (clearly indicates navigation)

## The Newspaper Analogy

You know what a **headline** looks like. You know what a **footer** looks like.

**HTML tags should match that conceptual structure**—not just visual appearance.

## Important Distinction: `<header>` vs `<head>`

**`<head>`**: Invisible settings for the browser

- Meta tags
- Title
- Stylesheets
- Scripts

**`<header>`**: Visible top of the page

- Logo
- Site title
- Main navigation

**Don't mix them up!**

**Example**:

```html
<html>
<head>
  <title>My Page Title</title>
  <meta charset="UTF-8">
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <h1>Welcome to My Site</h1>
    <nav>
      <a href="/">Home</a>
    </nav>
  </header>
```

## Semantic HTML Elements

### The `<nav>` Element

**[[nav Element]]**: Contains main navigation links.

**Purpose**: Tells screen readers "Here is the menu."

**Example**:

```html
<header>
  <h1>My Awesome Website</h1>
  <nav aria-label="Main Navigation">
    <ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#about">About</a></li>
      <li><a href="#services">Services</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
</header>
```

**Note**: [[aria-label Attribute]] provides additional context for assistive technologies.

### The `<main>` Element

**[[main Element]]**: The primary content of the page.

**Rule**: Should only be **one** `<main>` per page.

**Example**:

```html
<main>
  <section id="home">
    <h2>Welcome to My Awesome Website</h2>
    <p>This is the home section with latest updates and news.</p>
  </section>
</main>
```

**Purpose**: Helps screen readers skip to main content, bypassing navigation and headers.

### <`section> vs <article>`

**[[article Element]]**: Standalone, self-contained content.

**Test**: If you copied and pasted it to another website, would it still make sense?

**Examples**: Blog posts, news articles, product cards, user comments

**[[section Element]]**: A thematic grouping of content.

**Test**: It's part of a larger whole—like a chapter in a book.

**Examples**: Chapters, tabbed content sections, grouped features

**Complete example**:

```html
<main>
  <article>
    <h2>The Life of a Sentient Toaster</h2>
    <p>This article is a complete story. If you copied it to another 
    website, it would still make sense. It's the 'Beyoncé' of tags—
    it doesn't need the rest of the page to be famous.</p>
    
    <section>
      <h3>Chapter 1: The Bread Betrayal</h3>
      <p>This section discusses why the toaster felt used. It's a 
      specific theme, but it belongs to the article above.</p>
    </section>
  </article>
  
  <section id="newsletter-signup">
    <h2>Join our Toaster Cult</h2>
    <p>This isn't an 'article' because nobody wants to read this 
    independently. It's just a thematic group of contact forms.</p>
  </section>
</main>
```

### The `<footer>` Element

**[[footer Element]]**: Bottom section of page or article.

**Typical content**:

- Copyright information
- Contact details
- Social media links
- Sitemap
- Legal links

**Example**:

```html
<footer>
  <section>
    <h3>The End of the Road</h3>
    <p>You've reached the bottom of the page.</p>
  </section>
  
  <address>
    Built with ❤️ and Regret by 
    <a href="mailto:void@internet.com">The Developer</a><br>
    123 Digital Abyss Lane, Sector 7G
  </address>
</footer>
```

**Note**: [[address Element]] is for contact information, not physical addresses necessarily.

### The `<aside>` Element

**[[aside Element]]**: Content tangentially related to the main content.

**Use cases**:

- Sidebars
- Pull quotes
- Related links
- Advertisements
- Author bio boxes

**Example**:

```html
<main>
  <article>
    <h2>How to Befriend a Squirrel</h2>
    <p>To successfully earn the trust of a local squirrel, one must 
    move slowly and possess an alarming amount of high-quality walnuts.</p>
    
    <aside>
      <h4>Squirrel Fact #402</h4>
      <p>Squirrels can't actually see the color red. So if you are 
      wearing a bright red jumpsuit to blend in, you are failing for 
      no reason. Also, they are definitely judging your haircut.</p>
    </aside>
    
    <p>Once the squirrel has approached, offer the nut flat on your 
    palm. Do not flinch, or the alliance is broken forever.</p>
  </article>
  
  <aside>
    <h3>Related Gossip</h3>
    <ul>
      <li><a href="#">Top 10 Acorns of 2025</a></li>
      <li><a href="#">Are Pigeons just Squirrels with wings?</a></li>
      <li><a href="#">Why my cat is jealous of the backyard</a></li>
    </ul>
  </aside>
</main>
```

## Why Use Semantic HTML?

### Three Major Benefits

**1. [[SEO]]** (Search Engine Optimization):

- Google ranks semantic sites higher
- Search engines understand content structure better
- Improves discoverability

**2. [[Accessibility]]**:

- Screen readers can navigate more effectively
- Users can jump directly to main content
- Keyboard navigation works better

**3. [[Maintainability]]**:

- Code is easier to read and understand
- Other developers know what each section does
- Easier to update and modify

## The Modern Semantic Layout

**Standard structure**:

```html
<body>
  <header>
    <!-- Logo, site title, main navigation -->
  </header>
  
  <main>
    <article>
      <!-- Main content -->
    </article>
  </main>
  
  <footer>
    <!-- Copyright, contact, links -->
  </footer>
</body>
```

## Semantic HTML Quiz

**Question 1**: I want to put a copyright notice at the bottom. Which tag?

**Answer**: `<footer>`

**Question 2**: I want to write a blog post about Walter White. Which tag?

**Answer**: `<article>`

## Interactive Code Fix: Spot the Errors

### Error 1

```html
<ul> <p>Milk</p> </ul>
```

**Problem**: `<p>` inside `<ul>`—list items must use `<li>`, not paragraphs.

**Fix**:

```html
<ul> <li>Milk</li> </ul>
```

### Error 2

```html
<a src="...">Link</a>
```

**Problem**: Links use `href`, not `src`.

**Fix**:

```html
<a href="...">Link</a>
```

### Error 3

```html
<img src="cat.jpg">
```

**Problem**: Missing `alt` attribute (required for accessibility).

**Fix**:

```html
<img src="cat.jpg" alt="Cute cat sitting">
```

## Summary

**Lists organize data**: `<ul>`, `<ol>`, `<li>`

**Links connect the web**: `<a>` with `href`

**Images visualize content**: `<img>` with `src` and `alt`

**Semantics give structure**: `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`

---

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

---

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
    
30. Fix these three code errors:
    
    ```html
    <ul> <p>Item 1</p> </ul>
    <a src="page.html">Link</a>
    <img src="photo.jpg">
    ```
    

---

## Practical Exercises

### Exercise 1: Build a Recipe Page

Create an HTML page for your favorite recipe that includes:

- An ordered list for instructions
- An unordered list for ingredients
- A nested list showing ingredient categories (Wet Ingredients, Dry Ingredients)
- Proper semantic structure (header, main, footer)

### Exercise 2: Create a Navigation Menu

Build a semantic navigation menu with:

- A `<nav>` element
- An unordered list of links
- Links to: Home, About, Services, Contact
- At least one external link (with proper attributes)
- Proper accessibility attributes

### Exercise 3: Photo Gallery

Create a photo gallery page featuring:

- At least 4 images with proper `alt` text
- Each image wrapped in a `<figure>` with `<figcaption>`
- Organized in a semantic structure
- Attribution/credits in the footer

### Exercise 4: Fix the Broken Code

Fix all errors in this code:

```html
<!DOCTYPE html>
<html>
<header>
  <title>My Site</title>
</header>
<body>
  <head>
    <h1>Welcome</h1>
  </head>
  <ul>
    Products
    <li>Apples</li>
  </ul>
  <a src="contact.html">Contact
  <img src="logo.png">
</body>
</html>
```

### Exercise 5: Semantic Blog Post

Create a blog post about a topic of your choice that includes:

- Proper `<article>` structure
- Multiple `<section>` elements for different parts
- An `<aside>` with related information
- Jump links to different sections
- At least one image with caption
- Email contact link in the footer

---

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