### **HTML Interview Questions**

**1. What is the difference between `id` and `class` attributes in HTML?**  
- `id` is unique and used to identify a single element, while `class` can be shared by multiple elements.  
- `id` is used for specific tasks like targeting elements in JavaScript or CSS, whereas `class` is for grouping elements.  
- You can use the `#` selector in CSS for `id` and the `.` selector for `class`.  
- Example: In a project, I used `id` for a login form and `class` for styling multiple buttons.  

```html
<div id="login-form">Login Form</div>
<button class="btn">Submit</button>
```

**2. Explain the difference between `<section>` and `<div>`.**  
- `<section>` is semantic, indicating a thematic grouping of content.  
- `<div>` is non-semantic and used for general-purpose grouping.  
- `<section>` provides context for accessibility and SEO, while `<div>` requires extra attributes for the same.  
- Example: I used `<section>` to divide the blog into articles and `<div>` for layout structuring.  

```html
<section>
  <h2>Blog Post</h2>
  <p>Content of the blog.</p>
</section>
<div class="container">Wrapper for layout</div>
```

**3. What is the difference between inline and block-level elements?**  
- Inline elements occupy only as much width as necessary and don’t start on a new line.  
- Block-level elements take up the full width of their container and start on a new line.  
- Common inline elements include `<span>` and `<a>`, while `<div>` and `<p>` are block elements.  
- Example: I styled a navigation menu using `<a>` (inline) and organized sections using `<div>` (block).  

```html
<a href="#">Home</a>
<div class="block-element">Content</div>
```

**4. How does the `<meta>` tag work in HTML?**  
- It provides metadata about the HTML document, such as character set and viewport settings.  
- Metadata doesn’t appear on the page but affects how it’s rendered and indexed by search engines.  
- Examples include `<meta charset="UTF-8">` and `<meta name="viewport" content="width=device-width, initial-scale=1.0">`.  
- Example: I used `<meta>` to ensure responsiveness in my e-commerce project.  

```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**5. What is the purpose of the `<link>` tag in HTML?**  
- It connects the HTML document to external resources like stylesheets or icons.  
- Commonly used for including CSS files with `rel="stylesheet"`.  
- It can also be used for preloading assets with attributes like `rel="preload"`.  
- Example: In my project, I used `<link>` to include a CSS file for consistent theming.  

```html
<link rel="stylesheet" href="styles.css">
```

**6. What are semantic HTML tags? Provide examples.**  
- Semantic tags clearly define the meaning and structure of the content.  
- Examples include `<header>`, `<article>`, `<footer>`, and `<aside>`.  
- They improve accessibility and SEO by providing context to the content.  
- Example: I used semantic tags to enhance the readability of my portfolio website.  

```html
<header>
  <h1>Welcome to My Portfolio</h1>
</header>
<article>
  <p>About me section...</p>
</article>
```

**7. How does the `<canvas>` element work in HTML?**  
- `<canvas>` is used for rendering graphics, like drawings or animations, using JavaScript.  
- It requires a `width` and `height` attribute for defining the canvas area.  
- Graphics are created using a 2D or 3D context with JavaScript.  
- Example: I implemented an interactive graph on a dashboard using `<canvas>`.  

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
<script>
  const canvas = document.getElementById("myCanvas");
  const ctx = canvas.getContext("2d");
  ctx.fillStyle = "blue";
  ctx.fillRect(10, 10, 100, 50);
</script>
```

**8. What is the difference between `async` and `defer` attributes in a `<script>` tag?**  
- `async` loads the script asynchronously and executes it as soon as it’s available.  
- `defer` loads the script asynchronously but waits until the HTML parsing is complete before execution.  
- Use `async` for independent scripts and `defer` for scripts that depend on the DOM.  
- Example: I used `defer` in my project to load a script that manipulates DOM elements.  

```html
<script src="script.js" defer></script>
```

**9. What are empty elements in HTML?**  
- Elements that do not have closing tags and cannot contain content.  
- Examples include `<br>`, `<img>`, `<meta>`, and `<input>`.  
- They are self-closing and used for standalone purposes like inserting a line break or an image.  
- Example: I used `<img>` for displaying product images in a catalog.  

```html
<img src="product.jpg" alt="Product Image">
```

**10. Explain the purpose of the `<template>` tag.**  
- The `<template>` tag holds HTML content that is not rendered on page load.  
- It is useful for reusing blocks of content dynamically using JavaScript.  
- Content inside a `<template>` is inert until cloned and appended to the DOM.  
- Example: I used `<template>` to dynamically generate cards in a shopping app.  

```html
<template id="card-template">
  <div class="card">
    <h3>Product Name</h3>
  </div>
</template>
<script>
  const template = document.getElementById("card-template").content.cloneNode(true);
  document.body.appendChild(template);
</script>
```

