# Product Requirements Document (PRD)

## Aslam Tuition Classes — One-Page Landing Website

| Field | Value |
|---|---|
| Document version | 1.0 |
| Date | 19 October 2026 |
| Status | Approved for build |
| Owner | Aslam Tuition Classes |

---

## 1. Overview

### 1.1 Problem
Aslam Tuition Classes (Dadar East, Mumbai) offers NIOS home tuition and academic support, but prospective students/parents currently learn about the classes only through word of mouth or walk-ins. There is no single, shareable link that answers the three questions every enquiry asks: **What do you teach? When? Where? How do I call you?**

### 1.2 Solution
A single-page, mobile-first landing website that:
- Introduces the classes and their NIOS specialisation.
- Makes calling or WhatsApping the tutor one tap away from any point on the page.
- Shows the exact location with an embedded map and directions link.
- Answers common questions (timings, enrolment, subjects) via an FAQ.

### 1.3 Primary goal
Convert a visitor into a phone/WhatsApp enquiry. The page has **one** conversion action: contact the classes.

### 1.4 Non-goals (v1)
- Online payment, admission forms, or student portals.
- Blog, gallery, or multi-page navigation.
- CMS or backend — the page is a static file.
- Dedicated mobile app or PWA.

---

## 2. Target audience

| Persona | Description | Need |
|---|---|---|
| **NIOS learner** | Student (age 14–25) enrolled in NIOS secondary/senior secondary, needs subject tuition and exam guidance. | Flexible batch times, subject coverage, home tuition. |
| **Parent / guardian** | Parent of a school or NIOS student in Dadar, Parel, Matunga, Sion. | Trust, proximity, timings that fit school hours, quick call. |
| **Working student** | Employed learner who can only attend early-morning or weekend batches. | Clear timetable, weekend availability. |

**Geography:** Primary — Dadar East, Parel, Hindmata, Matunga, Wadala, Sion, Lower Parel (≈ 14-minute walk from Parel station).

---

## 3. Business information (source of truth)

| Item | Value |
|---|---|
| Name | Aslam Tuition Classes (NIOS Home Tuition) |
| Address | RANGARI MASJID BLDG, 158/B, Dada Saheb Phalke Marg, Hindmata, Dadar East, Mumbai, Maharashtra 400014 |
| Phone (E.164) | `+919702074658` |
| Phone (display) | +91 97020 74658 |
| Proximity note | Approx. 14 minutes walk from Parel |
| Offerings | NIOS Home Tuition, academic support for students |

### 3.1 Class schedule (as provided)

| Day | Timings |
|---|---|
| Monday | 7:30 AM – 9:00 AM (+ afternoon tutorial blocks) |
| Tuesday | 7:30 AM – 9:00 AM (+ afternoon tutorial blocks) |
| Wednesday | 7:00 AM – 9:00 AM |
| Thursday | 7:30 AM – 9:00 AM (+ afternoon tutorial blocks) |
| Friday | 7:30 AM – 9:00 AM (+ afternoon tutorial blocks) |
| Saturday | 8:00 AM – 9:30 AM |
| Sunday | 10:00 AM – 11:00 AM |

> **Note for content editors:** Exact afternoon tutorial block times were not specified. The schedule is exposed in the FAQ answer as a structured list using only the confirmed times. Update `index.html` when exact afternoon slots are confirmed.

---

## 4. Success metrics

| Metric | Target | How measured |
|---|---|---|
| Call/WhatsApp taps | 10%+ of unique visitors | Analytics event / link click tracking (optional, v1.1) |
| Bounce rate | < 60% | Hosting analytics |
| Mobile load time | < 2 s on 4G | Lighthouse |
| Lighthouse Performance | ≥ 95 | Lighthouse |
| Address/phone accuracy | 100% | Manual QA checklist |

---

## 5. Requirements

### 5.1 Functional

| ID | Requirement | Priority |
|---|---|---|
| F1 | Display business name, NIOS positioning, and tagline above the fold. | P0 |
| F2 | "Call Now" CTA must use a `tel:` link to `+919702074658` — one tap to dial. | P0 |
| F3 | "WhatsApp" CTA must open `https://wa.me/919702074658` with a pre-filled enquiry message. | P0 |
| F4 | Sticky header with business name + Call button, visible after scroll. | P1 |
| F5 | Sticky bottom call bar on mobile viewports (< 768 px) with Call + WhatsApp. | P0 |
| F6 | About / "Why choose us" section with 4 benefit cards. | P1 |
| F7 | Location section with full address, walk-from-Parel note, and "Get Directions" link to Google Maps. | P0 |
| F8 | Embedded Google Map (no API key) centred on the address. | P0 |
| F9 | FAQ section using native `<details>/<summary>` accordions, functional without JavaScript. | P1 |
| F10 | FAQ must include the full weekly timetable (§3.1). | P0 |
| F11 | Footer with name, phone, address, copyright year. | P2 |
| F12 | All contact links work from every section (CTAs repeated at hero, header, sticky bar). | P0 |

