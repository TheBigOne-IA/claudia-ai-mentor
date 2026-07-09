# Claudia — System Architecture (Production Pilot)

## Architecture Overview
┌─────────────────────────────────────────────────────────────────┐
│ Browser (Client Side) │
│ index.html (React 18) │
│ No build step — CDN + Babel Standalone │
└─────────────────────────────┬───────────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────────────┐
│ Cloudflare Worker: claudia-app │
│ Static site hosting + app shell │
└─────────────────────────────┬───────────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────────────┐
│ Cloudflare Worker: claudia-proxy │
│ API Gateway (CORS) │
│ Holds ANTHROPIC_API_KEY as Secret │
└─────────────────────────────┬───────────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────────────┐
│ Anthropic Messages API │
│ Model: claude-sonnet-4-6 │
│ Tools: web_search enabled │
└─────────────────────────────────────────────────────────────────┘

## Why This Architecture?

| Decision | Rationale |
|----------|-----------|
| **Single-file React app** | No build step, easy to deploy, zero npm dependencies. Perfect for a pilot. |
| **Cloudflare Workers** | Scalable, low-latency, serverless. Handles the pilot load (one client) with room to grow. |
| **Proxy Worker** | Keeps the API key secure (not exposed to the browser). Enforces CORS. |
| **Anthropic Claude** | Chosen for reasoning quality, tool calling (web_search), and multilingual support (pt-BR). |
| **No ChatGPT dependency** | Claudia was rebuilt to be independent — she is not a GPT wrapper. |

## What Makes This Architecture Unique

1. **Personalization is in the system prompt** — not in the code. This means Claudia can be reconfigured for a new client in minutes, not weeks.

2. **The client profile is encoded as business rules:**
   - Tier 1 companies (healthcare): 22 manually curated organizations
   - Tier 2 companies (logistics): fallback sector
   - Hard filters: law firms are silently excluded
   - Behavioral corrections: "we" → "I" in CV language
   - Language alerts: English-required jobs trigger a mandatory flag

3. **Modules are prompt-defined, not coded.** Each module (Reality Filter, CV Adaptation, Interview Simulation, Who to Contact, Job Search) is a different system prompt variation.

## Security

- `ANTHROPIC_API_KEY` is stored as a Cloudflare Secret — never exposed to the client.
- All requests are proxied through `claudia-proxy`.
- No user data is persisted (pilot phase — session only).
- Future versions will use per-client encrypted profiles.

## Current Limitations

- No multi-tenant support (one client at a time)
- No persistent session history (resets on page refresh)
- TTS uses browser API (voice quality varies by OS/browser)
- No Android app yet (roadmap)

## Next Technical Steps

- [ ] Migrate to multi-tenant architecture
- [ ] Add persistent conversation storage (Cloudflare D1)
- [ ] Implement neural voice (ElevenLabs or similar)
- [ ] Build native Android app for Play Store release
- [ ] Add `web_fetch` tool for reading job URLs directly
