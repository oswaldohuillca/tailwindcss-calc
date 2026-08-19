# Tailwind CSS v4 Calc Plugin

A Tailwind CSS v4 plugin built entirely with CSS that provides responsive utilities using `calc()` and `clamp()` based on viewport width.

Write the pixel values from your mockup — `w-100`, `p-20`, `text-32` — and every one of them scales with the viewport. **One breakpoint, two design references, no JavaScript.**

## 🚀 Features

- ✅ **100% CSS** - No JavaScript required
- ✅ **Tailwind CSS v4** - Compatible with the latest version
- ✅ **Viewport-based Scaling** - All utilities scale responsively using `calc()` and `clamp()`
- ✅ **Comprehensive Utilities** - Width, height, padding, margin, typography, positioning, and more
- ✅ **One breakpoint** - `md` swaps the base reference; no `md:` ladder for sizing
- ✅ **Customizable** - Set the base widths to match your own mockups

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

/* Your two design references — this is the entire configuration */
@layer theme {
  :root {
    --window-width: 375; /* mobile mockup */
  }

  @variant md {
    :root {
      --window-width: 1440; /* desktop mockup */
    }
  }
}
```

Then use the utilities in your HTML:

```html
<div class="w-500 h-300 p-20 m-10">
  <h1 class="text-32 mb-20">Hello World</h1>
  <p class="text-16 leading-24">Responsive content</p>
</div>
```

The defaults are already `375` / `1440`, so you can skip the `@layer theme`
block entirely if those match your mockups.

## 🛠️ Development

To run the example locally:

### Development

```bash
bun run dev
# or: npm run dev
```

Open your browser at `http://localhost:5173` to see the demo.

### Build

```bash
bun run build
```

### Preview

```bash
bun run preview
```

## 🎨 How It Works

All utilities use this formula to scale based on viewport width:

```css
calc(value * clamp(0px, 100vw, max-width) / base-width)
```

The formula is centralized in a single `--calc-ratio` variable, so every
utility multiplies its numeric value by the same viewport-based factor.

**Default configuration (mobile-first):**
- Base width: `375px`
- Max width: `375px`
- At the `md` breakpoint (`≥48rem`) the base scales up to `1440px`

This means `w-100` will be:
- On a 320px screen: ~85px
- At 375px (design base): 100px
- Above 375px: 100px (capped) until the `md` breakpoint
- At `md`, base becomes `1440`, so 768px → ~53px and 1440px → 100px
- Above 1440px: 100px (capped)

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
<div class="grid col-gap-25 row-gap-25">...</div>
```

### Border Radius
```html
<div class="rounded-10">...</div>
<div class="rounded-t-20 rounded-b-10">...</div>
<div class="rounded-l-8 rounded-r-8">...</div>
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

Override `--window-width` in **your own** stylesheet, after the import — there's
no need to edit `src/plugin.css`. Set it once for mobile and once at `md`:

```css
@import "tailwindcss";
@import "tailwindcss-calc";

@layer theme {
  :root {
    --window-width: 390; /* your mobile artboard */
  }

  @variant md {
    :root {
      --window-width: 1920; /* your desktop artboard */
    }
  }
}
```

Match these to the artboard widths in your design file. Every utility
recalculates automatically — there is nothing else to configure.

### Use `@variant md`, not a raw media query

```css
/* ✅ mobile-first, matches the plugin */
@variant md {
  :root { --window-width: 1440; }
}

/* ❌ desktop-first, fights the plugin */
@media (max-width: 768px) {
  :root { --window-width: 375; }
}
```

`@variant md` inherits your theme's `--breakpoint-md`, so the two stay in sync
if you ever change it. A hard-coded `768px` drifts — and because `max-width:
768px` and `min-width: 48rem` both match at exactly `768px`, which one wins
comes down to source order rather than intent.

### Sizing vs. layout

Reach for `md:` variants only where the **layout** changes (a column becomes a
row, an element appears). Sizing is already handled by the base-width swap, so
`text-32` needs no `md:text-52` companion.

### One caveat worth knowing

Viewport-scaled font sizes ignore the reader's browser font-size preference.
Use the scaled `text-*` utilities for display type, headings and UI chrome —
where matching the mockup matters — and keep long-form body copy in `rem`.

You can also add new utilities following the same pattern:

```css
@utility custom-* {
  custom-property: calc(--value(integer) * var(--calc-ratio));
}
```

`--calc-ratio` already holds `clamp(0px, 100vw, var(--window-max-width)) /
var(--window-width)`, so reuse it rather than repeating the formula.

## 💡 Use Cases

Perfect for:
- **Fixed designs** that need to scale to different screen sizes
- **Design-to-code** workflows where you want pixel-perfect scaling
- **Responsive layouts** driven by a single breakpoint instead of a `md:`/`lg:`/`xl:` ladder
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

This project uses [changelogen](https://unjs.io/packages/changelogen) for automatic changelog generation, and a GitHub Action for npm publishing and GitHub releases.

**Publishing is handled entirely by CI.** The local release command only bumps the version, updates the changelog, and pushes the commit + tag. Pushing a `v*` tag triggers the workflow, which publishes to npm and creates the GitHub release. This keeps the npm token in GitHub secrets only — never on your machine.

### Release Workflow

1. **Make changes** following conventional commits
2. **Run the release command** — bumps version, updates `CHANGELOG.md`, commits `chore(release)`, creates the git tag, and pushes both to GitHub
3. **GitHub Action** (triggered by the `v*` tag) creates the GitHub release **and publishes to npm**

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

Locally (`bun run release` / `npm run release`):

1. ✅ Analyzes commits since last release
2. ✅ Determines version bump (semver)
3. ✅ Updates `CHANGELOG.md`
4. ✅ Updates version in `package.json`
5. ✅ Creates git commit `chore(release): vX.Y.Z`
6. ✅ Creates git tag (e.g., `v1.0.0`)
7. ✅ Pushes commit + tag to GitHub

Then, automatically in CI (on the pushed `v*` tag):

8. ✅ GitHub Action creates the GitHub release
9. ✅ GitHub Action publishes to npm (using the `NPM_TOKEN` secret)

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

Publishing runs in CI, so no local npm login is needed. You only need the token configured once in GitHub:

1. **Create npm account** at [npmjs.com](https://www.npmjs.com/)
2. **Create an Automation token** at [npmjs.com/settings/tokens](https://www.npmjs.com/settings/tokens) (type **Automation**, with publish access — a read-only token will fail with a 404)
3. **Add it as `NPM_TOKEN`** in GitHub → Settings → Secrets and variables → Actions

The committed `.npmrc` reads this via `${NODE_AUTH_TOKEN}`, which the workflow populates from the `NPM_TOKEN` secret.

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
