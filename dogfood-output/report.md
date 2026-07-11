# Dogfood QA Report — manar.oversight.ee

**Target:** http://manar.oversight.ee
**Date:** 2026-07-11
**Scope:** Full site audit — navigation, asset integrity, page rendering
**Original Source:** wget mirror of manar.com.sa (WordPress + Elementor + Smart Slider 3)

---

## Executive Summary

| Severity | Count |
|----------|-------|
| 🔴 Critical | 0 |
| 🟠 High | 0 |
| 🟡 Medium | 0 |
| 🔵 Low | 0 |
| **Total** | **0** |

**Assessment:** Site is fully functional. All pages serve 200, all assets (45 CSS, 45 JS, 158 images) serve locally with no dependencies on the original server.

---

## Issues Resolved During Setup

| Issue | Fix |
|-------|-----|
| All assets pointed to `https://manar.com.sa/` | Rewritten to root-relative paths |
| Navigation links pointed to `https://manar-alomran.smart-media.agency/` | Rewritten to root-relative paths |
| wget appended `.css` to files with query strings (`file.css?ver=123.css`) | Renamed to correct filenames |
| `?ver=` and `&wpr_t=` query params in filenames | Stripped (files renamed, HTML references kept with query strings — server ignores them) |
| Cache-bg CSS paths contained `manar.com.sa` in directory name | Files kept as-is (structured mirrors original), HTML references fixed |
| No CNAME or deploy workflow | Added `.github/workflows/pages.yml` + `CNAME` |
| Corrupted HTML from aggressive regex | Restored from clean commit |

---

## Testing Coverage

### Pages Tested (all 200)
- Homepage (`/`)
- About Us (`/about-us/`)
- Our Services (`/our-services/`)
- Our Products (`/our-products/`)
- Contact Us (`/contact-us/`)
- Certifications (`/certifications/`)
- Media Center (`/media-center/`)
- Product sub-pages: formwork, scaffolding, heavy-duty formwork, insulation, system components

### Assets Verified (all 200)
- Elementor CSS + JS
- Smart Slider 3 CSS + JS
- jQuery
- Font Awesome
- Astra theme CSS
- Google Fonts (external, 200)
- All product/project images
- Logo and favicon

### Remaining External Links (expected)
- Google Maps (office locations) — intentional
- Google Fonts CDN — intentional

### WordPress API Endpoints (return 404, expected for static)
- `feed/`, `comments/feed/`, `wp-json/` — no backend available

---

## Git Repository

**Remote:** `github.com/ahmdngi/manar.oversight.ee`
**Local:** `~/git-repos-personal/manar.oversight.ee`
**Files:** 253 files, ~46MB
**Deploy:** GitHub Actions → GitHub Pages at `http://manar.oversight.ee/`
**CNAME:** `manar.oversight.ee` → `ahmdngi.github.io.`
