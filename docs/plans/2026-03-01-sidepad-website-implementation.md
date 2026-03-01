# Sidepad Website Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a static marketing site at `sidepad.app` with a landing page, privacy policy, and terms of use for Chrome Web Store submission.

**Architecture:** Three static HTML files sharing a Tailwind CSS build. No JS framework. Hosted on GitHub Pages with a custom domain.

**Tech Stack:** HTML, Tailwind CSS 4 (via `@tailwindcss/cli`), GitHub Pages

**Working Directory:** `/Users/raph/Developer/Projects/Sidepad-Website`

---

### Task 1: Project Scaffolding

**Files:**
- Create: `package.json`
- Create: `input.css`
- Create: `CNAME`
- Create: `.gitignore`

**Step 1: Initialize git repo**

Run: `cd /Users/raph/Developer/Projects/Sidepad-Website && git init`

**Step 2: Create package.json**

```json
{
  "name": "sidepad-website",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "build:css": "npx @tailwindcss/cli -i input.css -o dist/output.css --minify",
    "dev": "npx @tailwindcss/cli -i input.css -o dist/output.css --watch"
  }
}
```

**Step 3: Create input.css with color tokens**

```css
@import "tailwindcss";

@theme {
  --color-surface: #ffffff;
  --color-surface-subtle: #f5f6f8;
  --color-border-color: #e2e4e8;
  --color-foreground: #2b2b2b;
  --color-foreground-secondary: #4a5d73;
  --color-foreground-tertiary: #8a95a3;
  --color-primary: #374759;
  --color-primary-hover: #2a3644;
  --color-accent: #d4952b;
  --color-accent-bg: #fef7ed;
  --color-hero-bg: #f8f9fb;
  --color-cta: #374759;
  --color-cta-hover: #2a3644;
  --color-feature-icon: #4a5d73;
}
```

**Step 4: Create CNAME**

```
sidepad.app
```

**Step 5: Create .gitignore**

```
node_modules/
.DS_Store
```

**Step 6: Install Tailwind and build CSS**

Run: `cd /Users/raph/Developer/Projects/Sidepad-Website && npm install tailwindcss @tailwindcss/cli --save-dev && npm run build:css`

**Step 7: Commit**

```bash
git add package.json input.css CNAME .gitignore package-lock.json dist/
git commit -m "chore: scaffold project with Tailwind CSS 4"
```

---

### Task 2: Copy Brand Assets

**Files:**
- Create: `assets/logo.png`
- Create: `assets/screenshot.png`

**Step 1: Create assets directory and copy files**

```bash
mkdir -p /Users/raph/Developer/Projects/Sidepad-Website/assets
cp "/Users/raph/Developer/Projects/Sidepad/assets/logo-clean-high-quality-cropped.png" /Users/raph/Developer/Projects/Sidepad-Website/assets/logo.png
cp "/Users/raph/Developer/Projects/Sidepad/assets/Sidepad Icon screenshot/Screenshot 2026-02-28 at 8.44.12 PM.png" /Users/raph/Developer/Projects/Sidepad-Website/assets/screenshot.png
```

**Step 2: Commit**

```bash
git add assets/
git commit -m "chore: add brand assets (logo and screenshot)"
```

---

### Task 3: Landing Page (index.html)

**Files:**
- Create: `index.html`

**Step 1: Create index.html**

Full single-scroll marketing page with these sections:
- **Header (sticky):** Logo + "Sidepad" text (left), nav links Features / Privacy / Terms (center-right), "Add to Chrome" navy CTA button (right)
- **Hero:** `bg-hero-bg` section. Left side: bold headline "Capture and compose from anywhere on the web", subtext "Your companion for AI conversations. Capture responses from ChatGPT, Claude, and other AI tools into structured Markdown documents — saved locally, never uploaded.", "Add to Chrome" CTA button. Right side: screenshot image in a subtle browser-frame mockup (rounded corners, shadow).
- **Features:** 4 cards in a 2x2 grid on `bg-surface` background. Each card has an SVG icon (inline, colored `text-feature-icon`), title in `text-primary`, description in `text-foreground-secondary`. Cards:
  1. "Capture from any page" — "Highlight text on any webpage, then press ⌘+Shift+S or right-click to send it to Sidepad. Works everywhere."
  2. "Structured Markdown" — "Organize captures with headings, notes, and annotations. Every snippet links back to its source."
  3. "Local-first storage" — "Your documents are saved as .md files on your computer. No cloud, no account, no sign-up required."
  4. "Built for AI workflows" — "Designed for capturing from ChatGPT, Claude, Gemini, and other AI conversations."
- **How It Works:** `bg-hero-bg` section. Three numbered steps in a horizontal row: "1. Capture — Highlight text and send to Sidepad with a keyboard shortcut", "2. Organize — Add headings, notes, and annotations to structure your document", "3. Save — Export as Markdown files to any folder on your computer". Small amber accent line or dot on the step numbers.
- **Footer:** `bg-primary` dark navy background, white text. Links to Privacy Policy and Terms of Use. Copyright "© 2026 Sidepad. All rights reserved." Tagline: "Built for researchers, writers, and thinkers."

All pages link `dist/output.css`. Use semantic color classes from the `@theme` tokens: `text-foreground`, `bg-surface-subtle`, `text-primary`, `bg-cta`, `hover:bg-cta-hover`, `text-foreground-secondary`, `text-foreground-tertiary`, `bg-hero-bg`, `text-feature-icon`, `border-border-color`.

Use `@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap')` in the HTML head for typography. Set `font-family: 'Inter', system-ui, sans-serif` on body.

**Step 2: Build CSS and verify**

Run: `cd /Users/raph/Developer/Projects/Sidepad-Website && npm run build:css`

