# The 'Void' Check

**Remember**: [[Void Elements]] like `<img>` and `<br>` are self-closing.

# Tables
## When to Use Tables

**[[Data Tables]]**: Appropriate for displaying tabular data like:

- Schedules
- Statistical information
- Comparison charts
- Financial data

## The Table Anatomy

**[[Table Element]]** (`<table>`): The wrapper that contains the entire table.

**[[Table Row]]** (`<tr>`): Defines a row of cells.

**[[Table Data]]** (`<td>`): A cell containing data.

**[[Table Header]]** (`<th>`): A header cell (bold title, typically in first row or column).

```html
<table>
  <tr>
    <th>Header</th>
  </tr>
  <tr>
    <td>Data</td>
  </tr>
</table>
```

## The Caption Element

**[[Caption Element]]**: Every table needs a title.

**Usage**: Use `<caption>` immediately after the opening `<table>` tag.

**Example**:

```html
<table>
  <caption>Minion Employee List</caption>
  <tr>...</tr>
</table>
```

`<caption>` provides context for the table, especially important for accessibility.

## Understanding the Row (`<tr>`)

[[Table Row]]: Think of it like a typewriter.

**Process**:

1. Start row: `<tr>`
2. Type cells: `<td>` (or `<th>`)
3. Hit return: `</tr>`

**Common error**: If you miss a `<td>`, your table will have a **hole** (missing cell)!

>[!NOTE] Important 
>Each row should have the same number of cells (unless using colspan/rowspan).

## Borders

>[!NOTE] Default 
>Tables are invisible (no borders).

**Temporary Cheat**: Use the `border` attribute for development.

```html
<table border="1">
```

>[!NOTE] Modern approach: 
>Borders should be styled with CSS, not HTML attributes.

## Merging Cells

### Colspan

**[[Colspan]]**: Stretch cells horizontally (across columns).

**Attribute**: `colspan="2"` makes a cell span 2 columns.

### Rowspan

**[[Rowspan]]**: Stretch cells vertically (down rows).

**Attribute**: `rowspan="3"` makes a cell span 3 rows.

**Example**:

```html
<table border="4">
  <tr>
    <td colspan="2">I take up 2 spots!</td>
    <td rowspan="3">I am tall!</td>
  </tr>
  <tr>
    <td>Cell 1</td>
    <td>Cell 2</td>
  </tr>
  <tr>
    <td>Cell 3</td>
    <td>Cell 4</td>
  </tr>
</table>
```

## Semantic Tables

**[[Semantic Table Structure]]**: Organize tables into meaningful sections.

- **[[thead]]**: The header rows (column labels).

- **[[tbody]]**: The body data (main content).

- **[[tfoot]]**: The totals/summary row.

**Example**:

```html
<table>
  <thead>
    <tr><th>Item</th></tr>
  </thead>
  <tbody>
    <tr><td>Banana</td></tr>
  </tbody>
</table>
```

>**Benefits**: Better structure, easier to style, improved accessibility.s

# Forms 

The `<form>` Wrapper

**[[Form Element]]**: The container for all form controls.

**Required attributes**:

- **[[action Attribute]]**: Where to send the data (URL endpoint).

- **[[method Attribute]]**: How to send the data (GET or POST).

```html
<form action="https://httpbin.org/post" method="POST">
  <!-- form controls here -->
</form>
```

## GET vs. POST

### GET Method

**[[GET Method]]**: URL Data (typically for searches).

**Visibility**: Data visible in address bar: `?q=minions`

**Syntax**: `<form method="GET">`

>[!NOTE] Use cases 
Search forms, filters, **non-sensitive data.**

>**Limitation**: Data length limited by URL length. Security is compromised

### POST Method

**[[POST Method]]**: Hidden Data (for passwords, sensitive information).

**Visibility**: Data hidden inside the [[Request Body]].

**Syntax**: `<form method="POST">`

>[!NOTE] Use cases 
Login forms, registration, any sensitive data.

>**Security**: More secure than GET (though still needs HTTPS for true security).

## Fieldset

**[[Fieldset Element]]**: Groups related inputs with a visible box.

**[[Legend Element]]**: Provides a caption for the fieldset.

**Example**:

