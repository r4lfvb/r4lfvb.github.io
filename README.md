# Ralf – Personal Single Page

Minimal single‑page personal contact card implemented with **only HTML & CSS**.

## Overview

The page presents a centered, responsive “card” featuring the name, a concise tagline, and quick links to LinkedIn & GitHub. The aesthetic blends quiet Scandinavian restraint with subtle Art‑Deco typography cues—now in a pared‑back, airy style (no heavy ornamentation). Light and dark themes follow the user’s system preference via `prefers-color-scheme`.

## Current Design Characteristics

- Glassy, soft card (backdrop blur) with gentle mint background gradient.
- Accent color (currently `--color-accent: #ff8eea`) used for interactive emphasis & focus ring.
- Large display type (Yeseva One) + clean sans‑serif body (Raleway).
- Minimal pill outline buttons with inline official SVG icons (LinkedIn & GitHub).
- No JavaScript, no build tooling—pure static assets.
- Accessible focus styles, semantic landmarks, and descriptive link labels.

## File Structure

```text
index.html   # Markup, metadata, font preconnect + links
styles.css   # Theme tokens, layout, responsive & state styles
```

## Theming & Tokens

All primary design knobs live in `:root` (and dark-mode overrides). Adjust to suit your taste:

| Variable | Purpose |
|----------|---------|
| `--font-display` | Display font for the name heading |
| `--font-sans` | Body / UI text font stack |
| `--color-bg` | Base background (light) |
| `--color-bg-accent` | Subtle gradient partner tone |
| `--color-card` | Card surface (semi‑transparent) |
| `--color-border` | Subtle outline / divider base |
| `--color-border-strong` | Higher contrast accent border |
| `--color-text` | Primary text color |
| `--color-text-muted` | Secondary / tagline text |
| `--color-accent` | Interactive + focus highlight (change here to revert to neon yellow if desired) |
| `--shadow` | Card elevation shadow recipe |
| `--focus-ring` | Composite focus ring shadow |

## Accessibility Notes

- Landmarks: `<main>` + `<nav>` + ARIA labels provide assistive clarity.
- Focus Visibility: Custom accessible ring (`--focus-ring`) instead of relying on browser default.
- Color Contrast: Body & button label colors chosen to exceed WCAG AA for large text; verify if you alter tokens.
- Reduced Motion: Respects `prefers-reduced-motion` (transitions stripped).

## Deployment

Serve the repository root via any static host (e.g., GitHub Pages). With GitHub Pages (user/organization site):

1. Push to the `main` (or `master`) branch of the `username.github.io` repo.
2. Pages auto-builds—visit `https://<username>.github.io/`.

No build, bundler, or pipeline required.

## Project Documentation

This repository includes two governance / guidance documents:

| File | Purpose |
|------|---------|
| `CONSTITUTION.md` | Stable charter: mission, principles, performance & accessibility budgets, change rules. |
| `copilot-instructions.md` | Actionable rules & examples for consistent AI‑assisted edits (HTML/CSS/JS heuristics). |

When making non‑trivial changes, skim `CONSTITUTION.md` first. When using GitHub Copilot Chat, you can reference these files explicitly (e.g., “Apply performance budgets from CONSTITUTION.md”).