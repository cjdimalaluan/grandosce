# UI/UX Cohesion Refactoring Guide

## Overview
This guide standardizes the **Grand OSCE Reviewer** project to achieve a cohesive, maintainable design system. All pages will share unified styling, consistent spacing, typography, and interactive patterns.

---

## ✅ Phase 1: Foundation (Complete)
**Global Stylesheet Created: `styles.css`**

### What's Included
- **Design Tokens**: CSS custom properties for colors, typography, spacing, and transitions
- **Component Library**: Reusable styles for buttons, badges, cards, grids, and layouts
- **Typography Scale**: Unified heading and body text styles
- **Responsive Grid System**: Mobile-first breakpoints
- **Utility Classes**: Quick styling helpers (spacing, text alignment, etc.)

---

## 📋 Phase 2: Index Page Refactoring (Ready to Start)

### Target: `index.html`
**Goal**: Remove all inline `<style>` block and replace with external stylesheet.

#### Steps:
1. **Remove** the `<style>...</style>` block (lines 8–496)
2. **Add** to `<head>`:
   ```html
   <link rel="stylesheet" href="styles.css" />
   ```
3. **Add page-specific overrides** in a new `<style>` block (only if needed):
   ```html
   <link rel="stylesheet" href="styles.css" />
   <style>
     /* Hero-specific customizations only */
     .hero { padding: 80px 52px 88px; }
     /* ... */
   </style>
   ```

#### Classes to Add/Rename
- `.main` → add `container` class
- `.grid` → add `grid grid--standard` classes
- Section headers already use correct naming

---

## 📋 Phase 3: Station Pages Refactoring (Ready to Start)

### Targets: All 14 station files
**Goal**: Normalize station page structure and styling.

#### Examples:
- `internal-medicine-1.html`
- `internal-medicine-2.html`
- `pediatrics-1.html`
- etc.

#### Steps per File:
1. **Remove** inline `<style>` blocks
2. **Link** `styles.css` in `<head>`
3. **Add** `container-narrow` class to `.content` div
4. **Replace button classes** with standardized `btn btn-primary`
5. **Update navigation buttons** with `btn btn-secondary`

#### Example Transformation:

**Before:**
```html
<div class="content">
  <button class="btn-done" id="markBtn">Mark as Reviewed</button>
  <a class="stn-btn" href="family-medicine.html">← Family Medicine</a>
</div>
```

**After:**
```html
<div class="content container-narrow">
  <button class="btn btn-primary" id="markBtn">Mark as Reviewed</button>
  <a class="btn btn-secondary" href="family-medicine.html">← Family Medicine</a>
</div>
```

---

## 🎨 Design System Reference

### Color Tokens
| Token | Value | Usage |
|-------|-------|-------|
| `--teal-deep` | #0c3d3d | Header/footer backgrounds |
| `--teal-mid` | #0e5252 | Secondary backgrounds |
| `--teal-bright` | #1a8c8c | Primary interactive states |
| `--teal-light` | #2ab8b8 | Accents, hover states |
| `--teal-pale` | #e6f4f4 | Light backgrounds, badges |
| `--green` | #0e6643 | Success states |
| `--ink` | #0c2a2a | Primary text |
| `--ink-soft` | #5a7878 | Secondary text |

### Spacing Scale
| Class | Value | Use Case |
|-------|-------|----------|
| `--sp-xs` | 4px | Micro spacing |
| `--sp-sm` | 8px | Tight spacing |
| `--sp-md` | 16px | Standard spacing |
| `--sp-lg` | 24px | Section spacing |
| `--sp-xl` | 32px | Large sections |
| `--sp-2xl` | 48px | Header/footer padding |
| `--sp-3xl` | 64px | Page padding |

### Typography
```css
/* Headings: Cormorant Garamond */
h1 { font-size: clamp(38px, 5vw, 90px); }
h2 { font-size: clamp(28px, 4vw, 56px); }
h3 { font-size: 15px; font-weight: 600; }

/* Body: Syne */
body { font-family: 'Syne', sans-serif; font-size: 13px; }

/* Mono: DM Mono */
.text-mono { font-family: 'DM Mono', monospace; }
```

---

## 🔄 Component Patterns

### Buttons
```html
<!-- Primary Action -->
<button class="btn btn-primary">Mark as Reviewed</button>

<!-- Secondary Action -->
<a class="btn btn-secondary" href="...">← Previous</a>

<!-- With Icon -->
<button class="btn btn-primary">
  <span id="icon">○</span>
  <span>Mark as Reviewed</span>
</button>

<!-- Active/Marked State -->
<button class="btn btn-primary marked">✓ Reviewed!</button>
```

