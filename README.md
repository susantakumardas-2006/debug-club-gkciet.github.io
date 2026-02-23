# Coding Club Website

A website for our coding club built with Jekyll and the [CS50 theme](https://github.com/cs50/jekyll-theme-cs50/).

## Quick Start

### Prerequisites

- [Ruby](https://www.ruby-lang.org/) (>= 2.5) & Bundler
- [Node.js](https://nodejs.org/) (>= 18) & npm
- [Python 3](https://www.python.org/) with `Pygments` (`pip install Pygments`)
- Git

### Installation

1. **Clone this repository**
   ```bash
   git clone <your-repo-url>
   cd <your-repo-name>
   ```

2. **Install vendor assets**

   On **Linux/macOS** (or CI):
   ```bash
   npm install
   ```
   On **Windows**:
   ```bash
   npm install --ignore-scripts
   python setup_assets.py
   ```
   This fetches vendor libraries into `assets/` and generates SASS files in `_sass/`.

3. **Install Ruby dependencies**
   ```bash
   bundle install
   ```

4. **Run locally**
   ```bash
   bundle exec jekyll serve
   ```

5. **View the site**
   Open your browser and navigate to `http://localhost:4000`

> **Note:** The vendor assets (`assets/bootstrap/`, `_sass/bootstrap/`, etc.) are not committed to the repo, they are generated at install time. See `setup_assets.py` for details.

## Customization Guide

### 1. Basic Configuration

Edit [_config.yml](_config.yml) to set your club's basic information:

```yaml
cs50:
  title: "Debug Club @GKCIET"          # Change to your club's name
  description: "Modify club tagline"  # Change to your club's tagline
  tz: Asia/Kolkata             # Change to your timezone
```

### 2. Site Content

Edit [_data/site.yml](_data/site.yml) to update the following dynamic content:
- **Hero Section**: Title, description, and call-to-action buttons.
- **Stats Bar**: Active members, projects count, and Discord status.


### 3. Update Navigation

Edit [_includes/nav.md](_includes/nav.md) to customize the navigation menu. Add or remove pages as needed.

### 4. Update Header & Footer

- **Header / Navbar**: Edit [`_includes/navbar.html`](_includes/navbar.html) to add a logo or modify the header/navigation
- **Footer**: Edit [`_includes/footer_custom.html`](_includes/footer_custom.html) to add contact info and social links

### 5. Customize Pages

Replace the placeholder content in these pages:

- **Home**: [index.md](index.md)
- **About**: [about.md](about.md)
- **Events**: [events.md](events.md)
- **Projects**: [projects.md](projects.md)
- **Resources**: [resources.md](resources.md)
- **todos**: [todo.md](todo.md)


### 6. Add an Alert Banner

To add a site-wide alert banner:

1. Uncomment the `alert` line in `_config.yml`:
   ```yaml
   cs50:
     alert: warning  # Can be: primary, secondary, success, danger, warning, info, light, dark
   ```

2. Edit [_includes/alert.md](_includes/alert.md) with your alert message

### 7. Update Logo 

1. Add your logo image to the `assets/` folder
2. Uncomment the logo line in [_includes/header.md](_includes/header.md):
   ```markdown
   ![Club Logo](/assets/your-logo.png)
   ```

## Content Guidelines

### Using Special Features

#### Time Display
Display times in visitors' local timezones:
```markdown
{% local "2025-03-15 18:00" %}
```

#### Alerts
Create colored alert boxes:
```markdown
{% alert primary %}
Your alert message here
{% endalert %}
```

Types: `primary`, `secondary`, `success`, `danger`, `warning`, `info`, `light`, `dark`

#### Spoilers
Hide content behind a clickable reveal:
```markdown
{% spoiler "Click to reveal" %}
Hidden content here
{% endspoiler %}
```

#### Collapsible Lists
- Use `*` for regular bullets
- Use `+` for collapsed subtrees
- Use `-` for expanded subtrees

### Adding New Pages

1. Create a new `.md` file in the root directory
2. Add the page to [_includes/nav.md](_includes/nav.md)

## Customizing Styles

### Theme System (CSS Variables)

**⚡ IMPORTANT: Read this before adding any new styles or components!**

This website uses a **CSS Variable-based theme system** that automatically supports both light and dark modes. When you add new elements, you MUST follow this pattern to ensure they work in both themes.

#### The Golden Rule

Always use CSS variables for colors - never hardcode color values:

```scss
// ✅ CORRECT - This will work in both light and dark modes
.my-new-component {
    background-color: var(--bg-surface) !important;
    color: var(--text-primary) !important;
    border: 1px solid var(--border-color) !important;
}

// ❌ WRONG - This will only work in dark mode
.my-new-component {
    background-color: #0a0a0c;  // Won't change in light mode!
    color: #FFFFFF;              // Hard to read in light mode!
}
```

#### Available CSS Variables

Use these variables in your styles. They automatically adapt to light/dark themes:

**Colors & Accents:**
- `var(--primary-brand)` - Main accent color
- `var(--secondary-brand)` - Secondary accent
- `var(--accent-cyan)` - Tertiary accent

**Backgrounds:**
- `var(--bg-dark)` - Main page background
- `var(--bg-surface)` - Card/container background
- `var(--bg-surface-elevated)` - Elevated surfaces
- `var(--bg-surface-lighter)` - Light surfaces

**Text:**
- `var(--text-primary)` - Main headings and important text
- `var(--text-secondary)` - Body text and descriptions
- `var(--text-muted)` - Helper text, disabled text
- `var(--text-disabled)` - Disabled state text

**Utility:**
- `var(--border-color)` - Borders and dividers

#### Quick Examples

**Adding a new card:**
```scss
.my-card {
    background-color: var(--bg-surface) !important;
    color: var(--text-primary) !important;
    border: 1px solid var(--border-color) !important;
    border-radius: 8px;
    padding: 1rem;
}
```

**Adding a new button:**
```scss
.btn-custom {
    background-color: var(--primary-brand) !important;
    color: var(--bg-dark) !important;
    
    &:hover {
        background-color: var(--primary-brand-hover) !important;
    }
}
```

**Adding text with proper contrast:**
```scss
.my-description {
    color: var(--text-secondary) !important;  // Body text
}

.my-helper-text {
    color: var(--text-muted) !important;  // Subtle/disabled text
}
```

#### How It Works

- **Dark Theme** (default): Neon green accents (#00FF9D) on black background
- **Light Theme**: Blue accents (#2563EB) on white background
- When users toggle the theme, CSS variables automatically update
- Any element using these variables instantly adapts - no extra code needed!

#### Pre-built Utility Classes

Want to skip writing SCSS? Use these ready-made classes:

```html
<!-- Text colors -->
<p class="text-brand">Highlighted text</p>
<p class="text-brand-light">Secondary text</p>
<p class="text-brand-muted">Muted/helper text</p>

<!-- Backgrounds -->
<div class="bg-theme-surface">Card-like container</div>
<div class="bg-theme-elevated">Elevated surface</div>

<!-- Buttons -->
<button class="btn btn-theme-primary">Primary Button</button>
<button class="btn btn-theme-secondary">Secondary Button</button>

<!-- Containers -->
<div class="themed-container">Auto-themed container</div>
<section class="themed-section">Auto-themed section</section>
```

#### Checklist Before Submitting Code

When you add any new element (page, component, card, button):

- [ ] Used `var(--variable-name)` for ALL colors
- [ ] Added `!important` flags to CSS rules
- [ ] Tested in **dark mode** - does it look good?
- [ ] Tested in **light mode** - does it look good?
- [ ] Text is readable in both themes
- [ ] Hover/focus states work in both themes

#### For More Details

See the complete theme guide: [THEME-SYSTEM-GUIDE.md](THEME-SYSTEM-GUIDE.md)

---

### Custom Styling (Advanced)

To customize colors and styles, create `assets/page.scss`:

```scss
---
---

$link-color: #286dc0;  // Change link color

@import "page";

aside {
    background-color: #00356b;  // Change sidebar color
}
```

## Documentation

- **CS50 Jekyll Theme**: https://cs50.readthedocs.io/themes/jekyll/
- **Jekyll Documentation**: https://jekyllrb.com/docs/
- **Markdown Guide**: https://www.markdownguide.org/

## Deployment

### GitHub Pages

1. Push your repository to GitHub
2. Go to repository Settings → Pages
3. Set source to main branch
4. Your site will be available at `https://yourusername.github.io/repository-name/`

### Other Hosting Options

- **Netlify**: Connect your GitHub repo for automatic deployments
- **Vercel**: Similar to Netlify with easy GitHub integration
- **Custom Server**: Run `bundle exec jekyll build` and deploy the `_site/` folder

##  Project Structure

```
.
├── _config.yml           # Site configuration
├── _includes/            # Reusable components
│   ├── header.md        # Site header
│   ├── nav.md           # Navigation menu
│   ├── footer.md        # Site footer
│   └── alert.md         # Alert banner (optional)
├── _layouts/            # Page layouts
├── _sass/               # Styles
├── assets/              # Images, CSS, JS
├── index.md             # Home page
├── about.md             # About page
├── events.md            # Events page
├── projects.md          # Projects page
├── resources.md         # Resources page
└── README.md            # This file
```

##  Troubleshooting

### Port already in use
If port 4000 is already in use, specify a different port:
```bash
bundle exec jekyll serve --port 4001
```

### Changes not showing
Jekyll caches content. Try:
```bash
bundle exec jekyll clean
bundle exec jekyll serve
```

### Ruby version issues
Check your Ruby version:
```bash
ruby --version
```
Install the required version using a version manager like [rbenv](https://github.com/rbenv/rbenv) or [RVM](https://rvm.io/).

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project uses the CS50 Jekyll theme. See [LICENSE](LICENSE) for details.

## Support

- **Theme Documentation**: https://cs50.readthedocs.io/themes/jekyll/
- **Theme Repository**: https://github.com/cs50/jekyll-theme-cs50/
- **Jekyll Help**: https://jekyllrb.com/docs/

---

Built with ❤️ using [Jekyll](https://jekyllrb.com/) and the [CS50 theme](https://github.com/cs50/jekyll-theme-cs50/)