**11. What is the purpose of the `data-*` attributes in HTML?**  
- Custom attributes to store extra data directly on HTML elements.  
- Useful for transferring data to JavaScript without affecting layout or performance.  
- Data is accessed via `dataset` in JavaScript.  
- Example: I used `data-*` to store user preferences in an interactive app.  

```html
<div id="user" data-role="admin">User Info</div>
<script>
  const role = document.getElementById("user").dataset.role;
  console.log(role); // Output: admin
</script>
```

**12. What is the difference between `<b>` and `<strong>` tags?**  
- `<b>` is used for stylistic purposes to bold text, without semantic meaning.  
- `<strong>` conveys importance and has semantic meaning in addition to styling.  
- Search engines and screen readers prioritize `<strong>` over `<b>`.  
- Example: I used `<strong>` in a terms and conditions page to emphasize critical points.  

```html
<p><strong>Important:</strong> Read the guidelines carefully.</p>
```

**13. How does the `contenteditable` attribute work in HTML?**  
- It makes an element editable directly in the browser.  
- Accepts values `true` (editable) or `false` (non-editable).  
- Useful for creating rich-text editors or inline editing features.  
- Example: I implemented `contenteditable` in a project for live profile editing.  

```html
<div contenteditable="true">Edit this text</div>
```

**14. Explain the `<details>` and `<summary>` tags in HTML.**  
- `<details>` creates a collapsible container for content.  
- `<summary>` defines the visible heading that the user clicks to expand/collapse the details.  
- It’s a semantic and interactive alternative to toggle visibility.  
- Example: I used `<details>` to display FAQs on a support page.  

```html
<details>
  <summary>What is your refund policy?</summary>
  <p>We offer a 30-day refund policy.</p>
</details>
```

**15. What is the purpose of the `autofocus` attribute in HTML?**  
- Automatically focuses an input element when the page loads.  
- It’s applied to elements like `<input>`, `<textarea>`, or `<button>`.  
- Improves usability by directing the user to the primary interaction field.  
- Example: I used `autofocus` on the search bar of an e-commerce homepage.  

```html
<input type="text" autofocus placeholder="Search products">
```

### **HTML Interview Questions (Continued)**

**16. What is the purpose of the `<picture>` element in HTML?**  
- The `<picture>` element is used for providing multiple image sources for responsive designs.  
- It allows specifying images for different screen sizes or formats using `<source>` tags.  
- Helps optimize performance by loading the most appropriate image for the device.  
- Example: I used `<picture>` to display high-resolution images on desktop and smaller ones on mobile.  

```html
<picture>
  <source srcset="image-large.jpg" media="(min-width: 800px)">
  <source srcset="image-small.jpg" media="(max-width: 799px)">
  <img src="image-default.jpg" alt="Responsive Image">
</picture>
```

**17. How do you include external JavaScript in an HTML document?**  
- Use the `<script>` tag with the `src` attribute pointing to the script file.  
- Place the `<script>` tag in the `<head>` or before the closing `<body>` tag.  
- Add `async` or `defer` attributes to control script execution timing.  
- Example: In my project, I included a JavaScript file to handle form validation.  

```html
<script src="form-validation.js" defer></script>
```

**18. What are web storage APIs, and how are they used?**  
- Web storage APIs, `localStorage` and `sessionStorage`, store data in the browser.  
- `localStorage` persists data across sessions, while `sessionStorage` clears after the tab is closed.  
- Data is stored as key-value pairs and accessed using JavaScript.  
- Example: I used `localStorage` to save user preferences in a dashboard application.  

```javascript
localStorage.setItem("theme", "dark");
console.log(localStorage.getItem("theme")); // Output: dark
```

**19. What is the purpose of the `<noscript>` tag?**  
- Displays alternative content if JavaScript is disabled or unsupported in the browser.  
- Useful for providing fallback options to enhance user experience.  
- Typically contains instructions or links to upgrade the browser or enable JavaScript.  
- Example: I used `<noscript>` to show a message for a JavaScript-based interactive map.  

```html
<noscript>
  <p>Please enable JavaScript to use the interactive map.</p>
</noscript>
```

**20. What is the purpose of the `aria-*` attributes in HTML?**  
- ARIA (Accessible Rich Internet Applications) attributes improve web accessibility.  
- Used to define roles, states, and properties for screen readers.  
- Examples include `aria-label`, `aria-hidden`, and `aria-live`.  
- Example: I implemented `aria-label` to improve navigation accessibility in a web app.  

```html
<button aria-label="Submit form">Submit</button>
```

**21. How does the `<fieldset>` element work in HTML?**  
- Groups related elements in a form for better organization and accessibility.  
- Typically used with the `<legend>` element to provide a caption.  
- Enhances form semantics and user experience.  
- Example: I used `<fieldset>` to group address fields in a registration form.  

```html
<fieldset>
  <legend>Address</legend>
  <input type="text" placeholder="Street">
  <input type="text" placeholder="City">
</fieldset>
```

