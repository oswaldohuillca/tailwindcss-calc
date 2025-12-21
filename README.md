# Tailwind CSS v4 Calc Plugin

A Tailwind CSS v4 plugin built entirely with CSS that provides responsive utilities using `calc()` and `clamp()` based on viewport width.

## 🚀 Features

- ✅ **100% CSS** - No JavaScript required
- ✅ **Tailwind CSS v4** - Compatible with the latest version
- ✅ **Viewport-based Scaling** - All utilities scale responsively using `calc()` and `clamp()`
- ✅ **Comprehensive Utilities** - Width, height, padding, margin, typography, positioning, and more
- ✅ **Customizable** - Adjust the base window width to fit your design

## 📦 Installation

```bash
npm install tailwindcss-calc
# or
bun add tailwindcss-calc
# or
pnpm add tailwindcss-calc
```

## 🚀 Quick Start

After installation, create your CSS file:

```css
/* styles.css */
@import "tailwindcss";
@import "tailwindcss-calc";
```

Then use the utilities in your HTML:

```html
<div class="w-500 h-300 p-20 m-10">
  <h1 class="text-32 mb-20">Hello World</h1>
  <p class="text-16 leading-24">Responsive content</p>
</div>
```

## 🛠️ Development

To run the example locally:

### Development

```bash
npm run dev
```

Open your browser at `http://localhost:5173` to see the demo.

### Build

```bash
npm run build
```

### Preview

```bash
npm run preview
```

## 🎨 How It Works

All utilities use this formula to scale based on viewport width:

```css
calc(value * clamp(0px, 100vw, max-width) / base-width)
```

**Default configuration:**
- Base width: `1920px`
- Max width: `1920px`

This means `w-100` will be:
- On mobile (375px): ~19.5px
- On tablet (768px): ~40px
- On desktop (1440px): ~75px
- On large screens (1920px): 100px
- On ultra-wide (>1920px): 100px (capped)

## 📚 Available Utilities

### Width & Height
```html
<div class="w-100 h-200">...</div>
<div class="size-50">...</div>
<div class="min-w-300 max-w-500">...</div>
<div class="min-h-400 max-h-600">...</div>
```

### Padding
```html
<div class="p-20">...</div>
<div class="px-30 py-40">...</div>
<div class="pt-10 pb-10 pl-15 pr-15">...</div>
```

### Margin
```html
<div class="m-20">...</div>
<div class="mx-auto my-30">...</div>
<div class="mt-10 mb-20 ml-5 mr-5">...</div>
```

### Typography
```html
<h1 class="text-48 leading-60">Title</h1>
<p class="text-16 tracking-2">Paragraph</p>
<span class="word-spacing-4">Text</span>
```

### Gap (Flexbox & Grid)
```html
<div class="flex gap-20">...</div>
<div class="grid gap-x-30 gap-y-40">...</div>
<div class="grid grid-gap-25">...</div>
```

### Border Radius
```html
<div class="rounded-10">...</div>
<div class="rounded-20">...</div>
```

### Positioning
```html
<div class="top-50 left-100">...</div>
<div class="bottom-20 right-30">...</div>
<div class="inset-10">...</div>
<div class="inset-x-20 inset-y-30">...</div>
```

### Transform
```html
<div class="translate-x-50">...</div>
<div class="translate-y-100">...</div>
```

### Borders
```html
<div class="border-w-2">...</div>
<div class="border-t-1 border-b-1">...</div>
<div class="border-l-3 border-r-3">...</div>
```

### Outline
```html
<div class="outline-offset-4">...</div>
```

### Container
```html
<div class="container">Centered content with max-width</div>
```

## 📁 Project Structure

```
tailwindcss-calc/
├── src/
│   └── plugin.css         # Main plugin file
├── example/               # Demo folder
│   ├── index.html        # Demo page
│   ├── index.css         # Example CSS
│   ├── package.json      # Example dependencies
│   └── vite.config.js    # Vite configuration
├── package.json          # Root package.json
├── LICENSE              # MIT License
└── README.md            # This file
```

## 🔧 How to Use in Your Project

### Option 1: Install from npm (Recommended)

1. Install the package:

```bash
npm install tailwindcss-calc
```

2. Import in your CSS file:

```css
@import "tailwindcss";
@import "tailwindcss-calc";
```

That's it! All utilities are now available.

### Option 2: Import from node_modules

