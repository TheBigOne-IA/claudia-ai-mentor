# ⚖️ Claudia — My Career Mentor

> A personalized AI career mentor built for one client at a time.

---

## The Problem

Job searching is generic, time-consuming, and frustrating. Most tools treat every applicant the same way — and candidates with niche backgrounds (like a corporate lawyer who also trained as a nurse) rarely find tools that understand their real value.

## The Solution

**Claudia** is a personalized AI career mentor that works from a detailed profile of the person she's helping — their strengths, blind spots, target companies, and known behavioral patterns — and applies that context to every interaction. She doesn't give generic advice. She gives the right advice for that person, for that specific opportunity.

---

## Origin Story

Claudia started as a custom GPT — [**Meu Headhunter Jurídico CLT**](https://chatgpt.com/g/g-6918ea6f36ec8191acf9d2324e2bdd48-meu-headhunter-jurídico-clt) — built to support a single client: a corporate lawyer with a background in nursing, transitioning into the healthcare sector, applying for his first salaried (CLT) position after 10+ years as an independent contractor. The GPT prototype worked well, but living inside ChatGPT limited who could access it and how it could grow.

She was rebuilt from scratch as a standalone web app: a single-file React 18 application deployed on Cloudflare Workers, calling the Anthropic API through a secure server-side proxy — no ChatGPT dependency, full control over behavior and interface, and a clear path toward a native Android release (Play Store, roadmap).

---

## Live Demo

🔗 **Try Claudia:** [claudia-app.big-cia.workers.dev](https://claudia-app.big-cia.workers.dev/)

This is a live pilot instance currently being tested by one client in a 30-day trial.

---

## How It Works

1. **Choose a module** — or just ask her a question directly.
2. **Provide the input** — paste a job URL or description, upload a CV/PDF/screenshot, or speak by voice.
3. **Claudia responds** using a fixed set of business rules for that client: company tiers, hard filters, tone corrections, and known blind spots.
4. **You get a structured, downloadable result** — a tailored CV, a ready-to-send cover letter (Word download), an interview prep sheet, or a clear GO / NO-GO verdict.

---

## Key Features

### 🎯 Five Active Modules

| Module | What it does |
|--------|-------------|
| **Reality Filter** | Evaluates a job posting against the client's profile → GO ✅ / NO-GO ❌ / ATTENTION ⚠️ |
| **CV Adaptation** | Rewrites the CV for a specific role, ATS keywords included, always in first person |
| **Interview Simulation** | Researches the company, generates 5 likely questions, models ideal answers |
| **Who to Contact** | Maps the decision-maker at a target company + drafts a personalized outreach message |
| **Job Search** | Searches LinkedIn, Gupy, Glassdoor and Indeed for active openings matching the client's profile |

### 📄 Document Generation & Download
- CV adaptations and cover letters generated as formatted **Word (.doc) files**, ready to send.
- Download button appears automatically when Claudia produces a complete document.

### 📎 File Upload & Analysis
- Accepts **images** (screenshots of Gupy/LinkedIn forms, offer letters, profile pages) and **PDF** (current CV, job descriptions).
- Claudia analyzes the attachment in context and returns specific, actionable feedback.

### 🎙️ Voice Input & Output
- **Speech-to-text:** Continuous recording mode — speak multiple sentences, stop when done.
- **Text-to-speech:** Claudia reads her own responses aloud. Voice picker lets the user select among available pt-BR voices. Stop button available mid-speech.

### 🔍 Active Job Search with Quality Filter
- Prioritizes **Gupy** and **LinkedIn Jobs** (platforms that auto-remove closed listings).
- Verifies each result before including it — closed postings, expired listings and broken links are excluded.
- Applies client-specific filters silently: location (São Paulo Capital for in-person, Brazil-wide for remote), PCD-affirmative tags (🟣), and hard exclusions (no law firms, ever).

---

## The Technology

### Architecture

```
Browser (index.html)
    │
    └──► Cloudflare Worker: claudia-app (static site + app shell)
              │
              └──► Cloudflare Worker: claudia-proxy (API gateway)
                        │
                        └──► Anthropic Messages API
                                  ├── Model: claude-sonnet-4-6
                                  └── Tools: web_search
```

### Stack

- **Front-end:** Single-file React 18 app (CDN, no build step). JSX via Babel Standalone. Zero npm dependencies.
- **Proxy Worker:** Holds the `ANTHROPIC_API_KEY` server-side as a Cloudflare Secret. Enforces CORS. Forwards requests to the Anthropic Messages API and returns the response.
- **LLM:** Claude (Anthropic) — `claude-sonnet-4-6` via Messages API with `web_search` tool enabled.
- **Personalization layer:** Structured client profile + system prompt encoding company tiers, behavioral corrections, tone, and hard rules.

---

## Personalization Layer — How Claudia "Knows" the Client

The system prompt encodes:

- **Profile:** 10+ years of corporate law experience, background in nursing (rare differentiator), first CLT job seeker.
- **Target companies (Tier 1):** 22 healthcare companies (hospitals, insurers, pharma, diagnostics) prioritized by preference.
- **Target companies (Tier 2):** Logistics sector as fallback.
- **Hard filter:** Law firms are silently excluded from all suggestions, always.
- **Behavioral corrections:** Client tends to write "we did" instead of "I did" — Claudia corrects this with context, not criticism.
- **Language alerts:** Client reads English but does not speak it — mandatory alert when a role requires fluency.

---

## Roadmap

- [ ] Multi-tenant support — each client gets their own profile and agent
- [ ] Neural voice (replace browser TTS)
- [ ] Native Android release (Play Store)
- [ ] Persistent conversation history with session drawer
- [ ] Per-client branding and avatar
- [ ] `web_fetch` tool for reading job URLs directly

---

## Thesaurus Entry (Career Mentoring Domain)

| Relation | Term |
|----------|------|
| **BT** | AI-Powered Career Services |
| **NT** | CV Analysis & Optimization; Cover Letter Generation; Job Matching; Interview Preparation |
| **RT** | Recruitment Automation; Personal Branding; Candidate Experience |
| **UF** | Career Copilot; AI Mentor; Job Application Agent; Headhunter IA |

---

## Repository Structure

```
claudia/
├── index.html          # Full React app (single file, no build step)
├── worker.js           # Cloudflare Worker proxy (API gateway)
└── README.md
```

---

## About

Built by **Monalizza Goh** — AI/Localization Specialist & Career Consultant.  
This project is a working pilot, not a demo. One real client. One real job search. Real results.
