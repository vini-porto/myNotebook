# The Internet vs. The Web

>[!NOTE] The Internet 
>The physical hardware infrastructure: cables, routers, servers, and satellites. It's the global network that connects computers.

>[!NOTE] The Web (World Wide Web/WWW) 
>The software layer—documents and pages connected by hyperlinks that run on top of the Internet.

The Internet is the train tracks; the Web is the trains running on them.

# The Client-Server Model

**[[Client]]** (You): The browser that makes requests. It asks for information.

**[[Server]]** (Amazon/Google/etc.): The computer that stores and serves information. It answers requests.

>[!NOTE] Restaurant Analogy
>
>- You ([[Client]]) order food
>- Kitchen ([[Server]]) prepares it
>- Waiter ([[Network]]) brings it to you

# The Request-Response Cycle

The [[Request-Response Cycle]] is the fundamental pattern of web communication:

1. **Request**: The browser asks for a resource (e.g., "Get me index.html")
2. **Processing**: The server locates the requested file
3. **Response**: The server sends a status code (e.g., [[HTTP Status Code 200]] OK) plus the file
4. **Rendering**: The browser draws/displays the content

# HTTP vs. HTTPS

**[[HTTP]]** (Hypertext Transfer Protocol): The language of the web—the protocol that defines how messages are formatted and transmitted.

**[[HTTPS]]** (HTTP Secure): The encrypted, secure version of HTTP.

## Why HTTPS Matters

- Protects sensitive data like passwords and credit card information
- Required for modern websites
- Chrome and other browsers warn users if a site is not secure
- Essential for user trust and [[SEO]] (Search Engine Optimization)

# IP Addresses

Every device on the Internet needs a **[[Public IP Address]]** to communicate.

**Format**: [[IPV4]] addresses look like `192.168.1.5` (four numbers separated by dots)

- Websites have IP addresses too (e.g., Google = `142.250.190.46`)
- **Special IP**: `127.0.0.1` = **[[Localhost]]** (refers to your own computer)

## DNS (Domain Name System)

**[[DNS]]** (Domain Name System) is like the phone book of the Internet.

**Problem**: Humans are bad at memorizing numbers like `142.250.190.46`.

**Solution**: DNS maps human-readable domain names to IP addresses.

**Example**: `www.saultcollege.ca` → DNS lookup → `20.116.xxx.xxx`

If DNS breaks, you can't find websites by name—you'd have to know their IP addresses.

# Frontend vs. Backend

## Frontend (Client-Side)

**[[Frontend Development]]** is what users see and interact with directly:

- What you see and click
- Runs in the browser
- Technologies: [[HTML]], [[CSS]], [[JavaScript]]

## Backend (Server-Side)

**[[Backend Development]]** is what happens behind the scenes:

- Where data is stored ([[Databases]])
- Business logic and data processing
- Technologies: [[Python]], [[PHP]], [[Java]], [[SQL]], [[Node.js]]

# Languages of the Web

**[[HTML]]** (HyperText Markup Language) defines the structure and content of web pages. It's the skeleton.

**[[CSS]]** (Cascading Style Sheets) controls the visual appearance and layout. It's the styling.

**[[JavaScript]]** adds interactivity and dynamic behavior. It's the functionality.
****
## The Browser Engine

Browsers like [[Chrome]], [[Firefox]], and [[Safari]] are **[[Rendering Engines]]**. They:

- Read code line-by-line
- "Paint" pixels on the screen
- Interpret HTML, CSS, and JavaScript

>[!NOTE] Important note 
>Different browsers sometimes render things slightly differently. Web developers primarily test in Chrome/Edge (both [[Chromium]]-based browsers).

# Developer Tools

**View Page Source** (Right-click > "View Page Source"):

- Shows the raw HTML file as it was sent from the server
- Static snapshot of the original code

**Inspect** (Right-click > "Inspect"):

