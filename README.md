# privateeventmanager.com — Static Site

Hosted on Cloudflare Pages. This is the compliance and gateway site for Private Event Manager.

## Pages

| URL | File | Purpose |
|-----|------|---------|
| `/` | `index.html` | Homepage |
| `/signup/` | `signup/index.html` | Application form (posts to swinging.party API) |
| `/privacy-policy/` | `privacy-policy/index.html` | Privacy Policy |
| `/terms-and-conditions/` | `terms-and-conditions/index.html` | Terms & Conditions |
| `/sms-consent/` | `sms-consent/index.html` | SMS Consent info (for Twilio A2P verification) |

## Redirects

Handled by `_redirects` (Cloudflare Pages native):
- `/events/*` → `https://swinging.party/events/:splat` (301)
- `/join/*` → `https://swinging.party/join/:splat` (301)

## Signup Form

The signup form in `signup/index.html` posts to:
`https://swinging.party/wp-json/pem/v1/apply`

Update this URL when the REST endpoint is live on swinging.party (Phase 12).

## Email Obfuscation

Contact email is displayed using CSS `direction: rtl` trick — the HTML reads right-to-left but renders correctly visually. This defeats most email scrapers without JavaScript.

## Deployment

1. Push to GitHub
2. Cloudflare Pages auto-deploys on every push to main
3. Custom domain: privateeventmanager.com
4. Email Routing: info@privateeventmanager.com → your destination email (configured in Cloudflare dashboard)

## Font

Uses Google Fonts: Cormorant Garamond + Jost (loaded via CDN in style.css)
