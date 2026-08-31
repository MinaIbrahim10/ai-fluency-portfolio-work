# Open It on Your Phone

## Live Portfolio

https://minaibrahim.tech

## Real-Phone Check

I opened and tested the updated portfolio on a real phone after deployment.

I checked the page from top to bottom, including the hero, project sections, TensorFlow/open-source content, research section, skills, experience, contact form, and footer.

The updated mobile version looked correct after the fixes.

## Fix Log

### 1. Small Mobile Text

**Before:**
Some metadata and supporting text used very small font sizes, including 6px, 7px, 8px, and 9px text in technical sections.

**Problem:**
The layout was responsive, but some supporting text was harder to read comfortably on a phone.

**After:**
I increased the minimum mobile font size for metadata and technical labels while keeping the same visual hierarchy and design style.

---

### 2. Small Link Tap Targets

**Before:**
Some secondary text links and technical links had small visual and interactive areas.

**Problem:**
Small targets can be harder to tap accurately on a touchscreen.

**After:**
I added a minimum 44px interaction height to small standalone links and added mobile padding where needed.

---

### 3. Keyboard Focus Visibility

**Before:**
Interactive elements did not have a dedicated visible `:focus-visible` style.

**Problem:**
Keyboard users could have difficulty seeing which link, button, or form field was currently focused.

**After:**
I added visible focus outlines to links, buttons, inputs, and textareas.

---

### 4. Image and Asset Size Check

I checked the main portfolio assets for obvious size problems.

- Profile image: approximately 134 KB
- CV PDF: approximately 81 KB
- Open Graph image: approximately 41 KB

These were already reasonably sized, so I did not compress them unnecessarily.

## Responsive Review

The portfolio already had responsive breakpoints for mobile, tablet, and desktop.

For this audit I verified that:

- the mobile layout does not visibly break
- text remains readable
- buttons and links are tappable
- the contact form fits the mobile width
- project and technical sections stay within the viewport
- the main image remains crisp
- the page works correctly on a real phone

## Result

The live portfolio now has improved mobile readability, better touch targets, and clearer keyboard focus behavior while preserving the existing design.

Updated live URL:

https://minaibrahim.tech