**22. What is the difference between `relative`, `absolute`, and `fixed` URLs?**  
- Relative URLs are based on the location of the current document.  
- Absolute URLs specify the complete path, including protocol and domain.  
- Fixed URLs typically reference local files using a specific root.  
- Example: I used relative URLs to link internal pages and absolute URLs for external resources.  

```html
<a href="/about.html">Relative URL</a>
<a href="https://example.com">Absolute URL</a>
```

**23. What are the limitations of the `<iframe>` element?**  
- Can cause performance issues due to additional resource loading.  
- Some websites block embedding in `<iframe>` using the `X-Frame-Options` header.  
- Less secure, as it may expose the site to clickjacking attacks.  
- Example: I used `<iframe>` to embed Google Maps but ensured proper security measures.  

```html
<iframe src="https://maps.google.com" width="600" height="400"></iframe>
```

**24. What is the purpose of the `download` attribute in `<a>` tag?**  
- Enables file downloads when the link is clicked.  
- Specifies a filename for the downloaded file.  
- Improves user experience by skipping the file preview step.  
- Example: I used the `download` attribute to allow users to download invoices.  

```html
<a href="invoice.pdf" download="Invoice.pdf">Download Invoice</a>
```

**25. How does the `required` attribute in form elements work?**  
- Makes the input field mandatory for form submission.  
- It is supported by `<input>`, `<textarea>`, and `<select>` elements.  
- Provides basic client-side validation without JavaScript.  
- Example: I used `required` to ensure users fill in critical fields in a contact form.  

```html
<input type="text" required placeholder="Enter your name">
```

**26. What are the differences between the `<ol>` and `<ul>` elements?**  
- `<ol>` creates an ordered list with numbered or lettered items.  
- `<ul>` creates an unordered list with bullet points.  
- Both use `<li>` for list items, but their purposes differ.  
- Example: I used `<ol>` for steps in a process and `<ul>` for navigation links.  

```html
<ol>
  <li>Step 1</li>
  <li>Step 2</li>
</ol>
<ul>
  <li>Home</li>
  <li>About</li>
</ul>
```

**27. How does the `placeholder` attribute work in form fields?**  
- Displays a short hint inside the input field before the user enters data.  
- Used in `<input>` and `<textarea>` elements.  
- It disappears once the user starts typing.  
- Example: I used `placeholder` in a login form to guide users.  

```html
<input type="text" placeholder="Enter your username">
```

**28. What is the use of the `<time>` element?**  
- Represents a specific point in time or a duration.  
- Useful for events, publishing dates, or time-based data.  
- Can include the `datetime` attribute for machine-readable formatting.  
- Example: I used `<time>` to display event dates in a calendar app.  

```html
<time datetime="2024-12-01">December 1, 2024</time>
```

**29. What are the `autocomplete` attribute values in form fields?**  
- `on` enables and `off` disables browser autofill suggestions.  
- Helps improve the user experience by remembering input values.  
- Supported by `<input>`, `<textarea>`, and `<form>` elements.  
- Example: I enabled `autocomplete` for email fields in a signup form.  

```html
<input type="email" autocomplete="on" placeholder="Enter your email">
```

**30. How does the `<progress>` element work in HTML?**  
- Displays a progress bar for tasks like uploads or installations.  
- Requires `value` and `max` attributes to define progress and completion.  
- Provides a semantic way to represent progress.  
- Example: I used `<progress>` to show file upload status in a project.  

```html
<progress value="50" max="100">50%</progress>
```

### **CSS Interview Questions**

**31. What is the difference between `inline`, `inline-block`, and `block` elements in CSS?**  
- `inline`: Elements do not start on a new line and only take up as much width as necessary.  
- `inline-block`: Similar to `inline` but allows setting width and height.  
- `block`: Elements start on a new line and take up the full width available.  
- Example: I used `inline-block` for navigation links and `block` for main content sections.  

```css
.nav-item {
  display: inline-block;
  margin: 5px;
}
```

**32. How does the `z-index` property work in CSS?**  
- Defines the stack order of elements; higher values are closer to the front.  
- Works only on elements with a position value other than `static`.  
- Negative values are allowed to push elements further back.  
- Example: I used `z-index` to overlay a modal on top of page content.  

```css
.modal {
  position: fixed;
  z-index: 1000;
}
```

**33. What are pseudo-classes in CSS?**  
- Pseudo-classes define the special state of an element, such as `:hover` or `:nth-child()`.  
- They do not modify the content directly but change its appearance based on the state.  
- Useful for user interactions and conditional styling.  
- Example: I used `:hover` to create button hover effects in a landing page.  

```css
button:hover {
  background-color: blue;
  color: white;
}
```

