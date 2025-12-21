# Example - Tailwind CSS v4 Calc Plugin

This example demonstrates all the responsive utilities available in the plugin.

## 🚀 Running the Example

From the project root:

```bash
npm run dev
```

Or from this directory:

```bash
bun dev
```

Then open your browser at `http://localhost:5173`

## 📖 What's Included

The example demonstrates:

### 1. Responsive Width & Height
```html
<div class="w-100 h-200">100x200 (scales with viewport)</div>
<div class="size-150">150x150 square</div>
```

### 2. Responsive Spacing
```html
<div class="p-20 m-10">Padding 20, Margin 10</div>
<div class="px-30 py-40">Horizontal 30, Vertical 40</div>
```

### 3. Responsive Typography
```html
<h1 class="text-48 leading-60">48px font size, 60px line height</h1>
<p class="text-16 tracking-1">16px with letter spacing</p>
```

### 4. Layout Utilities
```html
<div class="flex gap-20">Flex with 20px gap</div>
<div class="grid gap-x-30 gap-y-40">Grid with custom gaps</div>
```

### 5. Positioning
```html
<div class="absolute top-50 left-100">Positioned element</div>
<div class="relative inset-20">Inset on all sides</div>
```

### 6. Transforms
```html
<div class="translate-x-50">Translate X by 50</div>
<div class="translate-y-100">Translate Y by 100</div>
```

### 7. Borders & Radius
```html
<div class="rounded-10 border-w-2">Rounded with border</div>
```

## 🎨 How to Use in Your Project

### Step 1: Import the plugin

In your CSS file:

```css
@import "tailwindcss";
@import "../src/plugin.css";
```

### Step 2: Use the utilities

```html
<div class="w-500 h-300 p-20 m-10">
  <h1 class="text-32 mb-20">Hello World</h1>
  <p class="text-16 leading-24">Content here</p>
</div>
```

### Step 3: Customize (optional)

Edit `src/plugin.css` to change the base width:

```css
@theme {
  --window-width: 1920;  /* Your design's base width */
  --window-max-width: var(--window-width) * 1px;
}
```

## 💡 Understanding the Values

When you use `w-100`, it means:
- **Design value**: 100px at the base width (default 1920px)
- **Actual size**: Scales proportionally to viewport width
- **Maximum**: Capped at base width (doesn't grow infinitely)

Example with default settings (base: 1920px):
- Mobile (375px): `100 * (375 / 1920) = ~19.5px`
- Tablet (768px): `100 * (768 / 1920) = ~40px`
- Desktop (1440px): `100 * (1440 / 1920) = ~75px`
- Large (1920px): `100 * (1920 / 1920) = 100px`
- Ultra-wide (>1920px): `100px` (capped at base width)

## 🔧 Tips

### Use with Standard Tailwind Classes

You can mix these utilities with standard Tailwind:

```html
<div class="w-500 bg-blue-500 rounded-lg shadow-xl hover:scale-105">
  Combines calc-based width with standard utilities
</div>
```

### Combine Utilities

```html
<div class="w-800 max-w-full mx-auto p-40">
  Responsive width with max-width fallback and auto margins
</div>
```

### Typography Scaling

```html
<h1 class="text-48 leading-60 tracking-2">
  Complete typography control
</h1>
```

## 📝 Notes

- All utilities are **viewport-responsive** by default
- Values represent pixels at the base width
- Uses `clamp()` to prevent growing beyond base width
- Works seamlessly with standard Tailwind utilities
- No JavaScript required - pure CSS
- Compatible with Tailwind CSS v4

## 🎯 Best Practices

1. **Use consistent base width** - Match your design's reference width
2. **Test on multiple screens** - Check how it scales
3. **Mix with standard utilities** - Use calc utilities for layout, standard for colors/effects
4. **Set max-width when needed** - Prevent elements from growing too large
5. **Use container utility** - For centered page layouts

## 📱 Responsive Behavior

The plugin scales automatically based on viewport width:

```
Mobile (320-480px)   → 16-25% of original size
Tablet (768-1024px)  → 40-53% of original size
Desktop (1440-1920px) → 75-100% of original size
Ultra-wide (>1920px) → 100% of original size (capped)
```

## 🚀 Performance

- **Zero runtime cost** - Pure CSS, no JavaScript
- **No build overhead** - Standard Tailwind compilation
- **Optimal caching** - Static CSS output
- **Small bundle** - Only includes used utilities

## 🤝 Need Help?

Check the main README for more details or open an issue on GitHub.
