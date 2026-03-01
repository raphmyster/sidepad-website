# Sidepad Website Design

## Goal

Build a static marketing site for the Sidepad Chrome extension at `sidepad.app`. Serves two purposes: (1) marketing landing page to drive Chrome Web Store installs, and (2) host the privacy policy and terms of use required for Chrome Web Store submission.

## Decisions

- **Stack:** Plain HTML + Tailwind CSS, no JS framework
- **Hosting:** GitHub Pages with custom domain (`sidepad.app`)
- **Structure:** Hybrid — single-scroll landing page + separate privacy and terms pages
- **Visual style:** Extension's color palette extended with marketing-specific tokens

## File Structure

```
Sidepad-Website/
├── index.html            # Marketing landing page
├── privacy.html          # Privacy policy
├── terms.html            # Terms of use
├── input.css             # Tailwind source (imports + custom tokens)
├── dist/
│   └── output.css        # Built Tailwind CSS
├── assets/
│   ├── logo.png          # From extension assets
│   ├── screenshot-*.png  # Extension screenshots
│   └── favicon.ico
├── tailwind.config.js
├── package.json          # npm run build:css
└── CNAME                 # sidepad.app
```

## Color System

### Base tokens (from extension)

| Token | Value | Usage |
|---|---|---|
| `--color-bg` | `#ffffff` | Page background |
| `--color-bg-subtle` | `#f5f6f8` | Alternating section backgrounds |
| `--color-border` | `#e2e4e8` | Borders, dividers |
| `--color-text` | `#2b2b2b` | Body text |
| `--color-text-secondary` | `#4a5d73` | Subtext, descriptions |
| `--color-text-tertiary` | `#8a95a3` | Captions, fine print |
| `--color-primary` | `#374759` | Headings, nav links |
| `--color-accent` | `#d4952b` | Small highlights only (not buttons or major UI) |
| `--color-accent-bg` | `#fef7ed` | Accent background areas |

### Marketing additions

| Token | Value | Usage |
|---|---|---|
| `--color-hero-bg` | `#f8f9fb` | Hero section background |
| `--color-cta` | `#374759` | "Add to Chrome" button (navy) |
| `--color-cta-hover` | `#2a3644` | CTA hover state (darker navy) |
| `--color-cta-text` | `#ffffff` | Button text on CTA |
| `--color-feature-icon` | `#4a5d73` | Feature card icon/accent |

Amber (`#d4952b`) is reserved for very small highlights only — not for buttons, CTAs, or major interactive elements.

## Landing Page Layout (index.html)

### 1. Header (sticky)
- Logo (left) + nav links: Features, Privacy, Terms
- "Add to Chrome" CTA button (right)
- White background, subtle bottom border on scroll

### 2. Hero
- Bold headline (e.g., "Capture and compose from anywhere on the web")
- One-liner subtext explaining what Sidepad does
- "Add to Chrome" CTA button
- Browser mockup screenshot showing the side panel in action

### 3. Features (4 cards or alternating rows)
- **Capture from any page** — highlight text, send to Sidepad with keyboard shortcut or right-click
- **Structured Markdown documents** — organize captures with headers, notes, annotations
- **Local-first** — files saved to your computer, no cloud, no account
- **Works with LLMs** — designed for ChatGPT, Claude, Gemini conversations

### 4. How It Works (3-step visual)
- Capture → Organize → Save as `.md`

### 5. Footer
- Links: Privacy Policy, Terms of Use
- Copyright notice
- Tagline (e.g., "Built for researchers, writers, and thinkers")

## Privacy Policy (privacy.html)

Clean text page with shared header/footer.

Key points:
- **No data collection** — no user data transmitted to external servers
- **Local storage only** — documents stored on user's device via `chrome.storage.local` and File System Access API
- **No analytics or tracking** — no cookies, telemetry, or third-party scripts
- **No accounts** — no sign-up or authentication
- **Permissions explained** — brief justification for each Chrome permission
- **Data deletion** — uninstall the extension or delete files from chosen folder
- **Contact:** support@sidepad.app

## Terms of Use (terms.html)

Clean text page with shared header/footer.

Key points:
- Extension provided "as is" with no warranty
- User responsible for their own content/files
- Terms and extension may be updated
- Governing jurisdiction
- Contact: support@sidepad.app

## Deployment

- GitHub Pages serving from `main` branch root
- Custom domain via `CNAME` file + DNS (A records to GitHub IPs, CNAME for `www`)
- HTTPS automatic (GitHub Pages + `.app` HSTS)
- Build: `npm run build:css` generates `dist/output.css` — committed to repo (no CI needed)

## Out of Scope

- Dark mode
- Blog or changelog
- JavaScript interactions beyond smooth scroll
- CMS or dynamic content
- Analytics (can add later if desired)