**34. What is the difference between relative, absolute, fixed, and sticky positioning in CSS?**  
- `relative`: Positions the element relative to its normal position.  
- `absolute`: Positions the element relative to its nearest positioned ancestor.  
- `fixed`: Positions the element relative to the viewport, staying in place on scroll.  
- Example: I used `sticky` for a header that stays at the top while scrolling down a page.  

```css
header {
  position: sticky;
  top: 0;
  background: white;
}
```

**35. How does the `flexbox` layout work in CSS?**  
- Provides a flexible layout for distributing space among items in a container.  
- Uses properties like `justify-content`, `align-items`, and `flex-wrap`.  
- Simplifies alignment and spacing for both horizontal and vertical layouts.  
- Example: I used `flexbox` to center align content in a card layout.  

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
```

**36. What is the purpose of the `grid-template-areas` property in CSS Grid?**  
- Defines named grid areas to simplify the placement of elements in the grid.  
- Areas are specified using strings that map out the grid layout.  
- Works with the `grid-area` property to position elements.  
- Example: I used `grid-template-areas` to organize a header, sidebar, and main content in a dashboard.  

```css
.container {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main";
}
```

**37. What is the difference between `em`, `rem`, and `px` in CSS?**  
- `px`: Absolute unit, fixed size independent of parent or root.  
- `em`: Relative to the font size of the parent element.  
- `rem`: Relative to the root element’s font size.  
- Example: I used `rem` for scalable typography in a responsive design.  

```css
h1 {
  font-size: 2rem;
}
```

**38. How does the `clip-path` property work in CSS?**  
- Clips an element to a specific shape, such as a circle or polygon.  
- Accepts values like `circle()`, `ellipse()`, and `polygon()`.  
- Used for creative design effects and masking content.  
- Example: I used `clip-path` to create custom shapes for images in a gallery.  

```css
.image {
  clip-path: circle(50%);
}
```

**39. What are the different types of CSS selectors?**  
- Universal selector (`*`): Selects all elements.  
- Type selector (`element`): Targets specific tags like `div` or `p`.  
- Class selector (`.class`): Selects elements with a specific class.  
- Example: I used a combination of type and class selectors to style a blog post layout.  

```css
p.intro {
  font-size: 1.2em;
  color: gray;
}
```

**40. What is the difference between `absolute` and `relative` units in CSS?**  
- Absolute units (`px`, `in`, `cm`): Fixed size, unaffected by parent elements.  
- Relative units (`em`, `%`, `vw`, `vh`): Dependent on parent or viewport size.  
- Absolute units provide consistency, while relative units enable responsiveness.  
- Example: I used `%` and `vw` for responsive layout designs.  

```css
.container {
  width: 80%;
  height: 50vh;
}
```

**41. What are media queries, and how are they used?**  
- Media queries apply styles based on device characteristics like screen size.  
- Use `@media` rules to define styles for different breakpoints.  
- Commonly used for responsive designs.  
- Example: I used media queries to adjust grid layouts for tablets and mobile devices.  

```css
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}
```

**42. What is the purpose of the `transition` property in CSS?**  
- Adds smooth animations between state changes, like hover effects.  
- Can specify properties like duration, delay, and easing functions.  
- Simplifies creating animations without JavaScript.  
- Example: I used `transition` for button hover effects in an interactive UI.  

```css
button {
  transition: background-color 0.3s ease;
}
button:hover {
  background-color: blue;
}
```

**43. How does the `object-fit` property work in CSS?**  
- Defines how an image or video fits within a container.  
- Common values: `cover`, `contain`, `fill`, and `none`.  
- Prevents distortion by maintaining the aspect ratio of media.  
- Example: I used `object-fit: cover` for profile pictures in a user list.  

```css
img {
  width: 100px;
  height: 100px;
  object-fit: cover;
}
```

**44. What are keyframe animations in CSS?**  
- Define animations by breaking them into key states using `@keyframes`.  
- Specify intermediate steps for properties like position or color.  
- Animations are applied with the `animation` property.  
- Example: I created a loading spinner using keyframe animations.  

```css
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
.loader {
  animation: spin 2s infinite linear;
}
```

**45. What is the difference between `visibility: hidden` and `display: none`?**  
- `visibility: hidden`: Hides the element but still occupies space in the layout.  
- `display: none`: Completely removes the element from the layout.  
- `visibility: hidden` is useful for toggling visibility without layout changes.  
- Example: I used `display: none` to collapse a sidebar menu on mobile.  

```css
.sidebar {
  display: none;
}
```

### **CSS Interview Questions (Continued)**

**46. How does the `overflow` property work in CSS?**  
- Controls what happens to content that overflows the container’s bounds.  
- Common values: `visible`, `hidden`, `scroll`, and `auto`.  
- Ensures layout stability by handling overflow content gracefully.  
- Example: I used `overflow: scroll` to enable scrolling for a long table in a dashboard.  

```css
.table-container {
  height: 300px;
  overflow: scroll;
}
```

**47. What is the purpose of the `box-shadow` property in CSS?**  
- Adds shadow effects around elements.  
- Defines offsets, blur radius, spread radius, and shadow color.  
- Can create depth and elevate elements visually.  
- Example: I applied `box-shadow` to buttons for a material design-inspired UI.  

```css
.button {
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
}
```

**48. What is the difference between `min-width`, `max-width`, and `width`?**  
- `width`: Sets the exact width of an element.  
- `min-width`: Defines the minimum width an element can have.  
- `max-width`: Sets the maximum width, allowing flexibility.  
- Example: I used `max-width` to constrain content in a responsive design.  

```css
.container {
  width: 100%;
  max-width: 1200px;
}
```

**49. How does the `opacity` property work in CSS?**  
- Controls the transparency level of an element, with values from `0` (fully transparent) to `1` (fully opaque).  
- Affects both the element and its content.  
- Often combined with transitions for fade effects.  
- Example: I used `opacity` to create hover effects for image captions.  

```css
.image-caption {
  opacity: 0;
  transition: opacity 0.5s;
}
.image:hover .image-caption {
  opacity: 1;
}
```

**50. What are CSS variables, and how are they used?**  
- Custom properties defined using the `--` prefix and accessed with `var()`.  
- Provide reusability and easier maintenance of styles.  
- Can be scoped to specific elements or globally in `:root`.  
- Example: I used CSS variables for consistent theming in a web application.  

```css
:root {
  --primary-color: #3498db;
}
.button {
  background-color: var(--primary-color);
}
```

**51. How does the `float` property work in CSS?**  
- Positions elements to the left or right of their container.  
- Commonly used for creating text wrapping around images.  
- Requires `clear` to avoid overlapping issues with succeeding elements.  
- Example: I used `float` to align product images beside descriptions in an e-commerce site.  

```css
.image {
  float: left;
  margin-right: 10px;
}
```

**52. What is the difference between `inline` and `inline-block` display values?**  
- `inline`: Allows elements to flow inline with text but cannot set width/height.  
- `inline-block`: Combines inline flow with the ability to set width/height.  
- Suitable for creating flexible layouts with precise spacing.  
- Example: I used `inline-block` for responsive grid items in a gallery.  

```css
.gallery-item {
  display: inline-block;
  width: 30%;
}
```

**53. How does the `cursor` property work in CSS?**  
- Changes the mouse pointer style when hovering over an element.  
- Common values: `pointer`, `default`, `text`, and `not-allowed`.  
- Enhances UX by visually indicating interactions.  
- Example: I used `cursor: pointer` for interactive buttons in a form.  

```css
.button {
  cursor: pointer;
}
```

**54. What is the difference between `absolute` and `fixed` positioning in CSS?**  
- `absolute`: Positions the element relative to its nearest positioned ancestor.  
- `fixed`: Positions the element relative to the viewport, unaffected by scrolling.  
- Both require `top`, `right`, `bottom`, or `left` properties for placement.  
- Example: I used `fixed` for a sticky navigation bar on a scrolling page.  

```css
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
}
```

**55. How do you use the `nth-child` pseudo-class in CSS?**  
- Targets elements based on their position within a parent.  
- Accepts values like `odd`, `even`, or specific numbers (e.g., `2n+1`).  
- Useful for styling alternating rows in tables or lists.  
- Example: I used `nth-child` to apply alternate background colors to table rows.  

```css
tr:nth-child(even) {
  background-color: #f2f2f2;
}
```

**56. What is the purpose of the `position: sticky` property?**  
- Keeps an element fixed within a container until a specific scroll position is reached.  
- Combines relative and fixed positioning.  
- Requires `top`, `right`, `bottom`, or `left` to define the sticky boundary.  
- Example: I used `position: sticky` for table headers in a long-scroll table.  

```css
th {
  position: sticky;
  top: 0;
  background: white;
}
```

**57. How does the `white-space` property work in CSS?**  
- Controls how text is handled within an element.  
- Common values: `normal` (default), `nowrap`, `pre`, and `break-spaces`.  
- Helps manage line breaks and spacing.  
- Example: I used `white-space: nowrap` to prevent wrapping in navigation menus.  

```css
.nav-item {
  white-space: nowrap;
}
```

**58. What is the difference between `transform` and `transition` in CSS?**  
- `transform`: Applies transformations like rotation, scaling, or translation to elements.  
- `transition`: Defines the timing for changes between states.  
- Often used together for smooth animated effects.  
- Example: I used `transform` and `transition` to create hover animations on icons.  

```css
.icon {
  transform: scale(1);
  transition: transform 0.3s;
}
.icon:hover {
  transform: scale(1.2);
}
```

**59. How does the `background-size` property work in CSS?**  
- Defines how the background image is sized within its container.  
- Common values: `auto`, `cover`, `contain`, and specific dimensions.  
- Ensures proper scaling without distortion.  
- Example: I used `background-size: cover` for full-page hero images.  

```css
.hero {
  background-image: url('hero.jpg');
  background-size: cover;
}
```

**60. What is the difference between `border` and `outline` in CSS?**  
- `border`: Affects the layout and can change the size of the element box.  
- `outline`: Does not affect layout; it’s drawn outside the border box.  
- Outlines are often used for focus indication and accessibility.  
- Example: I used `outline` to highlight form fields during validation errors.  

```css
input:focus {
  outline: 2px solid blue;
}
```

### **JavaScript Interview Questions**

**61. What is the difference between `var`, `let`, and `const` in JavaScript?**  
- `var`: Function-scoped, can be redeclared, and hoisted but not block-scoped.  
- `let`: Block-scoped, cannot be redeclared in the same scope, and not hoisted.  
- `const`: Block-scoped, immutable reference, but the value can still be mutable if it's an object.  
- Example: I used `const` for API keys and `let` for loop counters in a data-processing app.  

```javascript
const API_KEY = "abc123";
let counter = 0;
```

**62. What are JavaScript closures?**  
- A closure is a function that retains access to its lexical scope even when executed outside it.  
- Useful for data encapsulation and private variables.  
- Created automatically when a function is defined inside another function.  
- Example: I used closures to create reusable utility functions in a project.  

```javascript
function createCounter() {
  let count = 0;
  return function () {
    count++;
    return count;
  };
}
const counter = createCounter();
console.log(counter()); // Output: 1
```

**63. What is the difference between `==` and `===` in JavaScript?**  
- `==` performs type coercion, converting operands to the same type before comparison.  
- `===` checks for strict equality without type conversion.  
- Using `===` avoids unexpected results due to type coercion.  
- Example: I used `===` to validate user inputs in a form validation script.  

```javascript
console.log(1 == "1"); // true
console.log(1 === "1"); // false
```

**64. How does the `this` keyword work in JavaScript?**  
- Refers to the context in which the function is executed.  
- In global scope, it refers to `window` in browsers or `global` in Node.js.  
- In methods, it refers to the object the method belongs to.  
- Example: I used `this` in a class to refer to instance properties and methods.  

```javascript
class User {
  constructor(name) {
    this.name = name;
  }
  greet() {
    console.log(`Hello, ${this.name}`);
  }
}
const user = new User("Alice");
user.greet(); // Output: Hello, Alice
```

**65. What is event delegation in JavaScript?**  
- A technique where a parent element handles events for its child elements.  
- Reduces memory usage by attaching fewer event listeners.  
- Uses the `target` property to identify the clicked element.  
- Example: I used event delegation to manage a dynamic list of tasks in a to-do app.  

```javascript
document.querySelector(".task-list").addEventListener("click", (e) => {
  if (e.target.tagName === "LI") {
    e.target.classList.toggle("completed");
  }
});
```

**66. What is the difference between synchronous and asynchronous JavaScript?**  
- Synchronous: Tasks are executed one after another, blocking the main thread.  
- Asynchronous: Tasks are executed without waiting for other tasks to complete, using callbacks or promises.  
- Async methods prevent UI freezing during long-running tasks.  
- Example: I used asynchronous APIs to fetch data without blocking page rendering.  

```javascript
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