```html
<fieldset>
  <legend>Personal Info</legend>
  <input type="text">
</fieldset>
```

**Purpose**: Improves form organization and accessibility.

## The `<input>` Tag

**[[Input Element]]**: The "Transformer" of HTML changes shape based on `type` attribute.

**Key characteristic**: Self-closing (void element).

**Basic syntax**: `<input type="text">`

**Power**: One element, many forms through the [[type attribute]].

### Input Types 

#### Basic Text

**[[Text Input]]**: Standard single-line text field.

```html
<input type="text">
```

#### Secrets (Password)

**[[Password Input]]**: Masks typed characters.

```html
<input type="password">
```

#### Email Validation

**[[Email Input]]**: Validates @ symbol and email format.

```html
<input type="email">
```

**Browser validation**: Automatically checks for valid email format on submission.

#### Calendar

**[[Date Input]]**: Provides a date picker.

```html
<input type="date">
```

#### Color Picker

**[[Color Input]]**: Opens a color selection tool.

```html
<input type="color">
```

#### Slider

**[[Range Input]]**: Creates a slider control.

```html
<input type="range">
```

**Modern browsers**: All provide native UI controls for these input types.

## The Label 

**[[Label Element]]**: Connects text to the input using `for` and `id` attributes.

**Syntax**:

```html
<label for="user">Username:</label>
<input type="text" id="user">
```

>[!NOTE] Accessibility 
>Screen readers announce the label when the input receives focus.

**[[for Attribute]]**: Must match the input's `id` attribute exactly.

## Buttons

**[[Button Element]]**: Creates clickable buttons.

>[!NOTE] Default behavior
>Inside a form, automatically submits the form.

```html
<button>Submit Order</button>
```

**Non-submitting button**: Use `type="button"` to prevent submission.

```html
<button type="button">I do nothing</button>
```

**Types**: 
- `submit` (default)
- `button`
- `reset`

## Textarea

**[[Textarea Element]]**: For long, multi-line text (essays, comments, messages).

**Syntax**:

```html
<textarea rows="5">Type your story...</textarea>
```

**[[rows Attribute]]**: Controls visible height.

>[!NOTE] Difference from input 
>Can contain multiple lines of text

## Select & Option

**[[Select Element]]**: Creates a dropdown menu.

**[[Option Element]]**: Defines each choice in the dropdown.

```html
<select name="overlord">
  <option value="gru">Gru</option>
  <option value="vector">Vector</option>
</select>
```

**value attribute**: What gets sent to the server (can differ from displayed text).

## Checkbox vs. Radio

### Checkbox

**[[Checkbox Input]]**: Select Many (multiple selections allowed).

```html
<input type="checkbox" name="toppings"> Pepperoni
```

>[!NOTE] Use case 
Multiple independent choices (pizza toppings, features, interests).

### Radio Button

**[[Radio Input]]**: Select One (only one selection allowed).

**Critical rule**: Must share the same `name` to be mutually exclusive.

```html
<input type="radio" name="payment"> Visa
<input type="radio" name="payment"> Mastercard
```

>[!NOTE] Behavior
>Selecting one automatically deselects others with the same name.

## The 'name' Attribute

**[[name Attribute]]**: Critical for server communication.

>[!NOTE] Distinction
>
>- **[[id Attribute]]**: For CSS/JavaScript (client-side)
>- **[[name attribute]]**: For the Server (data submission)

>**Critical warning**: If you forget `name`, the server sees **nothing**!


```html
<input type="email" name="email">
```

>[!NOTE] Why it matters: 
>The `name` becomes the key in the submitted data.

## Placeholders

**[[Placeholder Attribute]]**: Ghost text inside the input box.

**Behavior**: Disappears when you start typing.

```html
<input type="text" placeholder="Enter your SIN number...">
```

**Use case**: Provide hints or examples without using labels.

## Required & Disabled

### Required Validation

**[[required Attribute]]**: Forces user to fill in the field before submitting.

```html
<input type="text" required>
```

**Browser behavior**: Prevents form submission and shows error message if empty.

### Disabled Input

**[[disabled Attribute]]**: Makes the input uneditable and grayed out.

```html
<input type="text" disabled>
```

**Use case**: Show fields that aren't currently editable.
# Visualizing the Data