### Cards
```html
<a class="card" href="...">
  <div class="card-top">
    <span class="card-num">01</span>
    <span class="card-arrow">↗</span>
  </div>
  <div class="card-title">Station Name</div>
  <div class="card-desc">Brief description...</div>
  <div class="card-footer">
    <span class="badge">Not started</span>
  </div>
</a>
```

### Grids
```html
<!-- Standard grid (290px min columns) -->
<div class="grid grid--standard">
  <div class="card">...</div>
  <!-- repeats -->
</div>

<!-- Compact grid (230px min columns) -->
<div class="grid grid--compact">
  <div class="tip">...</div>
  <!-- repeats -->
</div>
```

### Sections
```html
<div class="section-header">
  <span class="section-label">Section Title</span>
  <div class="section-rule"></div>
</div>
```

---

## 📱 Responsive Breakpoints

### Mobile-First Approach
```css
/* Default: mobile (< 640px) */
/* Tablet: 640px - 768px */
/* Desktop: 768px+ */
```

### Key Changes at Breakpoints
- **640px**: Increased padding, larger text
- **768px**: Grid columns adjust, container widths update

---

## ✨ Best Practices

### DOs
✅ Use CSS custom properties for all values  
✅ Apply utility classes for spacing (`mt-lg`, `mb-md`)  
✅ Keep component markup semantic  
✅ Test across mobile, tablet, desktop  
✅ Use `clamp()` for responsive typography  

### DON'Ts
❌ Add inline `style` attributes  
❌ Duplicate color values; use tokens instead  
❌ Use magic numbers; prefer spacing scale  
❌ Break component structure for visual changes  
❌ Hardcode media query values  

---

## 📊 Refactoring Checklist

### Files to Update
- [ ] `index.html` - Main landing page
- [ ] `internal-medicine-1.html` - Station 02
- [ ] `internal-medicine-2.html` - Station 03
- [ ] `pediatrics-1.html` - Station 04
- [ ] `pediatrics-2.html` - Station 05
- [ ] `obgyn-1.html` - Station 06
- [ ] `obgyn-2.html` - Station 07
- [ ] `surgery-1.html` - Station 08 *(if exists)*
- [ ] `surgery-2.html` - Station 09 *(if exists)*
- [ ] `orl.html` - Station 10
- [ ] `psychiatry.html` - Station 11
- [ ] `msk.html` - Station 12
- [ ] `neurology.html` - Station 13
- [ ] `ophthalmology.html` - Station 14

### Per-File Checklist
For each HTML file:
- [ ] Remove inline `<style>` block
- [ ] Add `<link rel="stylesheet" href="styles.css" />`
- [ ] Add `.container` or `.container-narrow` wrapper
- [ ] Update button classes: `btn btn-primary` / `btn btn-secondary`
- [ ] Update badge/pill classes if needed
- [ ] Test responsive layout at 640px, 768px
- [ ] Verify all interactive states (hover, active, marked)
- [ ] Check spacing consistency against scale
- [ ] Validate font loading and fallbacks

---

## 🚀 Implementation Timeline

| Phase | Tasks | Estimated Time |
|-------|-------|-----------------|
| **1** | ✅ Global stylesheet (`styles.css`) | Done |
| **2** | Refactor `index.html` | 30 min |
| **3** | Refactor station pages (14 files) | 2-3 hours |
| **4** | Cross-browser testing | 1 hour |
| **5** | Documentation & final QA | 1 hour |

---

## 🔍 Quality Assurance

### Testing Checklist
1. **Visual Consistency**
   - [ ] Colors match design tokens
   - [ ] Spacing follows scale
   - [ ] Typography is consistent

2. **Responsiveness**
   - [ ] Mobile (< 640px): Single-column layout
   - [ ] Tablet (640-768px): Transitional layout
   - [ ] Desktop (768px+): Full grid layout

3. **Interactivity**
   - [ ] Hover states work smoothly
   - [ ] Button transitions feel polished
   - [ ] Progress bar animates correctly
   - [ ] LocalStorage persistence works

4. **Accessibility**
   - [ ] Color contrast meets WCAG AA
   - [ ] Links are keyboard-navigable
   - [ ] Focus states are visible

---

## 📚 Resources

- **Design Tokens**: See `:root` in `styles.css`
- **Component Examples**: See "Component Patterns" section above
- **Google Fonts Used**:
  - Cormorant Garamond (Display)
  - Syne (Body)
  - DM Mono (Code/Mono)

---

## Notes

- All inline styles have been analyzed and converted to reusable classes
- The global stylesheet is framework-agnostic (pure CSS)
- Future enhancement: Consider SCSS/SASS for nesting and mixins
- All existing functionality is preserved; this is styling-only refactoring