- Shows the live [[DOM]] (Document Object Model) in browser memory
- Reflects current state including JavaScript changes
- **As developers, we use INSPECT**

## The Developer's Toolset

Every web developer needs three essential tools:

1. **Editor** (To write code) - [Visual Studio Code](https://code.visualstudio.com/docs/setup/setup-overview)
2. **Terminal** (To give commands) - [[Command Line Interface]]
3. **Browser** (To see results) - [[Chrome]], [[Firefox]], etc.

# Text Editors vs. IDEs

**Simple Text Editors** (Notepad, Word):

- No syntax highlighting
- Add hidden formatting that breaks code
- Not suitable for development

**[[IDE]]** (Integrated Development Environment):

- **Syntax Highlighting**: Colors code for readability
- **Autocomplete** ([[IntelliSense]]): Suggests code as you type
- **Error Checking**: Identifies problems before you run the code

## Visual Studio Code (VS Code)

**[[Visual Studio Code]]** is the industry standard editor, used by 70%+ of professional developers.

**Features**:

- Free and [[Open Source]] (created by Microsoft)
- Runs on Windows, Mac, and Linux
- Lightweight and fast
- Extensive extension ecosystem

>[!NOTE] Important 
>[[Visual Studio Code|VS Code]] is NOT the same as [[Visual Studio]] which is a full IDE for .NET development.

---
### Essential VS Code Extensions

VS Code is lightweight out of the box. You install **[[Extensions]]** to add features. Click the "Squares" icon on the left sidebar to browse extensions.

#### Live Server

Automatically refreshes the browser when you save your code

Saves enormous amounts of time during development, you don't have to manually refresh the browser after every change.

#### Prettier

**Function**: Code formatter

Automatically fixes messy indentation and formatting

#### Material Icon Theme

**Function**: Changes file icons in the explorer

Helps you visually distinguish `.html`, `.css`, `.js` files quickly, making navigation easier

# Understanding Live Server

When Live Server runs, you'll see an address like `127.0.0.1:5500`:

**127.0.0.1**: The [[IP Address]] of "Your Computer" (Localhost)

**:5500**: The **[[Port]]** number (like an apartment or door number on the building)

If port 5500 is busy, Live Server tries 5501, 5502, etc.

**Note**: This port number may vary depending on what's available.

# File Management

>[!NOTE] Important principle 
Web development is 50% code, 25% organizing files, and 25% design.

>**Broken links are usually broken paths.**

### The Root Folder

The **[[Root Folder]]** is the top-level folder of your project.

**Best practice**: Open THIS folder in VS Code—not your entire Desktop or C: Drive. This ensures correct [[Relative Paths]].

### Rule 1: Lowercase Only

**Problem**: Windows is case-insensitive (`Logo.png` = `logo.png`), but Linux servers (where most websites are hosted) are **CASE SENSITIVE**.

**Result**: If you code `Logo.png` but the file is actually `logo.png`, it works on your computer but breaks when deployed online.

**Solution**: ALWAYS use lowercase for all file and folder names.

### Rule 2: No Spaces in File Names

**Problem**: Browsers convert spaces to `%20` in [[URLs]].

**Example**: `My Resume.html` becomes `My%20Resume.html` in the browser address bar.

**Solution**: Use hyphens (`my-resume.html`) or underscores (`my_resume.html`) instead of spaces.

### The "Hidden Extension" Trap

**Warning**: Windows hides file extensions by default.

**Problem**: You might think you saved `index.html`, but you actually saved `index.html.txt`.

**Solution**: Enable "File Name Extensions" in Windows Explorer View settings. This is essential for web development.

### File Naming Quiz

Let's check if these file names are good or bad:

- `home page.html` → **BAD** (contains space)
- `HomePage.html` → **BAD** (contains capitals)
- `home-page.html` → **GOOD**
- `img/Dog.jpg` → **BAD** (capital D)
- `css/style.css` → **GOOD**

## Standard Project Structure

A typical web project follows this structure:

```
project-name/
├── index.html
├── css/           (or /styles)
├── js/            (or /scripts)
└── images/        (or /img)
```

**Note**: `index.html` is the default file that web servers look for when someone visits your website's root URL.

## Understanding File Paths

### Absolute Paths

**[[Absolute Paths]]** contain the full URL and connect to external sites:

**Example**: `https://www.google.com`

**Characteristics**:

- Always includes the protocol (`http://` or `https://`)
- Used for linking to external resources
- Works from anywhere

### Relative Paths

**[[Relative Paths]]** connect to local files within your project:

**Concept**: Directions from WHERE YOU ARE to WHERE YOU WANT TO GO.

**Syntax**:

- `./` = Current folder (often optional)
- `images/logo.png` = Go into the `images` folder, get `logo.png`

### The "Up" Command

**`../`** = Go up one folder level

**Use case**: If you're in `css/style.css` and need an image from the `images/` folder (which is at the same level as `css/`), you use:

```css
background-image: url('../images/bg.jpg');
```

### Path Quiz Example

**Scenario**: I am in `index.html` at the root level. I want a picture inside the `images` folder.

**Correct**: `src="images/pic.jpg"`

**Wrong**: `src="../images/pic.jpg"` (This goes up and out of the project—there's no parent folder to go up to)

## Introduction to HTML

**[[HTML]]** stands for HyperText Markup Language.

**Markup**: Annotating text to give it meaning and structure.

**Examples**:

- This is a heading
- This is a paragraph
- This is a link

## Anatomy of an HTML Element

```html
<p>Hello World</p>
```

**Parts**:

- **`<p>`**: [[Opening Tag]]
- **`Hello World`**: Content
- **`</p>`**: [[Closing Tag]] (has the forward slash `/`)

## The HTML Boilerplate

The **[[HTML Boilerplate]]** is the standard skeleton structure that every HTML document needs.

**Shortcut in VS Code**: Type `!` and hit Enter to generate it automatically.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

### Understanding the Doctype

```html
<!DOCTYPE html>
```

**What it is**: A declaration, NOT a tag. It tells the browser which version of HTML the page uses.

**What it does**:

- **Triggers Standards Mode**: Ensures the browser renders in modern "Standards Mode" rather than "[[Quirks Mode]]" (which emulates bugs from ancient browsers like Internet Explorer 5)
- **Identifies HTML5**: The specific syntax `<!DOCTYPE html>` indicates a modern [[HTML5]] document

### Head vs. Body

**`<head>`**: Contains meta-information for the browser and search engines

- Not displayed to users
- Includes title, character encoding, stylesheets, metadata

**`<body>`**: Contains content for the human user

- Everything visible on the page
- Text, images, links, etc.

### The `<title>` Tag

```html
<title>My Website</title>
```

**Location**: Lives in the `<head>` section

**Purpose**:

- Determines text shown in the browser tab
- Crucial for [[SEO]] (Search Engine Optimization)
- Used when people bookmark your site
- Appears in search engine results

### Understanding Meta Tags

**Charset Meta Tag**:

```html
<meta charset="UTF-8">
```

- Allows use of emojis and foreign characters
- Ensures proper text encoding

**Viewport Meta Tag**:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

- Tells mobile phones NOT to shrink the page
- Makes the site readable on small screens
- Essential for [[Responsive Design]]

## Your First HTML Code

Here's a simple example to get started:

```html
<body>
    <h1>My First Heading</h1>
    <p>This is my first paragraph.</p>
</body>
```

**`<h1>`**: The largest heading tag (Heading Level 1)

**`<p>`**: Paragraph tag for regular text

## Coming Up Next Week

HTML Deep Dive topics will include:

- **Lists**: [[Unordered Lists]] (`<ul>`), [[Ordered Lists]] (`<ol>`)
- **Images**: `<img>` tag
- **Links**: [[Anchor Tag]] (`<a>`)
- **[[Semantic HTML Tags]]**: Meaningful tags that describe content

---

## Key Concepts to Review

### Web Fundamentals

- [[HTML]]
- [[CSS]]
- [[JavaScript]]
- [[DOM]]
- [[Accessibility Standards]]
- [[Client]]
- [[Server]]
- [[Request-Response Cycle]]
- [[HTTP]]
- [[HTTPS]]
- [[HTTP Status Code 200]]
- [[SEO]]

### Networking Concepts

- [[Public IP Address]]
- [[IPV4]]
- [[Localhost]]
- [[DNS]]
- [[URLs]]
- [[Port]]

### Development Concepts

- [[Frontend Development]]
- [[Backend Development]]
- [[Databases]]
- [[Rendering Engines]]
- [[Chromium]]
- [[IDE]]
- [[IntelliSense]]
- [[Extensions]]
- [[Open Source]]
- [[Command Line Interface]]
- [[Terminal]]

### File Management

- [[Root Folder]]
- [[Relative Paths]]
- [[Absolute Paths]]

### HTML Concepts

- [[Opening Tag]]
- [[Closing Tag]]
- [[HTML Boilerplate]]
- [[Quirks Mode]]
- [[HTML5]]
- [[Semantic HTML Tags]]
- [[Unordered Lists]]
- [[Ordered Lists]]
- [[Anchor Tag]]
- [[Responsive Design]]

### Tools and Technologies

- [[Visual Studio Code]]
- [[GitHub]]
- [[Chrome]]
- [[Firefox]]
- [[Safari]]
- [[Live Server]]
- [[Git]]
- [[Node.js]]
- [[Python]]
- [[PHP]]
- [[Java]]
- [[SQL]]

---

## Review Questions

1. Explain the difference between the Internet and the Web. Provide an analogy to illustrate your answer.
    
2. Describe the four steps of the Request-Response Cycle. What role does the browser play versus the server?
    
3. What is the difference between HTTP and HTTPS? Why is HTTPS important for modern websites?
    
4. What is DNS and why is it necessary? What would happen if DNS stopped working?
    
5. Compare and contrast Frontend Development and Backend Development. What technologies are used in each?
    
6. Explain the roles of HTML, CSS, and JavaScript in web development using the "house" analogy from the lecture.
    
7. What is the difference between "View Page Source" and "Inspect" in browser developer tools? Which one should developers primarily use and why?
    
8. Why is Visual Studio Code preferred over simple text editors like Notepad for web development? List at least three features that make it better.
    
9. Explain what the Live Server extension does and why it's important. Why can't we just double-click HTML files to test them?
    
10. What does `127.0.0.1:5500` mean when you run Live Server? Break down each part of this address.
    
11. Why should you always use lowercase letters and no spaces in file names for web development? What problems can arise if you don't follow these rules?
    
12. What is the "hidden extension trap" in Windows? How can you avoid this problem?
    
13. Given this file structure, write the correct relative path to link to `logo.png` from `style.css`:
    
    ```
    project/
    ├── index.html
    ├── css/
    │   └── style.css
    └── images/
        └── logo.png
    ```
    
14. What is the HTML Boilerplate? What keyboard shortcut generates it in VS Code?
    
15. Explain the purpose of the `<!DOCTYPE html>` declaration. What is "Quirks Mode" and why do we want to avoid it?
    
16. What goes in the `<head>` section versus the `<body>` section of an HTML document? Give examples of each.
    
17. Why is the `<title>` tag important? Where does the title appear when someone visits your website?
    
18. What is the purpose of the viewport meta tag? Why is it essential for mobile devices?
    
19. Create a basic HTML structure with proper boilerplate that includes a heading saying "Welcome to My Site" and a paragraph with any text of your choice.
    
20. You're working on a website and your image links work on your Windows computer but break when you upload to a Linux server. What is the most likely cause and how would you fix it?