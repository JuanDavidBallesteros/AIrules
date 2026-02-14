# How to Read the Rules

This document explains how Cursor rules in `.cursor/rules/` are organized, how to find information, and **which rules take precedence** when they overlap.

---

## Rule precedence (most important)

**Framework- and technology-specific rules override general rules.**

When the same topic is covered in more than one rule file, follow the **more specific** one. The rule folder that matches your stack (e.g. `svelte/`, `ts/`, `python/`) takes precedence over the generic `architectures/`, `development/`, and—where implementation details differ—`UI_UX/`.

**Examples of the principle (not an exhaustive list):**

- **Architecture:** In a SvelteKit app, follow `svelte/sveltekit-architecture.mdc` over `architectures/feature-slicing.mdc` or `architectures/clean-architecture.mdc` where they conflict. In a Next.js app, prefer `ts/nextjs-app-router.mdc`; in FastAPI, prefer `python/fastapi-backend.mdc`.
- **Coding standards:** Use `development/general-coding.mdc` as the base; the framework folder (svelte, ts, python) adds or overrides for that stack.

**Summary:**  
**Specific (framework/subfolder) > General (architectures, development, UI_UX).**

---

## Where information is located

Rules are grouped by **folder**. Each folder has a **theme**; individual files are **topics** under that theme.

### By folder

| Folder | Theme | When to use |
|--------|--------|-------------|
| **`svelte/`** | Svelte 5, SvelteKit, Svelte UI/motion | Any `.svelte` or SvelteKit routes/lib code |
| **`ts/`** | TypeScript/React/Next.js | Next.js app router, React components |
| **`python/`** | Python/FastAPI | Backend API, `*.py`, `*.toml` |
| **`architectures/`** | Cross-stack architecture | Structure, layers, dependency direction, feature slicing |
| **`development/`** | Cross-stack dev practices | SOLID, naming, errors, testing |
| **`UI_UX/`** | Design system & visuals | Look & feel, motion, forms, a11y, layout (any frontend) |

### By topic (quick lookup)

| Topic | Primary location | Also relevant |
|-------|------------------|----------------|
| **Svelte 5 runes, props, snippets** | `svelte/svelte5-core.mdc` | `svelte/sveltekit-standards.mdc` |
| **SvelteKit load, actions, /lib** | `svelte/sveltekit-architecture.mdc` | `svelte/sveltekit-standards.mdc` |
| **Svelte UI & motion (transitions, Tailwind, a11y)** | `svelte/svelte-ui-motion.mdc` | `UI_UX/motion-physics.mdc`, `UI_UX/master-design.mdc` |
| **Next.js App Router, RSC, Server Actions** | `ts/nextjs-app-router.mdc` | — |
| **FastAPI structure, typing, async** | `python/fastapi-backend.mdc` | — |
| **Clean architecture, dependency rule** | `architectures/clean-architecture.mdc` | `architectures/feature-slicing.mdc` |
| **Feature-first / vertical slicing** | `architectures/feature-slicing.mdc` | `svelte/sveltekit-architecture.mdc`, `python/fastapi-backend.mdc` |
| **SOLID, naming, error handling** | `development/general-coding.mdc` | — |
| **Testing (AAA, mocking, F.I.R.S.T.)** | `development/testing.mdc` | — |
| **Design system (Kinetic Luxury)** | `UI_UX/master-design.mdc` | All other `UI_UX/*.mdc` |
| **Colors, glass, borders** | `UI_UX/visual-identity.mdc` | — |
| **Typography** | `UI_UX/typography.mdc` | — |
| **Layout, bento grid** | `UI_UX/layout-bento.mdc` | — |
| **Motion (hover, entrance, duration)** | `UI_UX/motion-physics.mdc` | `svelte/svelte-ui-motion.mdc` for Svelte |
| **Forms (inputs, validation)** | `UI_UX/forms.mdc` | — |
| **Accessibility & mobile** | `UI_UX/accessibility-mobile.mdc` | — |
| **Forbidden practices** | `UI_UX/anti-patterns.mdc` | — |

---

## How rules are applied (globs)

- Each rule file has a **`globs`** pattern in its frontmatter (e.g. `**/*.svelte`, `**/routes/**/*.ts`).
- A rule is **considered** when you have open (or in focus) files that match its globs.
- **Multiple rules can apply at once.** When they conflict, use the precedence rule above: **framework/subfolder over general.**

---

## File structure (reference)

```
.cursor/rules/
├── HOW-TO-READ-RULES.md          ← This file
├── architectures/
│   ├── clean-architecture.mdc
│   └── feature-slicing.mdc
├── development/
│   ├── general-coding.mdc
│   └── testing.mdc
├── python/
│   └── fastapi-backend.mdc
├── svelte/
│   ├── svelte5-core.mdc
│   ├── svelte-ui-motion.mdc
│   ├── sveltekit-architecture.mdc
│   └── sveltekit-standards.mdc
├── ts/
│   └── nextjs-app-router.mdc
└── UI_UX/
    ├── accessibility-mobile.mdc
    ├── anti-patterns.mdc
    ├── forms.mdc
    ├── layout-bento.mdc
    ├── master-design.mdc
    ├── motion-physics.mdc
    ├── typography.mdc
    └── visual-identity.mdc
```

---

## Summary

1. **Precedence:** Framework/subfolder rules (e.g. `svelte/`) override general rules (`architectures/`, `development/`, and `UI_UX/` where implementation conflicts).
2. **Finding rules:** Use the **By topic** table above, or open the folder that matches your stack (`svelte/`, `ts/`, `python/`) plus `architectures/`, `development/`, or `UI_UX/` as needed.
3. **Application:** Rules apply based on their `globs`; when in doubt, prefer the more specific rule for your framework or file type.