**What happens when you click Submit?**

The browser takes all `name` and `value` pairs and creates a **[[Query String]]**:

```
user=Kevin&pass=banana&overlord=gru
```

>[!NOTE] Format
>`name=value&name=value&name=value`

# External content

**[[iframe Element]]**: Cuts a "hole" in your site to show another website.

```html
<iframe src="https://www.wikipedia.org"></iframe>
```

**Concept**: Embeds external content directly into your page.

## YouTube Embeds

>Click Share > Embed on YouTube.

```html
<iframe width="560" height="315"
  src="https://www.youtube.com/embed/s5DjLT841eU?si=PtFWnyh93rERhZop">
</iframe>
```

## Google Maps Embeds

>Google Maps > Share > Embed a Map.

```html
<iframe src="http://googleusercontent.com/maps..."></iframe>
```

## iframe Attributes

**[[frameborder Attribute]]**: `frameborder="0"` removes ugly border.

**[[allowfullscreen Attribute]]**: Lets video go full screen.

**Example**:

```html
<iframe src="..." frameborder="0" allowfullscreen></iframe>
```

## The Dangers of iframes

**Restriction**: You can only iframe sites that **allow** it.

>[!NOTE] Blocked sites 
>Google/Facebook will block you from embedding them.

**Security**: Sites can use [[X-Frame-Options]] header to prevent being embedded.

## Audio (Review)

**[[Audio Element]]**: Embeds sound files.

```html
<audio controls>
  <source src="song.mp3" type="audio/mpeg">
</audio>
```

**[[controls Attribute]]**: Shows play/pause controls.

## Video (Review)

**[[Video Element]]**: Embeds video files.

```html
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
</video>
```

**Attributes**: Width, height, controls for user interface.

## Favicons

**[[Favicon]]**: The icon in the browser tab.

**Syntax** (in `<head>`):

```html
<head>
  <link rel="icon" href="favicon.ico">
</head>
```

**Purpose**: Branding and easy tab identification.

## Meta Tags (Social Media)

**[[Open Graph Meta Tags]]**: Control how your link looks on social media.

```html
<meta property="og:title" content="My Fan Page">
```

**What it does**: When you paste a link into Discord, Slack, or iMessage, this controls the preview card that appears.

**Without this tag**: Shows boring blue URL (www.mysite.com).

**With this tag**: Shows nice card with title "My Fan Page", image, and description.

**[[Social Media Preview]]**: The expanded link preview with image and text.

## Entities (Special Characters)

**[[HTML Entities]]**: Special codes for characters that can't be typed directly or have special meaning in HTML.

**Common entities**:

- `&copy;` → ©
- `&lt;` →
- `&gt;` → >
- `&nbsp;` → (Non-breaking space)

**Why needed**: `<` and `>` have special meaning in HTML, so must be escaped.

## Validation

**[[HTML Validation]]**: Check your code for errors.

**Tool**: Go to **[[validator.w3.org]]**

**Process**:

1. Upload your index.html
2. Fix the red errors
3. Verify warnings

**Purpose**: Ensures your HTML follows standards and works across browsers.

## The 'Code Bloat' Warning

**[[Code Bloat]]**: Unnecessary nesting of elements.

**Avoid this**:

```html
<div><div><div><p>No!</p></div></div></div>
```

**Better**: Use only the structure you need.

**Principle**: Keep HTML simple and semantic—don't add extra wrappers without purpose.

## Summary

**Tables**: `<table>`, `<tr>`, `<td>`, `<th>`

**Forms**: `<form>`, `<input>`, `<button>`, `<label>`

**Rich Media**: `<iframe>`, `<audio>`, `<video>`

**Key concepts**:

- Data tables for tabular information
- Forms for user input and interaction
- Embedding external content with iframes

## Lab #3 Introduction

**Project**: The Registration Page

**Goal**: Build a Sign-Up page with:

- A Data Table
- A Form

**Testing tool**: We'll use the "Magic Mirror" (**[[httpbin]]**) to test our data submission.

**Purpose**: See exactly what data your form sends to the server.

## Pro Tips for Lab

**Use `placeholder`**: Provide hints for what to enter.

**Use `required`**: Force users to fill in important fields.

