# Claudia — 30-Day Pilot Results

## Pilot Overview

**Client:** Corporate lawyer with nursing background, transitioning to healthcare sector  
**Duration:** 30 days (ongoing)  
**Goal:** Secure first salaried (CLT) position in healthcare after 10+ years as independent contractor  
**Status:** Active pilot — real job search, real applications, real results

---

## Key Metrics (as of pilot)

| Metric | Result |
|--------|--------|
| **Active modules used** | 5 (all modules) |
| **Job searches executed** | 20+ |
| **CV adaptations generated** | 3 |
| **Cover letters generated** | 5 |
| **Interview simulations run** | 2 |
| **GO / NO-GO verdicts** | 12 postings evaluated |
| **Target companies mapped** | 22 (Tier 1 healthcare) |
| **Satisfaction score** | 8.5 / 10 (user-rated) |

---

## What's Working

### 1. Reality Filter (GO / NO-GO)
- Claudia successfully identified **6 NO-GO** postings that matched the title but not the client's profile (seniority mismatch, law firm affiliation, location outside SP).
- Saved the client from wasting time on irrelevant applications.

### 2. CV Adaptation
- The client reported that Claudia's adaptations "capture the nuance" of his hybrid background (law + nursing) better than any previous version he's written.
- **Example:** Claudia transformed "we did" → "I did" across all CVs, addressing a known blind spot.

### 3. Interview Simulation
- Claudia researched actual target companies (Tier 1 healthcare) and generated company-specific questions.
- The client used the simulations to prepare and reported feeling "more confident" in conversations.

### 4. Job Search
- Claudia prioritizes Gupy and LinkedIn Jobs (auto-remove closed listings).
- Applied client-specific filters: location (SP Capital for in-person, Brazil-wide for remote), PCD-affirmative tags (🟣), and hard exclusions (no law firms).
- **Result:** Only relevant opportunities are presented.

---

## What's Not Working (Yet)

| Issue | Status |
|-------|--------|
| **Voice output quality** | Browser TTS is acceptable but not professional. Neural voice is roadmapped. |
| **Multi-tenant support** | Claudia is hard-coded for this client. Adding a second client requires code changes. |
| **Persistent history** | Conversations reset on page refresh. Workaround: client saves outputs manually. |
| **Android app** | Claudia is web-only for now. Native app is roadmapped. |
| **Direct job URL reading** | Client must paste job descriptions manually. `web_fetch` tool is roadmapped. |

---

## User Feedback (Direct Quote)

> *"Claudia understood my profile in a way no other tool has. She helped me articulate my hybrid experience in a way that recruiters actually notice. She doesn't treat me like a generic candidate — she knows my blind spots, my target companies, and what I need to fix before I even ask."*
> — Caio, Pilot Client

---

## Lessons Learned

| Lesson | Implication |
|--------|-------------|
| **Personalization works** | A single client with a tailored profile gets better results than a generic tool serving millions. |
| **Hard filters are essential** | Silently excluding law firms (the client's explicit request) made the outputs more relevant and saved time. |
| **Behavioral corrections need context** | Claudia corrects "we" → "I" with context, not criticism. The client accepted the feedback because it was framed as "this makes you look like a leader." |
| **Modules are the right abstraction** | Each module is a distinct use case. This makes the system extensible without re-architecting. |

---

## Next Steps (Pilot Phase 2)

- [ ] Expand job search to additional platforms (Indeed, Glassdoor)
- [ ] Add `web_fetch` tool to read job URLs automatically
- [ ] Enable persistent session history
- [ ] Prepare for client #2 (multi-tenant architecture)
- [ ] Begin Android app development

---

## Validation

Claudia's 8.5/10 satisfaction score is based on:

- **Relevance:** Outputs are highly specific to the client's profile and target companies
- **Accuracy:** The GO/NO-GO decisions are consistently correct
- **Usability:** Intuitive interface with voice, text, and file upload
- **Impact:** The client has already applied to 5 positions and has received 2 interview invitations
