# Copilot Instructions

Goal: Provide concise, actionable rules so AI suggestions stay faithful to the site’s philosophy (see `CONSTITUTION.md` for rationale). Keep this file practical; prune if it grows noisy.

---
## 1. Context Snapshot
- Project type: Single static HTML page + one CSS file + tiny inline JS (theme toggle only).
- No build system; source files are deployable as-is.
- Design language: minimal, soft glass card, token-driven theming, light/dark modes.

When generating or refactoring code, **do not introduce frameworks or tooling**.

## 2. HTML Authoring Rules
- Use semantic elements (`main`, `nav`, `header`, etc.).
- Every new interactive element must be keyboard accessible and get an accessible name (visible text or `aria-label`).
- Avoid unnecessary wrapper `<div>` elements; prefer meaningful structure.
- If adding an external link that opens a new tab: include `rel="noopener noreferrer"`.
- Keep icon SVGs inline (they inherit `currentColor`).

### Example: Adding a Mastodon Link Button
BAD:
```html
<a href="https://mastodon.social/@ralf">M</a>
```
GOOD:
```html
<a class="btn btn--mastodon" href="https://mastodon.social/@ralf" target="_blank" rel="noopener noreferrer" aria-label="Mastodon profile (opens in new tab)">
  <span class="btn__icon" aria-hidden="true">(svg here)</span>
  <span class="btn__text">Mastodon</span>
</a>
```

## 3. CSS Rules
- Define new visual values as CSS custom properties in `:root` (and dark variant) if reused ≥ 2 times.
- No hard-coded color literals inside component selectors (except temporary prototyping with a `/* TODO:tokenize */` comment).
- Maintain existing naming style: utilities or variations use double-hyphen (e.g., `btn--linkedin`).
- Ensure dark theme parity for any new color token.
- Prefer transitions that respect `prefers-reduced-motion`; don’t add complex animations.

### Example: New Accent Border Token
```css
:root { --color-border-accent-2: #c08bfa; }
:root[data-theme="dark"] { --color-border-accent-2: #b78bf9; }
```

## 4. JavaScript Rules
- Only author tiny, self-contained progressive enhancements.
- No external libraries, build steps, or large utility abstractions.
- MUST NOT block first paint (already inline at document end). Don’t move it to head.
- If adding logic: wrap in an IIFE or minimal block comment with rationale.

### Example Snippet for New Enhancement (Copy Pattern)
```html
<script>
// Enhancement: subtle prefers-color-scheme sync clarification (optional)
(() => {
  // Keep under 20 lines; bail out fast.
})();
</script>
```

## 5. Performance Guardrails
- Avoid adding more HTTP requests (sprites or base64 small inline SVG for icons is fine; no large images unless explicitly justified with a comment and measured size).
- Don’t embed large data URIs.
- Reuse existing typography (avoid adding more font weights or families without justification).

## 6. Accessibility Prompts
When unclear, ask Copilot:
> “Ensure WCAG AA contrast and keyboard operability for any new interactive element.”

Checklist for each new element:
- Focus visible?  (The global focus ring should appear.)
- Contrast meets thresholds?  (Use existing token palette.)
- Has an accessible name? (Text or aria-label.)

## 7. Commit Message Style (For Automated Suggestions)
- Imperative present tense: “Add Mastodon button” / “Refactor theme toggle state handling”.
- If exceeding a budget: “Increase CSS budget to 36KB (adds high contrast variant)”.

## 8. Prompt Snippets (Reuse These)
- “Refactor the open HTML to reduce unnecessary wrappers; preserve semantics.”
- “Generate a new social button following existing button class pattern and accessible naming.”
- “Suggest a minimal enhancement for X without introducing build tooling.”
- “List any tokens referenced fewer than 2 times for pruning.”

## 9. Negative Instructions (Do NOT Do These)
- Do NOT add React/Vue/Svelte/etc.
- Do NOT add a bundler (Vite/Webpack/Rollup) or package manager manifest.
- Do NOT introduce analytics scripts.
- Do NOT exceed JS size budget; prefer CSS where possible.

## 10. Quick Heuristics Copilot Should Imitate
| Area | Heuristic |
|------|-----------|
| Class naming | `block__element--modifier` (loose BEM hybrid) & `btn--platform` variants |
| Tokens | All theme-specific values originate in root token sets |
| Focus styling | Always rely on existing `:focus-visible` ring; don’t override locally |
| SVG icons | Inline, inherit `currentColor`, sized by parent | 
| JS style | Small functions, no global vars, early return patterns |

## 11. Housekeeping Tasks (Safe for Automation)
- Sort root CSS custom properties alphabetically (while preserving grouped logical blocks) if they drift.
- Identify and remove unused button variant classes.
- Flag duplicate hard-coded colors for tokenization.

## 12. If a Rule Must Be Broken
Add an inline comment: `/* exception: reason + date (YYYY-MM-DD) */` and (optionally) open a cleanup issue.

## 13. CHANGELOG
- 2025-11-05: Initial instructions file created.

---
Keep this under ~400 lines. Remove stale sections when obsolete to maintain high signal density.
