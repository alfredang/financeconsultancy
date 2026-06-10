# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A single-file marketing landing page for an investment-strategy consultancy ("FinanceGuru"). The entire site — HTML, CSS, and JS — lives in [index.html](index.html). There is no build step, package manager, framework, or test suite. Open the file in a browser (or serve the directory with any static server, e.g. `python -m http.server`) to view changes.

## Architecture

[index.html](index.html) is organized top-to-bottom in three blocks, each marked with `=====` comment banners:

1. **`<style>`** — all CSS. Starts with a `:root` design-token block (colors, shadows, radii, `--nav-h`, `--ease`); every section thereafter references those tokens. Responsive rules live in two `@media` queries (`980px`, `760px`) at the bottom.
2. **`<body>`** — page sections in order: nav, hero, why, process, testimonials, lead-magnet, enquiry (form), faq, final-cta, footer. Sections are linked by `id` and navigated via `#`-anchor smooth scrolling.
3. **`<script>`** — one IIFE handling sticky nav, mobile menu toggle, smooth scroll, FAQ accordion, scroll-reveal (IntersectionObserver), form validation, and footer year.

### Things worth knowing before editing

- **Form submission** posts to FormSubmit (`https://formsubmit.co/angch@tertiaryinfotech.com`) — a third-party service that emails form contents. The `_subject`, `_captcha`, `_template` hidden inputs configure it. The same email/phone appear in the footer contact block; keep them in sync if changed.
- **Form field names contain spaces** (e.g. `name="Full Name"`) so they render nicely in the FormSubmit email. Because of this, the JS reassigns `form.name`/`form.email`/`form.phone` to the actual elements *by id* (`getElementById`) before validating — don't rely on `form.elements` name lookups for these.
- **Validation is client-side only** and non-blocking on success: valid submits fall through to the native FormSubmit POST. Email/phone use the `emailRe`/`phoneRe` regexes plus a digit-count check for phone.
- **Scroll-reveal** depends on the `reveal` class plus the IntersectionObserver adding `visible`. New animated sections need the `reveal` class or they'll stay at `opacity: 0`. A `prefers-reduced-motion` query disables reveals/animation.
- **Nav scroll offset** is hardcoded to `72` in the smooth-scroll JS, matching `--nav-h: 72px`. Change both together.
