# Tailwind CSS Practice — INT-001

> **Module:** M2 Deep React + Styling  
> **Task:** TailwindCSS Fundamentals  
> **Author:** Metaniya Shiferaw  
> **Status:** In Progress

---

## What this project is

This project was built as a hands-on exercise to learn **TailwindCSS** from the ground up. The goal was to understand the utility-first workflow by building a real UI — a responsive dashboard with a Navbar, Sidebar, Card Grid, and Dark Mode — in **two different ways**:

1. Using **Tailwind CSS** (utility classes directly in HTML)
2. Using **Plain HTML + CSS** (traditional approach, for comparison)

Having both versions side by side makes it easy to see exactly what Tailwind replaces and why it speeds up development.

---

## Folder structure

```
TAILWIND-PRACTICE/
├── tailwind/
│   └── index.html        # Dashboard built with Tailwind CSS CDN
├── plain-css/
│   ├── index.html        # Same dashboard built with plain HTML
│   └── style.css         # All the CSS written manually
└── README.md
```

---

## What was built

Both versions include the exact same UI components:

### Navbar
A sticky top navigation bar that stays visible when you scroll. It contains the app brand on the left, navigation links in the center, and a dark mode toggle button on the right. On desktop the links are always visible. On mobile they collapse and a hamburger button appears instead.

### Sidebar
A left-side navigation panel with three links: Dashboard, Projects, and Settings. The active link is highlighted in purple. Clicking any link updates the highlight instantly. The sidebar is hidden on mobile screens to save space.

### Responsive Card Grid
Three profile cards displayed in a grid. The grid changes column count based on screen width — one column on mobile, two on tablet, three on desktop. Each card has an avatar circle, a name, a role, and a colored status badge.

### Dark Mode
A toggle button switches the entire page between light and dark themes. In the Tailwind version this works by adding a `dark` class to the `<html>` element. In the plain CSS version it works by adding a `dark` class to `<body>`.

---

## Why JavaScript is included

This project is HTML and CSS focused, but three small JavaScript functions were necessary. No libraries or frameworks are used — it is all plain vanilla JS.

### 1. `toggleDark()` — Dark mode switch
```js
function toggleDark() {
  document.documentElement.classList.toggle('dark') // Tailwind version
  // or
  document.body.classList.toggle('dark')            // Plain CSS version
}
```
CSS alone cannot respond to a button click. JavaScript is needed to add or remove the `dark` class when the user presses the toggle button. Once the class is added, all the dark-mode styles activate automatically through CSS.

### 2. `toggleMenu()` — Mobile hamburger menu
```js
let menuOpen = false
function toggleMenu() {
  menuOpen = !menuOpen
  document.getElementById('mobileMenu').style.display = menuOpen ? 'flex' : 'none'
}
```
The mobile menu is hidden by default. When the user taps the hamburger icon, JavaScript flips a `menuOpen` boolean and shows or hides the dropdown by setting `style.display`. Using `style.display` directly (instead of toggling a CSS class) was important in the Tailwind version because Tailwind's `hidden` class uses `!important`, which would override any class-based toggle.

### 3. `setActive()` — Sidebar active link highlight
```js
function setActive(e, el) {
  e.preventDefault()
  document.querySelectorAll('.sidebar-link').forEach(l => l.classList.remove('active'))
  el.classList.add('active')
}
```
When a sidebar link is clicked, JavaScript removes the `active` class from all links and adds it only to the clicked one. This is how active/selected state is managed in navigation without a full framework. `e.preventDefault()` stops the page from jumping to `#` when the link is clicked.

---

## How responsive design works

Responsive design means the layout adjusts automatically based on screen width. No separate mobile version exists — it is one layout that adapts.

### In Tailwind (breakpoint prefixes)
Tailwind uses prefixes directly on classes:
```html
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3">
```
- No prefix → applies to all screens (mobile first)
- `sm:` → applies at 640px and above (tablet)
- `md:` → applies at 768px and above
- `lg:` → applies at 1024px and above (desktop)

The navbar links use `hidden md:flex` — invisible on mobile, flex row on desktop. The hamburger uses `md:hidden` — only shows on mobile.

### In Plain CSS (media queries)
The same logic is written as traditional `@media` rules in `style.css`:
```css
/* Mobile — 1 column */
.card-grid { grid-template-columns: repeat(1, 1fr); }

/* Tablet — 2 columns */
@media (min-width: 640px) {
  .card-grid { grid-template-columns: repeat(2, 1fr); }
}

/* Desktop — 3 columns */
@media (min-width: 1024px) {
  .card-grid { grid-template-columns: repeat(3, 1fr); }
}

/* Hide sidebar and desktop links on mobile */
@media (max-width: 767px) {
  aside { display: none; }
  .nav-links { display: none; }
  .hamburger { display: flex; }
}
```

Tailwind is just a shorthand for writing these same rules — instead of a separate CSS file, the breakpoints live directly on the HTML element.

---

## Key Tailwind concepts practised

| Concept | Example classes used |
|---|---|
| Typography | `text-xl`, `font-bold`, `text-gray-500` |
| Spacing | `p-4`, `px-6`, `mb-3`, `gap-6` |
| Flexbox | `flex`, `items-center`, `justify-between`, `gap-3` |
| Grid | `grid`, `grid-cols-3`, `col-span-2` |
| Responsive | `sm:grid-cols-2`, `md:flex`, `lg:grid-cols-3` |
| Dark mode | `dark:bg-gray-800`, `dark:text-white` |
| Hover states | `hover:text-purple-600`, `hover:bg-gray-100` |
| Transitions | `transition-colors`, `transition-shadow` |

---

## How to run locally

No installation or build step required.

1. Clone the repo:
   ```bash
   git clone https://github.com/YOUR_USERNAME/tailwind-practice.git
   ```
2. Open either file directly in your browser:
   - `tailwind/index.html` — Tailwind version
   - `plain-css/index.html` — Plain CSS version

That's it. The Tailwind version loads the framework from a CDN so an internet connection is needed for it to work correctly.

---

## How to push this to GitHub

```bash
# 1. Open your project folder in terminal
cd path/to/TAILWIND-PRACTICE

# 2. Initialize git
git init

# 3. Add all files
git add .

# 4. First commit
git commit -m "feat: add tailwind and plain CSS dashboard - INT-001"

# 5. Go to github.com, create a new repo called tailwind-practice
#    then connect it:
git remote add origin https://github.com/YOUR_USERNAME/tailwind-practice.git

# 6. Push
git branch -M main
git push -u origin main
```