**DON'T FORGET THE `name` ATTRIBUTE!**: Without it, the server receives no data from that field.

**Critical reminder**: `name` is what makes form data work—never skip it!

---

## Key Concepts to Review

### Tables

- [[Data Tables]]
- [[Layout Tables]]
- [[Screen Readers]]
- [[Table Element]]
- [[Table Row]]
- [[Table Data]]
- [[Table Header]]
- [[Caption Element]]
- [[Table Row Concept]]
- [[Temporary Cheat]]
- [[Colspan]]
- [[Rowspan]]
- [[Semantic Table Structure]]
- [[thead Element]]
- [[tbody Element]]
- [[tfoot Element]]

### Forms

- [[Form Element]]
- [[action Attribute]]
- [[method Attribute]]
- [[GET Method]]
- [[POST Method]]
- [[Request Body]]
- [[Fieldset Element]]
- [[Legend Element]]
- [[Input Element]]
- [[Text Input]]
- [[Password Input]]
- [[Email Input]]
- [[Date Input]]
- [[Color Input]]
- [[Range Input]]

### Form Controls

- [[Label Element]]
- [[for Attribute]]
- [[Button Element]]
- [[Textarea Element]]
- [[rows Attribute]]
- [[Select Element]]
- [[Option Element]]
- [[Checkbox Input]]
- [[Radio Input]]

### Form Attributes

- [[name Attribute]]
- [[id Attribute]]
- [[Query String]]
- [[Placeholder Attribute]]
- [[required Attribute]]
- [[disabled Attribute]]

### Rich Media

- [[iframe Element]]
- [[frameborder Attribute]]
- [[allowfullscreen Attribute]]
- [[X-Frame-Options]]
- [[Audio Element]]
- [[controls Attribute]]
- [[Video Element]]
- [[Favicon]]
- [[Open Graph Meta Tags]]
- [[Social Media Preview]]

### Miscellaneous

- [[HTML Entities]]
- [[HTML Validation]]
- [[validator.w3.org]]
- [[Code Bloat]]
- [[httpbin]]
- [[CSS]]
- [[Void Elements]]

---

## Review Questions

1. What is the "Restaurant Analogy" and how do forms relate to it?
    
2. When should you use tables in HTML? When should you NOT use tables?
    
3. Why is using tables for layout bad for accessibility?
    
4. What are the four main table elements? Explain what each does.
    
5. Where should the `<caption>` element be placed in a table?
    
6. Explain the "typewriter" analogy for understanding table rows.
    
7. What happens if you forget a `<td>` in a table row?
    
8. What is the difference between `colspan` and `rowspan`? Give an example of each.
    
9. What are the three semantic table sections (`<thead>`, `<tbody>`, `<tfoot>`) and when would you use each?
    
10. Why should you use `<th>` instead of `<td><b>Text</b></td>` for headers?
    
11. What are the two required attributes for the `<form>` element? What does each control?
    
12. Explain the difference between GET and POST methods. When would you use each?
    
13. What is the purpose of the `<fieldset>` and `<legend>` elements?
    
14. Why is the `<input>` element called the "Transformer" of HTML?
    
15. Name at least five different `type` values for the `<input>` element and what each creates.
    
16. What is the purpose of the `<label>` element? How do you properly associate it with an input?
    
17. What is the difference between the `id` and `name` attributes on form inputs?
    
18. What happens if you forget the `name` attribute on a form input?
    
19. What is a query string? Give an example of what form data looks like when submitted.
    
20. What does the `placeholder` attribute do? Is it a replacement for labels?
    
21. What does the `required` attribute do? What does `disabled` do?
    
22. What is the difference between `<input type="checkbox">` and `<input type="radio">`?
    
23. For radio buttons to work properly (only one selectable), what must they all share?
    
24. What is an `<iframe>` and what is it used for?
    
25. Can you iframe any website? What happens if a site blocks embedding?
    
26. Write the HTML for a table with:
    
    - Caption "Class Schedule"
    - Headers: Day, Time, Subject
    - Two data rows of your choice
27. Write a login form with:
    
    - Email input (with validation)
    - Password input
    - Submit button
    - Proper labels for accessibility
28. What is a favicon and how do you add one to your website?
    
