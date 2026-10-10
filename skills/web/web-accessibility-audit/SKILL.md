---
name: web-accessibility-audit
description: Comprehensive WCAG 2.2 AA accessibility auditor for Next.js, React, and HTML/CSS. Analyzes contrast ratios, keyboard accessibility, semantic landmarks, and ARIA compliance.
version: 1.0.0
metadata:
  category: web
  tags: [accessibility, a11y, wcag, react, nextjs, frontend, ui-ux]
---

# Web Accessibility (a11y) & WCAG 2.2 Audit ♿🔍

## 📐 Core WCAG 2.2 AA Standards Checklist

1. **Color Contrast (Criterion 1.4.3 & 1.4.11):**
   * Normal text (< 18pt / 24px): Minimum **4.5:1** contrast ratio against background.
   * Large text (>= 18pt or 14pt bold): Minimum **3:1** contrast ratio.
   * UI components and graphical objects: Minimum **3:1** contrast ratio.
2. **Keyboard Accessibility (Criterion 2.1.1 & 2.4.7):**
   * All interactive elements (`<button>`, `<a>`, `<input>`) must be operable via Tab/Enter/Space.
   * Never set `outline: none` without providing an explicit `:focus-visible` alternative.
3. **Semantic Landmarks & ARIA (Criterion 1.3.1):**
   * Use `<main>`, `<nav>`, `<header>`, `<footer>`, `<aside>`. Avoid `<div>` soup.
   * Icon buttons with no text must have an `aria-label` or `aria-labelledby`.
4. **Form Controls (Criterion 3.3.2):**
   * Every `<input>` must have an associated `<label htmlFor="...">` or `aria-label`.

---

## 🛠️ Contrast Ratio Formula & Python Auditor

```python
def relative_luminance(r, g, b):
    # sRGB to linear RGB conversion
    def adjust(c):
        c = c / 255.0
        return c / 12.92 if c <= 0.03928 else ((c + 0.055) / 1.055) ** 2.4
    return 0.2126 * adjust(r) + 0.7152 * adjust(g) + 0.0722 * adjust(b)

def contrast_ratio(rgb1, rgb2):
    l1 = relative_luminance(*rgb1)
    l2 = relative_luminance(*rgb2)
    lighter = max(l1, l2)
    darker = min(l1, l2)
    return (lighter + 0.05) / (darker + 0.05)

# Example: #818cf8 (text) on #0d1117 (dark background)
text_color = (129, 140, 248)
bg_color = (13, 17, 23)
ratio = contrast_ratio(text_color, bg_color)
print(f"Contrast Ratio: {ratio:.2f}:1 -> {'PASS (WCAG AA)' if ratio >= 4.5 else 'FAIL'}")
```