**67. How do `call()`, `apply()`, and `bind()` work in JavaScript?**  
- `call()`: Invokes a function with a specific `this` value and arguments as a list.  
- `apply()`: Similar to `call()` but accepts arguments as an array.  
- `bind()`: Returns a new function with `this` bound to the specified context.  
- Example: I used `bind()` to pass a method as a callback with the correct `this` context.  

```javascript
const obj = { name: "Alice" };
function greet() {
  console.log(`Hello, ${this.name}`);
}
const boundGreet = greet.bind(obj);
boundGreet(); // Output: Hello, Alice
```

**68. What is the purpose of `Promises` in JavaScript?**  
- Promises handle asynchronous operations and avoid callback hell.  
- Has three states: pending, resolved, and rejected.  
- Methods like `then()`, `catch()`, and `finally()` handle promise outcomes.  
- Example: I used Promises for sequential API calls in a weather app.  

```javascript
fetch("https://api.example.com/weather")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

**69. What is the difference between `let` and `var` in loops?**  
- `let` is block-scoped, so each iteration gets a new instance.  
- `var` is function-scoped, so the value persists across iterations.  
- Using `let` prevents issues in closures inside loops.  
- Example: I used `let` in a loop to ensure proper scoping for event listeners.  

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000); // Outputs 0, 1, 2
}
```

