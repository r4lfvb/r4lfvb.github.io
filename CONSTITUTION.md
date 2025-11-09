# Project Constitution

Date: 2025-11-05  
Domain: `ralfvb.com` (GitHub Pages custom domain)

This document is the stable charter for the personal single‑page site. It captures enduring principles, quality bars, and change governance. Tactical “how to prompt Copilot” rules live in `copilot-instructions.md`.

---
## 1. Mission
Provide a fast, elegant, accessible, zero‑build personal presence page with minimal maintenance overhead.

## 2. Scope & Non‑Goals
In Scope:
- Single HTML document + one CSS file (+ favicon, fonts, minor inline SVG assets).
- Tiny progressive enhancement JavaScript limited to theme toggling / light UX sugar.

Out of Scope / Non‑Goals:
- Client frameworks (React/Vue/etc.).
- Bundlers, transpilers, pipeline complexity.
- Tracking / analytics scripts.
- Heavy animation or canvas/WebGL flourishes.
- Server code or dynamic backends.

## 3. Design Principles
1. Clarity > cleverness (readable semantic HTML, descriptive class & aria labels).
2. Progressive enhancement: page fully usable without JavaScript.
3. Performance first: less bytes beats more features; limit network requests.
4. Accessibility is not optional (WCAG AA target for contrast & focus indicators).
5. Deterministic simplicity: no hidden build steps; source = deployed artifact.
6. Tokenized design: color, spacing, typography via CSS custom properties.
7. Consistent aesthetic: refined, quiet, minimal—avoid visual noise.

## 4. Architecture & Structure
Single layer with *content*, *presentation*, and *very light behavior* kept conceptually distinct:
- `index.html`: semantic structure + metadata.
- `styles.css`: design tokens, layout, state, responsive adjustments.
- Inline `<script>`: only feature: theme toggle (dark/light). Future JS must justify itself inline with a comment referencing this constitution (e.g., `// Allowed: progressive enhancement – reason:`).

### Layer Boundaries / Rules
- HTML must remain semantic (no purely decorative `<div>` wrappers without class purpose).
- JS MUST NOT block initial rendering (keep inline, tiny, after critical markup; no external JS files unless <2KB and well‑justified).
- Fonts may remain via Google Fonts for now; future optimization: self‑host to reduce third‑party reliance.

## 5. Performance Budgets
| Artifact | Budget (uncompressed) | Notes |
|----------|-----------------------|-------|
| `index.html` | ≤ 60 KB | Currently well below; avoid inline bloat. |
| `styles.css` | ≤ 35 KB | Keep cascade tidy; prune unused selectors. |
| JS (inline) | ≤ 4 KB | Only enhancement; no libraries. |
| Requests (initial) | ≤ 8 | HTML + CSS + favicon + fonts*. |

*Font count may be reduced later by trimming weights.

## 6. Accessibility Standards
- Visible focus always (custom ring already implemented).
- Provide `aria-label` where link text alone is ambiguous (e.g., icon-only future buttons).
- Maintain contrast ≥ 4.5:1 normal text, 3:1 large text.
- Respect `prefers-reduced-motion`: no essential info conveyed only via motion.
- Landmarks: keep primary content in `<main>`; navigation elements labeled.

## 7. Theming & Tokens
All theming defined in `:root` (+ `[data-theme]` overrides) using CSS custom properties. Allowed changes:
- Add new tokens only if reused ≥2 times.
- Dark theme parity required for new color tokens.
- No hard‑coded hex values outside token definitions (except temporary experimentation with a `TODO:` comment).

## 8. Security & Privacy
- No third‑party analytics or trackers.
- No inline user‑submitted content (XSS surface is effectively none—keep it that way).
- Avoid leaking unnecessary referrer data (use `rel="noopener noreferrer"` on external links — already enforced).

## 9. Governance / Change Process
| Change Type | Requirement |
|-------------|-------------|
| Content text tweak | Direct commit acceptable |
| Style token addition | Brief rationale in commit message |
| New JS feature | Justify with comment + keep under budget |
| Performance budget increase | Update table + rationale section |
| Constitution change | PR labeled `constitution-change` |

A constitution change should: (a) state the problem, (b) list options, (c) justify chosen adjustment.

## 10. Anti‑Patterns (Disallowed)
- Adding a framework or build system “just because”.
- Inlining large base64 images.
- Adding more than minimal JS state management (no global reactive systems).
- Excessive box‑shadows / layered glows that reduce legibility.
- Hard‑coding duplicated color literals instead of a token.

## 11. Future Considerations (Optional Backlog)
- Self‑host fonts (subsetting for smaller CLS + privacy).
- Add `link rel=preload` for critical font files if self‑hosted.
- Introduce automated HTML/CSS validation in CI (if CI is ever added).
- Generate a static screenshot preview image for social sharing (`og:image`).

## 12. Glossary
- Token: A named design variable (CSS custom property) controlling a visual primitive.
- Progressive Enhancement: Baseline experience functions without JS; JS enriches but is not required.
- Budget: A soft upper limit; exceeding must be explicitly justified.

## 13. CHANGELOG
- 2025-11-05: Initial constitution created.

---
Amend responsibly. Keep this file concise; high churn suggests misplaced content (move implementation details to `copilot-instructions.md`).
