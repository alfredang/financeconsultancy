# FinanceGuru

A single-file marketing landing page for an investment-strategy consultancy. The entire site — HTML, CSS, and JavaScript — lives in [index.html](index.html). No build step, package manager, framework, or dependencies.

![Screenshot of the FinanceGuru landing page](screenshot.png)

## Getting started

Open [index.html](index.html) directly in a browser, or serve the directory with any static server:

```bash
python -m http.server
```

Then visit http://localhost:8000.

## Structure

[index.html](index.html) is organized top-to-bottom in three blocks:

1. **`<style>`** — all CSS, starting with a `:root` design-token block (colors, shadows, radii, spacing). Responsive rules live in two `@media` queries (`980px`, `760px`).
2. **`<body>`** — page sections in order: nav, hero, why, process, testimonials, lead-magnet, enquiry form, FAQ, final CTA, footer. Sections link by `id` and navigate via `#`-anchor smooth scrolling.
3. **`<script>`** — one IIFE handling sticky nav, mobile menu toggle, smooth scroll, FAQ accordion, scroll-reveal (IntersectionObserver), form validation, and the footer year.

## Contact form

The enquiry form posts to [FormSubmit](https://formsubmit.co), which emails the submitted contents. Validation is client-side only; valid submissions fall through to the native FormSubmit POST.

## Deployment

The site is deployed to GitHub Pages via a GitHub Actions workflow on every push to `main`.