**70. What is the purpose of the `async` and `await` keywords in JavaScript?**  
- Simplify writing asynchronous code, making it look synchronous.  
- `async` marks a function to return a Promise.  
- `await` pauses execution until the Promise resolves or rejects.  
- Example: I used `async/await` to handle API responses in a cleaner way.  

```javascript
async function fetchData() {
  try {
    const response = await fetch("https://api.example.com/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}
fetchData();
```

**71. What are JavaScript modules, and how are they used?**  
- Modules allow code to be split into reusable and maintainable pieces.  
- Export functionality using `export` and import it in other files using `import`.  
- Supported natively in modern browsers and Node.js.  
- Example: I used modules to separate utility functions in a large-scale app.  

```javascript
// math.js
export function add(a, b) {
  return a + b;
}
// app.js
import { add } from "./math.js";
console.log(add(2, 3)); // Output: 5
```

**72. How does JavaScript handle data types?**  
- JavaScript has dynamic typing, so variables can hold any data type.  
- Includes six primitive types (e.g., string, number) and objects.  
- Type conversion occurs automatically or can be enforced.  
- Example: I ensured type validation for user inputs in a form.  

```javascript
const age = "30";
console.log(Number(age) + 5); // Output: 35
```

**73. What is the difference between `null` and `undefined` in JavaScript?**  
- `null` is explicitly assigned to indicate the absence of value.  
- `undefined` means a variable is declared but not assigned a value.  
- Both are falsy values but represent different states.  
- Example: I used `null` to reset an object property after deletion.  