Open `index.html` in browser to verify layout and colors.

**Step 3: Commit**

```bash
git add index.html dist/output.css
git commit -m "feat: add marketing landing page"
```

---

### Task 4: Privacy Policy Page (privacy.html)

**Files:**
- Create: `privacy.html`

**Step 1: Create privacy.html**

Same header and footer as index.html. Main content is a centered prose column (`max-w-3xl mx-auto`) with:

**Title:** "Privacy Policy"
**Effective date:** March 1, 2026

**Sections:**

1. **Overview** — Sidepad is a Chrome extension that helps you capture and organize text from web pages. We are committed to protecting your privacy. This policy explains how Sidepad handles your data.

2. **Data Collection** — Sidepad does not collect, transmit, or store any personal data on external servers. All data remains on your device.

3. **Local Storage** — Sidepad stores your documents and settings locally using two mechanisms:
   - `chrome.storage.local` — for document state and pending captures
   - File System Access API — for saving `.md` files to a folder you choose on your computer

   No data is sent to any server. Sidepad has no backend, no database, and no cloud storage.

4. **Analytics and Tracking** — Sidepad does not use cookies, analytics, telemetry, or any third-party tracking scripts.

5. **Accounts** — Sidepad does not require or support user accounts. There is no sign-up, login, or authentication.

6. **Chrome Permissions** — Sidepad requests the following permissions, each used solely for its core functionality:
   - `sidePanel` — to display the Sidepad interface in Chrome's side panel
   - `contextMenus` — to provide a "Send to Sidepad" option when you right-click selected text
   - `storage` — to save your document state and pending captures locally
   - `activeTab` — to read the URL of your current tab for source attribution on captured text
   - `scripting` — to capture selected text on pages where the content script is not yet loaded

7. **Data Deletion** — You can delete your data at any time by:
   - Removing `.md` files from your chosen save folder
   - Clearing extension data in Chrome settings
   - Uninstalling the extension

8. **Changes to This Policy** — We may update this policy from time to time. Changes will be posted on this page with an updated effective date.

9. **Contact** — If you have questions about this privacy policy, contact us at support@sidepad.app.

**Step 2: Build CSS and verify**

Run: `npm run build:css`

Open `privacy.html` in browser.

**Step 3: Commit**

```bash
git add privacy.html dist/output.css
git commit -m "feat: add privacy policy page"
```

---

### Task 5: Terms of Use Page (terms.html)

**Files:**
- Create: `terms.html`

**Step 1: Create terms.html**

Same header and footer. Centered prose column. Content:

**Title:** "Terms of Use"
**Effective date:** March 1, 2026

**Sections:**

1. **Acceptance of Terms** — By installing or using Sidepad, you agree to these terms. If you do not agree, please uninstall the extension.

2. **Description of Service** — Sidepad is a Chrome extension that allows you to capture text from web pages and organize it into structured Markdown documents saved locally on your device.

3. **Use of the Extension** — You may use Sidepad for any lawful purpose. You are responsible for all content you capture and create using the extension.

4. **Intellectual Property** — Sidepad and its original content, features, and functionality are owned by Sidepad. The text you capture and documents you create belong to you.

5. **No Warranty** — Sidepad is provided "as is" and "as available" without warranties of any kind, either express or implied. We do not guarantee that the extension will be uninterrupted, error-free, or free of harmful components.

6. **Limitation of Liability** — To the fullest extent permitted by law, Sidepad shall not be liable for any indirect, incidental, special, consequential, or punitive damages arising from your use of the extension.

7. **Changes to Terms** — We reserve the right to modify these terms at any time. Changes will be posted on this page with an updated effective date. Continued use of the extension constitutes acceptance of the updated terms.

8. **Contact** — If you have questions about these terms, contact us at support@sidepad.app.

**Step 2: Build CSS and verify**

Run: `npm run build:css`

Open `terms.html` in browser.

**Step 3: Commit**

```bash
git add terms.html dist/output.css
git commit -m "feat: add terms of use page"
```

---

### Task 6: Visual Polish and Final Build

**Files:**
- Modify: `index.html` (if needed)
- Modify: `input.css` (if needed)

**Step 1: Run final CSS build**

Run: `npm run build:css`

**Step 2: Visual review of all three pages**

Open each page in browser. Check:
- Color consistency with extension palette
- Typography hierarchy (headings, body, secondary text)
- Responsive layout at mobile, tablet, desktop widths
- All internal links work (nav links, footer links)
- Screenshot renders clearly in hero section
- CTA buttons have correct hover states

**Step 3: Fix any issues found**

**Step 4: Final commit**

```bash
git add -A
git commit -m "polish: visual refinements and final build"
```

---

### Task 7: GitHub Pages Deployment Setup

**Step 1: Create GitHub repository**

Run: `cd /Users/raph/Developer/Projects/Sidepad-Website && gh repo create Sidepad-Website --public --source=. --push`

**Step 2: Enable GitHub Pages**

Run: `gh api repos/{owner}/Sidepad-Website/pages -X POST -f source.branch=main -f source.path=/`

Or configure manually: GitHub repo → Settings → Pages → Source: main branch, root folder.

**Step 3: Configure custom domain DNS**

User action (manual): Point `sidepad.app` DNS to GitHub Pages:
- A records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
- CNAME: `www.sidepad.app` → `<username>.github.io`

**Step 4: Verify deployment**

Visit `https://sidepad.app` (after DNS propagation) and confirm all three pages load with HTTPS.

**Step 5: Update Chrome Web Store submission checklist**

Mark "Write and host a privacy policy" as complete in `/Users/raph/Developer/Projects/Sidepad/docs/plans/2026-03-01-chrome-web-store-submission.md`. The privacy policy URL is `https://sidepad.app/privacy`.
