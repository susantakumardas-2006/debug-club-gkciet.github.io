# 🎨 Theme System Guide - GKCIET Coding Club Website

> **TL;DR**: Use CSS custom properties (`var(--variable-name)`) in all new styles. The theme system automatically handles light/dark mode switching. No manual color management needed!

---

## 📋 Quick Overview

This website implements a **CSS Custom Properties-based theme system** that automatically switches between:
- **Dark Theme**: Neon green (#00FF9D) on black (#030305)  
- **Light Theme**: Blue (#2563EB) on white/slate

All new elements will automatically adapt to both themes when using the provided CSS variables.

---

## 🎯 How to Add New Elements (The Right Way)

### Method 1: Using CSS Variables (Recommended)

Always use CSS custom properties for new styles:

```scss
.my-new-card {
    // ✓ Good - automatically switches themes
    background-color: var(--bg-surface) !important;
    color: var(--text-primary) !important;
    border: 1px solid var(--border-color) !important;
}

.my-new-button {
    // ✓ Good - uses theme colors
    background: var(--primary-brand) !important;
    color: var(--bg-dark) !important;
    
    &:hover {
        background: var(--primary-brand-hover) !important;
    }
}

.my-text-element {
    // ✓ Good - proper text contrast in both themes
    color: var(--text-secondary) !important;
}
```

### Method 2: Using Utility Classes

Pre-built utility classes are available:

```html
<!-- Text Colors -->
<p class="text-brand">Highlighted text (brand color)</p>
<p class="text-brand-light">Secondary text</p>
<p class="text-brand-muted">Muted text</p>

<!-- Backgrounds -->
<div class="bg-theme-surface">Themed container</div>
<div class="bg-theme-elevated">Elevated surface</div>

<!-- Buttons -->
<button class="btn btn-theme-primary">Primary Button</button>
<button class="btn btn-theme-secondary">Secondary Button</button>

<!-- Icons -->
<div class="icon-inherit">
    <i class="fas fa-github"></i> <!-- Inherits text color -->
</div>
```

---

## 📚 Available CSS Variables

### Color Variables

**Dark Theme (`:root`)**
| Variable | Value | Use Case |
|----------|-------|----------|
| `--primary-brand` | #00FF9D | Main accent, links |
| `--primary-brand-hover` | #5CFFC3 | Hover states |
| `--primary-brand-dim` | #00CC7D | Dimmed states |
| `--secondary-brand` | #BC13FE | Secondary accent |
| `--accent-cyan` | #00F0FF | Tertiary accent |

**Light Theme (`body.light-theme`)**
| Variable | Value | Use Case |
|----------|-------|----------|
| `--primary-brand` | #2563EB | Main accent, links |
| `--primary-brand-hover` | #1D4ED8 | Hover states |
| `--primary-brand-dim` | #1E40AF | Dimmed states |
| `--secondary-brand` | #7C3AED | Secondary accent |
| `--accent-cyan` | #06B6D4 | Tertiary accent |

### Background Variables

| Variable | Dark Value | Light Value | Use Case |
|----------|-----------|------------|----------|
| `--bg-dark` | #030305 | #F0F4F8 | Main background |
| `--bg-surface` | #0a0a0c | #FFFFFF | Surface/card background |
| `--bg-surface-elevated` | #121216 | #F8FAFC | Elevated surfaces |
| `--bg-surface-lighter` | #1A1A20 | #F1F5F9 | Lighter surfaces |

### Text Variables

| Variable | Dark Value | Light Value | Use Case |
|----------|-----------|------------|----------|
| `--text-primary` | #FFFFFF | #0F172A | Main text |
| `--text-secondary` | #B0B0C0 | #475569 | Secondary text |
| `--text-muted` | #6E6E7A | #94A3B8 | Muted/helper text |
| `--text-disabled` | #404045 | #CBD5E1 | Disabled text |
| `--border-color` | rgba(255,255,255,0.08) | rgba(15,23,42,0.12) | Borders/dividers |

---

## 💡 Common Patterns

### Cards & Containers
```scss
.my-card {
    background-color: var(--bg-surface) !important;
    color: var(--text-primary) !important;
    border: 1px solid var(--border-color) !important;
    border-radius: 8px;
    padding: 1rem;
    
    h3, h4, h5 {
        color: var(--text-primary) !important;
    }
    
    p {
        color: var(--text-secondary) !important;
    }
}
```

### Form Inputs
```scss
input, textarea {
    background-color: var(--bg-surface) !important;
    color: var(--text-primary) !important;
    border: 1px solid var(--border-color) !important;
    
    &:focus {
        border-color: var(--primary-brand) !important;
        box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.15) !important;
    }
    
    &::placeholder {
        color: var(--text-muted) !important;
    }
}
```

### Buttons
```scss
.btn-custom {
    background-color: var(--primary-brand) !important;
    color: var(--bg-dark) !important;
    border: 1px solid var(--primary-brand) !important;
    
    &:hover {
        background-color: var(--primary-brand-hover) !important;
        border-color: var(--primary-brand-hover) !important;
    }
    
    &:active {
        background-color: var(--primary-brand-dim) !important;
    }
}
```

### Text Elements
```scss
.custom-heading {
    color: var(--text-primary) !important;
    font-weight: 700;
}

.custom-description {
    color: var(--text-secondary) !important;
}

.custom-helper-text {
    color: var(--text-muted) !important;
    font-size: 0.875rem;
}
```

### Icon Styling
```scss
.my-icon-button {
    color: var(--text-secondary) !important;
    
    // Ensure icons inherit color
    i, .fas, .fab, .far, svg {
        color: inherit !important;
    }
    
    &:hover {
        color: var(--primary-brand) !important;
    }
}
```

---

## ⚠️ What NOT to Do

```scss
/* ✗ BAD - Hardcoded colors won't change themes */
.my-element {
    background-color: #030305;  // Dark mode only!
    color: #00FF9D;             // Won't work in light mode!
}

/* ✗ BAD - Missing !important flags can be overridden */
.my-button {
    color: var(--text-primary);  // Might get overridden
}

/* ✓ GOOD */
.my-element {
    background-color: var(--bg-surface) !important;
    color: var(--text-primary) !important;
}
```

---

## 🔄 Theme Switching Mechanism

The website uses a JavaScript-based theme switcher located at `assets/js/theme-switcher.js`:

1. User clicks the theme toggle button
2. JavaScript sets `data-bs-theme` and applies `body.light-theme` class
3. CSS variables in `body.light-theme` override `:root` values
4. All elements using `var(--variable-name)` automatically update

**This happens instantly - no page reload needed!**

---

## 📁 File Structure

```
_sass/custom/
├── _variables.scss        # SCSS variables (color definitions)
├── _main.scss            # Core styles + CSS custom properties definitions
│   └── :root             # Dark theme CSS variables
│   └── body.dark-theme   # Explicit dark theme overrides (if needed)
├── _light-theme.scss     # Light theme CSS variable overrides
│   └── body.light-theme  # Light theme CSS variables
├── _core_values.scss     # Custom brand section styling
├── _team.scss            # Team section styling
└── (other partials)

assets/js/
└── theme-switcher.js     # Theme toggle JavaScript
```

---

## ✅ Checklist for Adding New Elements

When adding a new page, component, or element:

- [ ] Use `var(--variable-name)` for all colors (no hardcoded values)
- [ ] Add `!important` flags to ensure styles apply
- [ ] Test in both **dark mode** and **light mode**
- [ ] Check text contrast (readable in both themes)
- [ ] Ensure icons inherit text color with `color: inherit !important`
- [ ] Test hover/focus states in both themes
- [ ] Use utility classes when possible (`.text-brand`, `.bg-theme-surface`)
- [ ] If creating new component class, add to both `:root` and `body.light-theme` if using custom values

---

## 🌐 Example: Adding a New Page

Here's how to add a styled new page element:

```html
<section class="py-5 themed-section">
    <div class="container">
        <h1 class="text-brand">New Section Title</h1>
        <p class="text-brand-light">This text uses secondary color</p>
        
        <div class="card bg-theme-surface border-theme">
            <div class="card-body">
                <h3>Card Title</h3>
                <p>Card content with proper theming</p>
            </div>
        </div>
    </div>
</section>
```

The `.themed-section` class automatically provides:
- Correct background for dark/light mode
- Appropriate text colors
- Proper heading colors
- Full theme support

---

## 🔧 Troubleshooting

**Element looks wrong in light mode?**
- Check if you used hardcoded colors instead of variables
- Add `!important` to your CSS rules
- Verify the element isn't being overridden by a more specific selector

**Colors not changing on theme toggle?**
- Make sure you're using `var(--variable-name)` not `$scss-variable`
- Check browser cache (clear it!)
- Verify the CSS is compiled from SCSS

**Text not readable?**
- Use `--text-primary` for main text
- Use `--text-secondary` for secondary text  
- Use `--text-muted` for helper/disabled text
- Avoid mixing dark/light text on wrong background

---

## 📞 Questions?

Refer to the inline documentation in:
- `_sass/custom/_main.scss` - Comprehensive utility class examples
- `_sass/custom/_light-theme.scss` - Theme override system documentation
- Individual component SCSS files - Specific styling patterns

**Key Principle**: If you use CSS custom properties, the theme system handles everything else!

---

**Happy styling! 🎨**
