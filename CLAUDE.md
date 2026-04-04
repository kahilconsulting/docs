# University Student Lifecycle Explorer — Project Instructions

Instructions for Claude on how to maintain, extend, and modify the Student Lifecycle Explorer (`Student Lifecycle Explorer.html`).

---

## Overview

A single self-contained HTML file — an **interactive Student Lifecycle explorer** for universities, co-branded between **Bayshann** and **Kahil Consulting**. It renders a 6-stage lifecycle as a CSS Grid with click-to-expand detail panels. Solution stack: **Microsoft Power Apps**, **Power Pages**, and **Copilot Studio Agents**.

**Stage content is the source of truth in the HTML file.** All stage/card data lives in the `STAGES` array in `Student Lifecycle Explorer.html`. Read that file before modifying or extending any content — do not rely on this file for content details.

---

## Branding & identity

- **Primary brand:** Bayshann
  - Logo image: `https://images.squarespace-cdn.com/content/v1/697a873a313d78431864c69f/df0d74a2-4bd9-4c41-a37b-b1349abe9cb7/Bayshann-Full-Logo-Blue-Transparent.png.png`
- **Partner brand:** Kahil Consulting
  - Logo image: `https://kahilconsulting.com/wp-content/uploads/2025/11/cropped-Kahil-Consulting-Logo2.png`
- Both logos appear in a co-brand strip at the top of the page header, separated by a vertical divider

**Colour palette**
- Teal accent: `#2FA6A4` (hover: `#1F7F7D`)
- Dark: `#111827`
- Background: `#F6F8FB`
- Borders: `#E2E8F0`
- Light muted text: `rgba(17,24,39,0.55–0.72)`

**Typography:** Segoe UI (system font, no external dependency), weights 400 / 500 / 600 / 700

---

## Page header

- Co-brand strip (logos)
- Page title: `StudentFlow XP`
- Sub-title: `Modern Student Lifecycle Platform to manage the entire Student Journey` (font-size 12px)
- No tagline

---

## Grid layout

A CSS Grid with:
- **Column 1:** Row label (76 px wide, vertical rotated text)
- **Columns 2–7:** One column per lifecycle stage (6 stages)
- **Final row:** Full-width "Student Support" continuous layer strip

**Rows (in order)**
1. Stage header pills (dark pill badges with stage name)
2. Features — functional capability cards with platform badge, clickable (multiple per cell)
3. Common Features — grey dashed card, clickable
4. AI Agents — Copilot Agent card (indigo accent), clickable
6. Student Support — full-width teal-accent strip, clickable

---

## Card types & visual styles

| Card type | Background | Border | Eyebrow colour |
|---|---|---|---|
| Feature card (`.w-card`) | `#fff` | `1px solid #E2E8F0` | — (platform badge only) |
| Common Features (`.common-feat-card`) | `#F6F8FB` | `1.5px dashed #c8cdd8` | muted dark |
| AI Agent (`.agent-card`) | `rgba(67,56,202,0.07)` | `1.5px solid rgba(67,56,202,0.25)` | `#4338CA` (indigo) |

Each lifecycle stage has its own distinct pastel colour applied to the stage pill and key activity card backgrounds:

| Stage | Pill colour | Card background |
|---|---|---|
| Nurture & Enquiry | `#FF8FAB` (pastel pink) |
| Applications & Admissions | `#FFB085` (pastel peach) |
| Enrolment & Onboarding | `#FFD97D` (pastel yellow) |
| Study & Engage | `#80D8A8` (pastel mint) |
| Graduation | `#7EC8E3` (pastel sky blue) |
| Alumni Management | `#B8A0D8` (pastel lavender) |

Colours are injected as a dynamic `<style>` block via `injectStageStyles()` using `data-sid` attributes. Each colour is used for the stage header top border (`::before`) and the feature card left border (`border-left-color`).

All cards have hover states (border strengthens to teal, subtle shadow / background shift). Key activity cards lift `translateY(-1px)` on hover.

Each card title includes a small grey count badge (`<span class="card-count">N</span>`) showing the number of items in the detail panel.

**Badges on key activity cards**
- Type badge: `Power Apps` (dark pill), `Power Pages` (light grey), `Copilot Agent` (light grey)
- An optional short descriptor badge (e.g. "Staff portal", "Self-service", "AI-assisted")

---

## Slide-in detail panel

A fixed right-side panel (500 px wide, full height) that slides in from off-screen when a card is clicked. A semi-transparent blurred overlay covers the rest of the page.

Panel structure:
- Close button (✕) top-right
- Eyebrow (stage name / context)
- Title (large, bold)
- Meta row (platform badge + type label)
- Scrollable body containing:
  - Description paragraph
  - Optional note/callout box (amber or green teal variant)
  - Sections with optional sub-headings and bullet lists

Keyboard support: Enter / Space to open any card; Escape to close panel.

---

## Stage content

All stage and card content (key activities, student actions, staff prepare, outcomes, Student Support) is defined in the `STAGES` array and the `supportLayer` object in `Student Lifecycle Explorer.html`. **Always read the HTML file before modifying content** — this file does not duplicate it.

To add or edit a stage, card, or detail panel: find the relevant entry in the `STAGES` array and update it there.

---

## Technical requirements

- Single self-contained HTML file — no external JS dependencies (no frameworks)
- All CSS embedded in `<style>` tag; all JS in a `<script>` tag
- Data-driven: stages and content stored in a `STAGES` JS array; grid rendered dynamically via `renderGrid()`
- Grid uses CSS Grid with `grid-template-columns: 76px repeat(6, 1fr)` — row label column + 6 stage columns
- Overflow-x scrollable on small screens; min-width 960 px for the grid
- Responsive: panel goes full-width on mobile (`max-width: 768px`)
- Keyboard accessible: cards respond to Enter / Space; Escape closes panel
- XSS-safe: all user-facing strings passed through an `esc()` HTML-escape helper before insertion via `innerHTML`
- Font: Segoe UI (system font — no Google Fonts dependency required)