### 5.2 Non-functional

| ID | Requirement | Target |
|---|---|---|
| N1 | Single static file, no build step, no external JS libraries. | 1 × `index.html` |
| N2 | Fully responsive at 360 px, 768 px, 1024 px, 1440 px. | No horizontal scroll |
| N3 | First Contentful Paint < 1.5 s on throttled 4G. | Lighthouse |
| N4 | Works with JavaScript disabled (except scroll header nicety). | Manual test |
| N5 | WCAG 2.1 AA: semantic landmarks, contrast ≥ 4.5:1, visible focus states, aria labels on icon-only controls. | axe / manual |
| N6 | SEO: unique `<title>`, meta description, Open Graph tags, `LocalBusiness` JSON-LD schema. | Valid rich result |
| N7 | Language: English copy. | — |
| N8 | Design system: clean & professional — navy/indigo primary, white surfaces, rounded cards, system font stack. | — |

---

## 6. Page structure (information architecture)

```
┌ Sticky header ────────────────────── [Call] ┐
│ 1. Hero        — headline, subline, Call + WhatsApp CTAs, trust chips
│ 2. About       — intro paragraph + 4 benefit cards
│ 3. Location    — address card, directions button, embedded map iframe
│ 4. FAQ         — 6 accordions incl. full timetable
│ 5. Footer      — name, phone, address, © year
└ Sticky mobile call bar (< 768 px):  [Call Now] [WhatsApp] ┘
```

### 6.1 FAQ content outline

1. Where are you located? (address + Parel walk note)
2. What are the class timings? (full weekly schedule)
3. Do you offer NIOS home tuition?
4. What subjects do you cover?
5. How do I enrol / book a demo?
6. How can I contact you?

---

## 7. Design direction

| Aspect | Decision |
|---|---|
| Style | Clean & professional, education/trust feel |
| Primary colour | Navy / indigo (`#1e3a8a` family) with accent (`#f59e0b` amber for CTA highlights) |
| Surfaces | White cards on light slate background |
| Typography | System font stack (`system-ui, -apple-system, Segoe UI, Roboto…`) — zero font requests |
| Imagery | None required (icon-only, inline SVG); keeps the file self-contained |
| Layout | Mobile-first, max content width 1080 px, 8 px spacing scale |

---

## 8. Technical approach

| Aspect | Decision | Rationale |
|---|---|---|
| Stack | Single static `index.html` with embedded `<style>` and minimal inline `<script>` | Hostable anywhere (Netlify, GitHub Pages, shared hosting, cPanel), zero tooling, easy to WhatsApp the file itself |
| Map | `https://maps.google.com/maps?q=<url-encoded address>&z=16&output=embed` in an `<iframe>` | Keyless, no billing account needed |
| Call | `tel:+919702074658` | Universal one-tap dial on mobile |
| WhatsApp | `https://wa.me/919702074658?text=<encoded message>` | Opens WhatsApp Web/app with message ready |
| FAQ | Native `<details>` | Accessible, works without JS |
| JS budget | ≤ 15 lines | Header scroll state + current year only |

---

## 9. Assumptions & open questions

| # | Item | Status |
|---|---|---|
| A1 | Business name shown as "Aslam Tuition Classes"; NIOS used as descriptor. | Assumed |
| A2 | Page language is English only. | Confirmed |
| A3 | Afternoon tutorial block timings TBD — shown as a note, not fabricated times. | **Open — needs client input** |
| A4 | Subject list not provided; FAQ answers generically ("core academic subjects + NIOS secondary & senior secondary"). | Assumed, needs review |
| A5 | No logo supplied; header uses text wordmark + graduation-cap SVG icon. | Assumed |
| A6 | No domain/hosting chosen yet; any static host will work. | Open |

---

## 10. Milestones

| Phase | Scope | Est. |
|---|---|---|
| M1 | PRD + README | Done |
| M2 | `index.html` build (all P0 + P1 items) | 1 session |
| M3 | QA: responsive, links, accessibility, Lighthouse | 1 session |
| M4 | Publish to host, connect analytics (optional) | TBD |
