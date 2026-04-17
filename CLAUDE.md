# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static compliance and gateway site for `privateeventmanager.com`, hosted on Cloudflare Pages. Pure HTML5/CSS3/vanilla JS — no build step, no framework, no package manager.

## Running Locally

No build required. Serve the directory with any static server:

```bash
python -m http.server 8000
# or
npx http-server
```

## Deployment

Push to `main` → Cloudflare Pages auto-deploys. Custom domain: `privateeventmanager.com`.

## Architecture

**Single global stylesheet:** `style.css` — all pages share it. Uses CSS custom properties for the color palette (dark navy, gold, cream). Mobile breakpoints at 768px and 480px.

**Pages:**
- `/` (`index.html`) — Single-scroll homepage. Hero → How It Works → Footer.
- `/signup/` — Application form; POSTs JSON to `https://swinging.party/wp-json/pem/v1/apply`
- `/privacy-policy/`, `/terms-and-conditions/`, `/sms-consent/` — Legal/compliance pages required for Twilio A2P SMS registration

**Routing:** `_redirects` proxies `/events/*` and `/join/*` to `swinging.party` via 301.

## Positioning & Tone

The platform is invitation-only event management for private clubs and membership organizations — closed groups that need to control who joins and who attends (e.g. clubs, alumni groups, hobbyist circles, membership associations). The site content is deliberately neutral and upscale.

**Do not use these words or framings in any page copy:**
- "discretion," "complete discretion," "absolute discretion"
- "secrecy," "secret," "discreet"
- "lifestyle" or any lifestyle-adjacent language
- "events that require privacy" (the platform is built for *hosts who run private groups*, not for events whose content is secret)

**Do not list specific example group types on the homepage.** Keep descriptions abstract ("private clubs, membership organizations, and invitation-only groups"). Example types may appear in this CLAUDE.md for internal context but never in public-facing copy.

**Homepage is single-scroll.** Do not add a Features grid, an About section, or additional marketing sections without discussion. The Hero and How It Works sections, plus the footer, are the whole page.

## Key Conventions

**Email obfuscation:** Contact email uses CSS `direction: rtl` — the HTML characters are reversed but render correctly. Do not "fix" this; it's intentional scraper protection.

**SMS consent flow:** In `signup/index.html`, the SMS opt-in checkbox is hidden until a phone number is entered (JS toggle). This is a compliance requirement — do not remove the conditional display logic.

**Form endpoint:** `https://swinging.party/wp-json/pem/v1/apply` — expects JSON POST, returns `{ success: bool, message?: string }`.

**Typography:** Cormorant Garamond (headings/serif) + Jost (body/sans-serif), loaded from Google Fonts CDN in `style.css`.