```javascript
let obj = { name: "Alice" };
obj.name = null;
console.log(obj.name); // Output: null
```

**74. What are arrow functions, and how do they differ from regular functions?**  
- Arrow functions have a concise syntax and do not have their own `this`.  
- Cannot be used as constructors or with `new`.  
- Useful for callbacks and anonymous functions.  
- Example: I used arrow functions for event listeners in a React project.  

```javascript
const add = (a, b) => a + b;
console.log(add(2, 3)); // Output: 5
```

**75. What is the purpose of the `reduce()` method in JavaScript?**  
- Executes a reducer function on an array to accumulate a single output.  
- Takes two arguments: an accumulator and the current value.  
- Commonly used for aggregating data.  
- Example: I used `reduce()` to calculate the total price in a shopping cart.  

```javascript
const prices = [10, 20, 30];
const total = prices.reduce((acc, price) => acc + price, 0);
console.log(total); // Output: 60
```

### **JavaScript Interview Questions (Continued)**

**76. What is the difference between `map()`, `filter()`, and `forEach()` in JavaScript?**  
- `map()`: Returns a new array by applying a function to each element of the original array.  
- `filter()`: Returns a new array with elements that satisfy a given condition.  
- `forEach()`: Executes a function for each element but does not return a new array.  
- Example: I used `map()` to transform data, `filter()` to extract matching records, and `forEach()` to log each item during debugging.  

```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(num => num * 2); // [2, 4, 6, 8]
const evens = numbers.filter(num => num % 2 === 0); // [2, 4]
numbers.forEach(num => console.log(num)); // Logs 1, 2, 3, 4
```

**77. What are JavaScript generators, and how are they used?**  
- Generators are functions that can be paused and resumed, defined using `function*`.  
- Use `yield` to pause execution and produce values.  
- Useful for iterating over sequences or managing asynchronous workflows.  
- Example: I used generators to handle paginated API responses lazily.  

```javascript
function* numbers() {
  yield 1;
  yield 2;
  yield 3;
}
const gen = numbers();
console.log(gen.next().value); // Output: 1
console.log(gen.next().value); // Output: 2
```

**78. How does the `setTimeout()` function work in JavaScript?**  
- Executes a callback function after a specified delay in milliseconds.  
- Does not block other code execution.  
- Returns a timeout ID that can be used to clear the timeout.  
- Example: I used `setTimeout()` to show a delayed welcome message on page load.  

```javascript
setTimeout(() => {
  console.log("Welcome!");
}, 2000); // Logs "Welcome!" after 2 seconds
```

**79. What is the difference between `setTimeout()` and `setInterval()`?**  
- `setTimeout()`: Executes a function once after a specified delay.  
- `setInterval()`: Executes a function repeatedly at specified intervals.  
- Both return IDs for managing or clearing timers.  
- Example: I used `setInterval()` to update a digital clock every second.  

```javascript
setInterval(() => {
  const now = new Date();
  console.log(now.toLocaleTimeString());
}, 1000);
```

**80. How does the `typeof` operator work in JavaScript?**  
- Returns the type of a given operand as a string.  
- Works for primitive types and objects but has some quirks (e.g., `typeof null` returns `"object"`).  
- Useful for type checking in dynamic environments.  
- Example: I used `typeof` to validate API response data types.  

```javascript
console.log(typeof 42); // Output: "number"
console.log(typeof "Hello"); // Output: "string"
console.log(typeof null); // Output: "object"
```

