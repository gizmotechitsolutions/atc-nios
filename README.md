# Nes Asha — Landing Page

Single-page, mobile-first landing page for **Nes Asha** (A School For Slow Learners, Dadar East, Mumbai), contact person: Mr. Aslam Kundiwala.

**Live action:** one goal — get the visitor to call or WhatsApp.

---

## Quick start

No build step, no dependencies. Just open the file:

```powershell
start .\index.html
```

Or double-click `index.html` in File Explorer.

---

## What's inside

```
atc/
├── index.html   # the entire landing page (HTML + CSS + tiny JS)
├── images/      # 5 stock photos (local fallbacks for the CDN URLs)
├── PRD.md       # product requirements document
└── README.md    # this file
```

Styles, icons, and scripts are all inlined in `index.html` (≈ 27 KB). Photos (≈ 540 KB total) load from the Pixabay CDN and fall back to the local `images/` folder automatically. No fonts or libraries to download.

---

## Page sections

| # | Section | Purpose |
|---|---|---|
| 1 | Sticky header | Business name + Call button, appears on scroll |
| 2 | Hero | Photo background, headline, benefit-led subline, Call + WhatsApp CTAs, "At a glance" panel |
| 3 | About / Why choose us | Intro + 4 photo benefit cards |
| 4 | Location | Full address, walk-from-Dadar-and-Parel note, embedded Google Map, Get Directions |
| 5 | FAQ | Accordion answers incl. full weekly timetable |
| 6 | Footer | Name, phone, address, © year |
| — | Sticky mobile bar | Call + WhatsApp buttons fixed at bottom (< 768 px) |

---

## Contact links used

| Link | Where it points |
|---|---|
| Call buttons | `tel:+919702074658` |
| WhatsApp buttons | `https://wa.me/919702074658?text=...` (pre-filled enquiry message) |
| Get Directions | Google Maps directions to the Dadar East address |
| Map embed | Keyless `maps.google.com/maps?q=...&output=embed` iframe |

---

## How to edit

Open `index.html` in any text editor (Notepad, VS Code).

### Change the phone number

Find & replace **all** occurrences of `9702074658` (used in `tel:`, `wa.me`, display text, and JSON-LD schema). The display format is `+91 97020 74658`.

### Change the WhatsApp pre-filled message

Search for `wa.me/919702074658?text=` — the message after `text=` is URL-encoded. Example decoded text:

> Hello, I am interested in NIOS Home Tuition at Nes Asha. Please share details.

### Change the address

Update it in **three** places:

1. The visible address text in the Location section.
2. The `q=` parameter of the Google Maps iframe URL (URL-encoded address).
3. The `address` field inside the JSON-LD `<script type="application/ld+json">` block in `<head>`.

### Change class timings

Timings live inside the FAQ answer for *"What are the class timings?"* — look for the `.timetable` list markup.

> **Known gap:** exact afternoon tutorial block times are not yet specified; the page only shows the confirmed morning/weekend slots plus a note. Update when the client confirms.

### Change colours

The palette is defined as CSS custom properties at the top of the `<style>` block:

```css
:root {
  --navy: #1e3a8a;      /* primary */
  --navy-dark: #172554;
  --accent: #f59e0b;    /* amber CTA highlight */
  --ink: #0f172a;       /* body text */
  --muted: #64748b;     /* secondary text */
  --bg: #f8fafc;        /* page background */
  --card: #ffffff;      /* card surface */
}
```

### Change the photos

Five photos live in `images/` (local fallbacks) and are referenced by their Pixabay CDN URL in `index.html`. To swap one:

1. Replace the file in `images/` with your new image.
2. Update the matching `<img src="…">` URL and its `onerror` fallback path in `index.html`.

All photos are from [Pixabay](https://pixabay.com) — free for commercial use, no attribution required.

---

## Deploying (any option works)

| Host | Steps |
|---|---|
| **Netlify Drop** | Drag the folder onto [app.netlify.com/drop](https://app.netlify.com/drop) — live in ~10 s. |
| **GitHub Pages** | Push `index.html` **and `images/`** to a repo → Settings → Pages → deploy from branch `main`. |
| **cPanel / shared hosting** | Upload `index.html` and the `images/` folder into `public_html/`. |
| **Vercel** | `npx vercel --prod` in this folder (framework preset: *Other*). |
| **WhatsApp** | Send the whole folder as a zipped document (photos live in `images/`). |

No environment variables, no server, no database.

---

## Browser support

Modern evergreen browsers: Chrome, Edge, Firefox, Safari (last 2 versions). The page also degrades gracefully with JavaScript disabled — only the sticky-header scroll effect is lost; all links and the FAQ still work.

---

## Accessibility & SEO checklist (built in)

- Semantic landmarks: `header`, `main`, `section`, `footer`
- FAQ uses native `<details>/<summary>` (keyboard accessible, no JS)
- Visible focus styles, aria-labels on icon-only controls
- Contrast ≥ 4.5:1 for all text
- Unique `<title>`, meta description, Open Graph tags
- `EducationalOrganization` / `LocalBusiness` JSON-LD schema for local SEO

---

## QA checklist before publishing

- [ ] Call button dials `+91 97020 74658` on a real phone
- [ ] WhatsApp button opens WhatsApp with the message pre-filled
- [ ] Google Map pin matches the Dadar East address
- [ ] Directions link opens Google Maps with the correct destination
- [ ] No horizontal scroll at 360 px width
- [ ] Timings in the FAQ match the client-confirmed schedule
- [ ] All 5 photos load (CDN) — and still appear from `images/` when the CDN is blocked
- [ ] Page renders with JavaScript disabled

---

## Roadmap ideas (v1.1+)

- Subjects list section with per-subject cards
- Testimonials from parents/students
- Contact form (FormSubmit / Web3Forms — no backend needed)
- Click-to-call analytics (Plausible / GoatCounter event)
- Exact afternoon tutorial block timings (blocked on client input)