29. What do Open Graph meta tags do? Why are they important for social media?
    
30. What is validator.w3.org used for? Why should you validate your HTML?
    

---

## Practical Exercises

### Exercise 1: Build a Course Schedule Table

Create a table showing your weekly schedule with:

- Caption: "Weekly Schedule"
- Columns: Time, Monday, Tuesday, Wednesday, Thursday, Friday
- At least 3 time slots
- Use `<th>` for all headers
- Use semantic sections (`<thead>`, `<tbody>`)

### Exercise 2: Registration Form

Build a registration form with:

- Full Name (text input, required)
- Email (email input, required)
- Password (password input, required)
- Date of Birth (date input)
- Gender (radio buttons: Male, Female, Other)
- Interests (checkboxes: Sports, Music, Art)
- Bio (textarea)
- Submit button
- All inputs must have proper labels and name attributes

### Exercise 3: Product Order Form

Create an order form for a pizza shop:

- Customer name (required)
- Phone number (required)
- Size (radio: Small, Medium, Large)
- Toppings (checkboxes: Pepperoni, Mushrooms, Olives, Extra Cheese)
- Special instructions (textarea)
- Organize using `<fieldset>` for "Customer Info" and "Pizza Options"

### Exercise 4: Table with Merged Cells

Create a table for a grade report:

- Student name spanning 2 columns in first row
- Headers: Assignment, Grade
- 3 assignments with grades
- Final row: "Average" spanning first column, grade in second

### Exercise 5: Embed Rich Media

Create a page with:

- An embedded YouTube video of your choice
- An embedded Google Map of Sault College
- Both should have appropriate width/height
- Remove borders and allow fullscreen

### Exercise 6: Contact Form with Validation

Build a contact form with:

- Name (required, placeholder: "John Doe")
- Email (required, email validation)
- Subject (required)
- Message (textarea, required, placeholder: "Enter your message...")
- All fields have proper labels
- Submit button
- Use POST method
- Action: "https://httpbin.org/post"

### Exercise 7: Fix the Broken Code

Find and fix all errors in this code:

```html
<table>
  <tr>
    <td><b>Name</b></td>
  </tr>
  <tr>
    <td>Alice
    <td>Bob</td>
  </tr>
</table>

<form>
  <input type="text" id="email">
  <input type="password" id="pass">
  <button type="button">Submit</button>
</form>
```

### Exercise 8: Survey Form

Create a survey form asking:

- Age range (select dropdown: 18-25, 26-35, 36-50, 50+)
- Satisfaction rating (range slider, 1-10)
- Would recommend? (radio: Yes, No)
- Comments (textarea)
- All with proper structure and validation

---

## Common Mistakes to Avoid

1. **Using tables for layout** - Tables are for data only, not positioning
2. **Forgetting closing tags on tables** - `<tr>`, `<td>`, `<th>` all need closing tags
3. **Missing `<th>` for headers** - Bad for accessibility
4. **Forgetting the `name` attribute** - Form data won't be submitted
5. **Using same `name` for radio buttons that shouldn't be grouped** - They'll interfere with each other
6. **Confusing `id` and `name`** - `id` for CSS/JS, `name` for server
7. **Not matching `for` and `id` in labels** - Label won't connect to input
8. **Using GET for sensitive data** - Passwords should use POST
9. **Forgetting `required` on important fields** - Users can submit incomplete forms
10. **Not providing labels for inputs** - Bad for accessibility
11. **Using placeholder as a replacement for labels** - Screen readers may not announce it
12. **Forgetting `type="button"` on non-submit buttons** - Will accidentally submit form
13. **Mismatched number of cells in table rows** - Creates broken tables
14. **Not validating HTML** - Errors may not be visible but break functionality
15. **Excessive div nesting** - Creates code bloat and maintenance issues

---

## Practical Tags for Obsidian

#HTML #Tables #Forms #WebForms #DataTables #UserInput #HTMLTables #FormValidation #Accessibility #WebDevelopment #Frontend #HTMLStructure #SemanticHTML #FormControls #InputTypes #RichMedia #iframes #HTMLBasics #WebDesign #UserInteraction #FormDesign #WebAccessibility #HTMLElements #InteractiveForms #WebContent