**81. What is the difference between `Object.keys()`, `Object.values()`, and `Object.entries()`?**  
- `Object.keys()`: Returns an array of an object's property names.  
- `Object.values()`: Returns an array of an object's property values.  
- `Object.entries()`: Returns an array of key-value pairs.  
- Example: I used `Object.entries()` to iterate over an object in a dashboard app.  

```javascript
const user = { name: "Alice", age: 25 };
console.log(Object.keys(user)); // ["name", "age"]
console.log(Object.values(user)); // ["Alice", 25]
console.log(Object.entries(user)); // [["name", "Alice"], ["age", 25]]
```

**82. What is the event loop in JavaScript?**  
- The mechanism that handles asynchronous operations in JavaScript.  
- Uses a queue to process events and execute callbacks.  
- Ensures non-blocking behavior in single-threaded environments.  
- Example: I debugged an issue where `setTimeout()` callbacks were delayed due to a blocking loop.  

```javascript
setTimeout(() => console.log("First"), 0);
console.log("Second"); // Logs "Second" first, then "First"
```

**83. How do you deep copy an object in JavaScript?**  
- Use `JSON.parse(JSON.stringify(object))` for simple objects without methods.  
- For complex objects, use libraries like Lodash or custom recursive functions.  
- Deep copies create entirely new references, unlike shallow copies.  
- Example: I used deep copying to duplicate nested configuration objects safely.  

```javascript
const obj = { a: 1, b: { c: 2 } };
const deepCopy = JSON.parse(JSON.stringify(obj));
console.log(deepCopy.b === obj.b); // Output: false
```

**84. What are JavaScript WeakMaps and WeakSets?**  
- WeakMaps: Collections of key-value pairs where keys are weakly referenced objects.  
- WeakSets: Collections of unique weakly referenced objects.  
- Prevent memory leaks as objects are garbage-collected when no longer referenced.  
- Example: I used WeakMaps to store metadata for DOM elements dynamically.  

```javascript
const weakMap = new WeakMap();
const obj = {};
weakMap.set(obj, "value");
console.log(weakMap.get(obj)); // Output: "value"
```

**85. How do `try`, `catch`, and `finally` blocks work in JavaScript?**  
- `try`: Contains code that may throw an error.  
- `catch`: Handles the error and prevents application crashes.  
- `finally`: Executes code regardless of whether an error occurred.  
- Example: I used a `try-catch` block to handle API request errors gracefully.  

```javascript
try {
  const data = JSON.parse('{"key": "value"}');
  console.log(data);
} catch (error) {
  console.error("Invalid JSON", error);
} finally {
  console.log("Parsing attempt completed.");
}
```

**86. What is a JavaScript `Proxy`?**  
- An object that wraps another object and intercepts operations like property access and assignment.  
- Provides custom behavior for fundamental operations using traps.  
- Useful for validation, logging, or mocking.  
- Example: I used a Proxy to validate object property updates in a settings manager.  

```javascript
const settings = {
  theme: "dark",
};
const proxy = new Proxy(settings, {
  set(target, prop, value) {
    if (prop === "theme" && !["dark", "light"].includes(value)) {
      throw new Error("Invalid theme");
    }
    target[prop] = value;
    return true;
  },
});
proxy.theme = "light"; // Works
// proxy.theme = "blue"; // Throws an error
```

**87. What are template literals in JavaScript?**  
- Allow string interpolation using backticks (`) and placeholders `${expression}`.  
- Support multi-line strings without escape characters.  
- Simplify concatenation and dynamic string creation.  
- Example: I used template literals to dynamically create HTML content in a component.  

```javascript
const name = "Alice";
const greeting = `Hello, ${name}!`;
console.log(greeting); // Output: "Hello, Alice!"
```

**88. How does destructuring work in JavaScript?**  
- Extracts values from arrays or properties from objects into variables.  
- Supports default values for missing properties.  
- Simplifies code for accessing nested data.  
- Example: I used destructuring to extract specific fields from API responses.  

```javascript
const user = { name: "Alice", age: 25 };
const { name, age } = user;
console.log(name, age); // Output: "Alice", 25
```

**89. What are JavaScript promises chaining and error handling?**  
- Chaining allows sequential execution of multiple `then()` calls.  
- Errors can be caught and handled with `catch()` in any step.  
- Ensures clean and manageable asynchronous code.  
- Example: I used promise chaining to fetch user data, then their posts.  

```javascript
fetch("/user")
  .then((response) => response.json())
  .then((user) => fetch(`/posts?userId=${user.id}`))
  .then((response) => response.json())
  .then((posts) => console.log(posts))
  .catch((error) => console.error(error));
```

**90. How do you handle exceptions in asynchronous code?**  
- Use `try-catch` blocks inside `async` functions.  
- Attach `.catch()` to promises to handle errors.  
- Prevents unhandled rejections that can crash the application.  
- Example: I used error handling in `async/await` functions to manage API failures.  

```javascript
async function fetchData() {
  try {
    const response = await fetch("/data");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}
fetchData();
``` 