```css
@import "tailwindcss";
@import "tailwindcss-calc/src/plugin.css";
```

### Option 3: Copy the source

Copy the content from `src/plugin.css` and paste it into your main CSS file after `@import "tailwindcss"`.

**Important:** Use `@import` for CSS files, not `@plugin`. The `@plugin` directive is only for JavaScript files in Tailwind CSS v4.

## ⚙️ Customization

Edit `src/plugin.css` and modify the theme variables:

```css
@theme {
  --window-width: 1920;  /* Change base width */
}
```

You can also add new utilities following the same pattern:

```css
@utility custom-* {
  custom-property: calc(--value(integer) * clamp(0px, 100vw, var(--window-max-width)) / var(--window-width));
}
```

## 💡 Use Cases

Perfect for:
- **Fixed designs** that need to scale to different screen sizes
- **Design-to-code** workflows where you want pixel-perfect scaling
- **Responsive layouts** without multiple breakpoints
- **Prototyping** with design specs that use a fixed reference width

## 🌟 Advantages

1. **Simplicity** - No JavaScript configuration needed
2. **Performance** - Pure CSS, no runtime overhead
3. **Maintainability** - Easy to understand and modify
4. **Consistency** - All values scale proportionally
5. **Flexibility** - Works with any design reference width

## 📚 Resources

- [Tailwind CSS v4 Documentation](https://tailwindcss.com/docs)
- [CSS calc() Function](https://developer.mozilla.org/en-US/docs/Web/CSS/calc)
- [CSS clamp() Function](https://developer.mozilla.org/en-US/docs/Web/CSS/clamp)
- [Vite](https://vitejs.dev/)

## 📄 License

MIT

## 🚀 Publishing & Releases

This project uses [changelogen](https://unjs.io/packages/changelogen) for automatic changelog generation, npm publishing, and GitHub releases.

### Release Workflow

1. **Make changes** following conventional commits
2. **Run release command** (automatically bumps version, updates CHANGELOG, commits, creates git tag, publishes to npm, and pushes to GitHub)
3. **GitHub Action** automatically creates GitHub release when tag is pushed

### Release Commands

```bash
# Patch release (0.0.x) - for bug fixes
npm run release
# or
npm run release:patch

# Minor release (0.x.0) - for new features
npm run release:minor

# Major release (x.0.0) - for breaking changes
npm run release:major

# Only generate changelog (no publish)
npm run changelog

# Create GitHub release from existing tag
npm run release:gh
```

### What Happens on Release

1. ✅ Analyzes commits since last release
2. ✅ Determines version bump (semver)
3. ✅ Updates `CHANGELOG.md`
4. ✅ Updates version in `package.json`
5. ✅ Creates git commit with changes
6. ✅ Creates git tag (e.g., `v1.0.0`)
7. ✅ Pushes to GitHub
8. ✅ Publishes to npm
9. ✅ GitHub Action creates release (automatically)

### Commit Convention

Use [conventional commits](https://www.conventionalcommits.org/) for automatic changelog generation:

```bash
feat: add new utility          # Minor bump (new feature)
fix: resolve calc issue        # Patch bump (bug fix)
perf: improve performance      # Patch bump (performance)
docs: update README            # No version bump
refactor: simplify code        # Patch bump (refactor)
style: format code             # No version bump
test: add tests                # No version bump
chore: update dependencies     # No version bump
ci: update workflow            # No version bump

# Breaking changes (Major bump)
feat!: change API completely
fix!: breaking fix

# Or with body
feat: add new feature

BREAKING CHANGE: This changes the API
```

### Setup Requirements

#### For npm Publishing

1. **Create npm account** at [npmjs.com](https://www.npmjs.com/)
2. **Login locally**: `npm login`
3. **Set npm token in GitHub** (for CI):
   - Create token at [npmjs.com/settings/tokens](https://www.npmjs.com/settings/tokens)
   - Add as `NPM_TOKEN` in GitHub repository secrets

#### For GitHub Releases

GitHub token is automatically available in GitHub Actions via `GITHUB_TOKEN`.

For local releases with GitHub integration:
- Use GitHub CLI: `gh auth login`
- Or set `GITHUB_TOKEN` environment variable

## 🤝 Contributing

Contributions are welcome! Please:

1. Use conventional commits for your changes
2. Run tests before submitting PR
3. Update documentation if needed
4. Open an issue or pull request
