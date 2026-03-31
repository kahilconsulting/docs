# University Student Lifecycle Explorer — HTML Diagram Instructions

This file documents the prompt/instructions used to generate the Student Lifecycle interactive explorer HTML page. Use it to regenerate, update, or extend the file consistently.

---

## What to build

Generate a single, self-contained HTML page — an **interactive Student Lifecycle explorer** for universities, co-branded between **Bayshann** and **Kahil Consulting**.

The page renders a 6-stage student lifecycle as a CSS Grid, with click-to-expand detail panels for every card. The solution stack is built on **Microsoft Power Apps**, **Power Pages**, and **Copilot Studio Agents**.

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
- **Column 1:** Row label (76 px wide) — labels: *(empty)*, "Key activities", "Student actions", "Staff prepare", "Outcomes"
- **Columns 2–7:** One column per lifecycle stage (6 stages)
- **Final row:** Full-width "Student Support" continuous layer strip

**Rows (in order)**
1. Stage header pills (dark pill badges with stage name)
2. Key activities — app/agent function cards, clickable
3. Student actions — student self-service cards (teal dashed), clickable
4. Staff prepare — backstage staff work cards (grey dashed), clickable
5. Outcomes — teal-tinted outcome cards, clickable
6. Student Support — full-width teal-accent strip, clickable

---

## Card types & visual styles

| Card type | Background | Border | Eyebrow colour |
|---|---|---|---|
| Key activity card | `#fff` | `1px solid #E2E8F0` | — (badge only) |
| Student actions card | `rgba(221,242,241,0.5)` | `1.5px dashed rgba(47,166,164,0.45)` | `#2FA6A4` |
| Staff prepare card | `#F6F8FB` | `1.5px dashed #c8cdd8` | muted dark |
| Outcome card | `rgba(47,166,164,0.06)` | `1px solid rgba(47,166,164,0.28)` | `#2FA6A4` |

Each lifecycle stage has its own distinct pastel colour applied to the stage pill and key activity card backgrounds:

| Stage | Pill colour | Card background |
|---|---|---|
| Nurture & Enquiry | `#3D7EC8` (blue) | `rgba(180,215,242,0.42)` |
| Applications & Admissions | `#C96B2A` (orange) | `rgba(248,196,152,0.42)` |
| Enrolment & Onboarding | `#8B4EA8` (violet) | `rgba(210,178,228,0.42)` |
| Study & Engage | `#B8860B` (amber) | `rgba(250,226,140,0.45)` |
| Graduation | `#28855A` (emerald) | `rgba(178,222,196,0.42)` |
| Alumni Management | `#546AA0` (slate blue) | `rgba(188,198,232,0.42)` |

Colours are injected as a dynamic `<style>` block via `injectStageStyles()` using `data-sid` attributes on stage header and key-activity cells. Student actions, staff prepare, and outcome cards retain their existing cross-stage styles.

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

## Lifecycle stages & content

### Stage 1 — Nurture & Enquiry

**Key activities**
- *Course Discovery* · Power Pages · Self-service — Prospective students browse courses, entry requirements, fees, and campus information through a public-facing portal
- *Enquiry Management* · Power Apps · Staff portal — Staff capture, assign, and track all inbound enquiries; log interactions; set follow-up tasks
- *AI Enquiry Agent* · Copilot Agent · AI-assisted — Answers common questions about courses, entry requirements, and processes 24/7; captures lead details; escalates to staff when needed
- *Open Day & Event Registration* · Power Pages · Self-service — Prospective students register for open days, campus tours, and information sessions

**Student actions**
- Title: "Prospect Self-Service"
- Description: What a prospective student can do independently before speaking to anyone
- Items: Browse courses and entry requirements; Submit an enquiry via web form or chat; Register for an open day or campus tour; Track responses to their enquiry

**Staff prepare**
- Items: Review and qualify inbound enquiries; Assign enquiries to the right advisor or faculty; Prepare personalised follow-up communications; Log all prospect interactions in the CRM record; Monitor engagement and flag high-intent prospects

**Outcomes**
- A qualified prospect record with full enquiry history
- Advisor assigned and follow-up scheduled
- Prospect's course interests and intent captured
- Engagement score to prioritise outreach

---

### Stage 2 — Applications & Admissions

**Key activities**
- *Online Application* · Power Pages · Self-service — Students complete and submit their full application including personal details, academic history, supporting statements, and required documents
- *Document Management* · Power Pages · Self-service — Secure upload of transcripts, identification, references, and any required evidence; status visible to applicant
- *Admissions Review* · Power Apps · Staff portal — Admissions staff assess applications, request additional information, record decisions, and manage offer workflows
- *AI Admissions Agent* · Copilot Agent · AI-assisted — Guides applicants through requirements, answers status questions, and flags incomplete applications before submission

**Student actions**
- Title: "Applicant Self-Service"
- Description: What the applicant manages independently through the portal
- Items: Complete and submit the application form; Upload supporting documents; Track application status in real time; Respond to requests for additional information; Accept or decline an offer

**Staff prepare**
- Items: Review submitted applications against eligibility criteria; Request missing documents or clarifications from applicants; Record assessment decisions and recommendations; Generate conditional or unconditional offers; Monitor acceptance deadlines and follow up on outstanding offers

**Outcomes**
- A complete, assessed application record
- Offer issued and acceptance status confirmed
- Any conditions cleared and documented
- Student record created and ready for enrolment

---

### Stage 3 — Enrolment & Onboarding

**Key activities**
- *Course Enrolment* · Power Pages · Self-service — Students select and enrol in their courses/units for the upcoming study period, subject to availability and prerequisites
- *Student Onboarding Portal* · Power Pages · Self-service — Guided onboarding checklist: IT account setup, ID card collection, compliance modules, key dates, and introduction to services
- *Onboarding Administration* · Power Apps · Staff portal — Staff manage student records, confirm enrolment, assign advisors, track onboarding task completion, and flag outstanding items
- *Orientation Agent* · Copilot Agent · AI-assisted — Answers new student questions about campus, systems, and processes; guides students through their onboarding checklist step by step

**Student actions**
- Title: "New Student Self-Service"
- Description: What the new student completes independently to become fully active
- Items: Select and enrol in courses for the study period; Complete online orientation and compliance modules; Set up university IT accounts and systems access; Download student ID and collect physical card; Review timetable and key dates

**Staff prepare**
- Items: Confirm enrolment and activate student record in all systems; Assign personal advisor or faculty contact; Schedule orientation sessions and send invitations; Monitor onboarding checklist completion and follow up on outstanding items; Prepare welcome communications and first-week resources

**Outcomes**
- Active, fully enrolled student record
- All courses confirmed and timetable generated
- Onboarding checklist completed
- Advisor assigned and first contact made
- Student has system access and ID

---

### Stage 4 — Study & Engage

**Key activities**
- *Student Portal* · Power Pages · Self-service — Central hub for timetables, course materials, assessment deadlines, results, and university communications
- *Academic Progress Monitoring* · Power Apps · Staff portal — Staff track attendance, assessment submissions, grades, and academic standing; identify and manage at-risk students
- *Assessment & Results Management* · Power Apps · Staff portal — Record and manage assessment marks, grade approvals, and results publication; manage special consideration requests
- *Study Support Agent* · Copilot Agent · AI-assisted — Answers questions about assessment requirements, deadlines, policies, and study resources; books appointments with advisors; escalates concerns to staff

**Student actions**
- Title: "Student Self-Service"
- Description: What the student manages through the portal during their studies
- Items: View timetable, course information, and assessment deadlines; Submit assignments and track submission status; Check results and academic progress; Book appointments with academic advisors or tutors; Update personal details and communication preferences

**Staff prepare**
- Items: Monitor attendance and flag unexplained absences; Review and submit assessment marks; Identify and proactively contact at-risk students; Process special consideration and extension requests; Prepare and publish results in line with academic calendar

**Outcomes**
- Up-to-date academic record with grades and attendance
- At-risk students identified and intervention initiated
- Assessment results published and communicated
- Progression decisions recorded for each study period

---

### Stage 5 — Graduation

**Key activities**
- *Graduation Application* · Power Pages · Self-service — Students apply to graduate, confirm personal details, select ceremony preferences, and track their application status
- *Completion Audit* · Power Apps · Staff portal — Staff audit course completion requirements, confirm eligibility, manage exceptions, and approve graduation applications
- *Ceremony Management* · Power Apps · Staff portal — Manage ceremony scheduling, guest ticketing, academic dress orders, and on-the-day logistics
- *Graduation Agent* · Copilot Agent · AI-assisted — Answers questions about graduation requirements, ceremony logistics, and document issuance; guides students through the application process

**Student actions**
- Title: "Graduate Self-Service"
- Description: What the graduating student manages independently
- Items: Apply to graduate and confirm personal details; Select preferred ceremony and register attendance; Order academic dress and manage guest tickets; Download digital transcript and access testamur; Update post-graduation contact details

**Staff prepare**
- Items: Run completion audits against each applicant's academic record; Resolve any outstanding requirements or exceptions; Confirm the graduation list and obtain required approvals; Coordinate ceremony logistics — venue, order of proceedings, academic staff; Issue testamurs and official transcripts; Transition completed student records to alumni status

**Outcomes**
- Graduation eligibility confirmed and approved
- Testamur and official transcript issued
- Ceremony attendance recorded
- Student record transitioned to alumni

---

### Stage 6 — Alumni Management

**Key activities**
- *Alumni Portal* · Power Pages · Self-service — Graduates maintain their profile, access benefits, register for events, explore CPD offerings, and connect with the alumni network
- *Alumni Engagement Management* · Power Apps · Staff portal — Staff manage alumni database, plan and execute engagement campaigns, track participation, and manage giving programs
- *Continuing Education & CPD* · Power Pages · Self-service — Alumni browse and enrol in short courses, professional development programs, and postgraduate pathways
- *Alumni Engagement Agent* · Copilot Agent · AI-assisted — Answers questions about alumni benefits, CPD offerings, and events; facilitates reconnection with the university; routes enquiries about postgraduate study to admissions

**Student actions**
- Title: "Alumni Self-Service"
- Description: What alumni manage independently through the portal
- Items: Update contact details and career information; Register for alumni events, reunions, and networking sessions; Browse and enrol in CPD and continuing education programs; Access alumni benefits and discounts; Refer prospective students to the university; Explore postgraduate study options

**Staff prepare**
- Items: Maintain and cleanse the alumni database; Design and send segmented engagement campaigns; Track event attendance and engagement metrics; Manage alumni giving and fundraising programs; Coordinate mentoring and industry networking programs; Identify alumni for postgraduate re-engagement pathways

**Outcomes**
- Active, maintained alumni record with career and engagement history
- Alumni engaged with at least one program or event per year
- Postgraduate and CPD pipeline identified
- Alumni net promoter score and engagement rate tracked

---

## Continuous layer — Student Support

A full-width strip spanning all 6 stage columns at the bottom of the grid. Teal top border, light teal background, clickable.

- **Eyebrow:** "Continuous layer"
- **Title:** "Student Support"
- **Description:** A consistent support layer active from first enquiry through to alumni — covering wellbeing, mental health, financial assistance, disability services, and student advocacy across every stage of the lifecycle.
- **Tags (pills):** Wellbeing · Mental Health · Financial Aid · Disability Services · Student Advocacy · Crisis Support · Complaints · Appeals

**Detail panel content**

What Student Support covers:
- Wellbeing check-ins and proactive outreach to students showing signs of disengagement
- Mental health referrals and case management, including crisis response
- Financial hardship assessment and emergency aid distribution
- Disability support plans — assessment, reasonable adjustments, and review
- Student advocacy — guidance through formal complaints, academic appeals, and misconduct processes
- Peer support programs and community-building initiatives

How it works across stages:
- Stage 1–2: Support services introduced during enquiry and application; accessibility needs captured early
- Stage 3: Support referrals initiated during onboarding for students who disclose needs
- Stage 4: Ongoing monitoring, proactive outreach, and case management during studies
- Stage 5: Wellbeing check-in ahead of graduation; support for students with outstanding needs
- Stage 6: Alumni mental health and career transition support

Built on:
- Power Apps — case management for support staff; referral and triage workflows
- Power Pages — student self-referral forms; support resource hub; appointment booking
- Copilot Studio — 24/7 triage agent; guides students to the right service; escalates urgent cases to on-call staff

---

## Technical requirements

- Single self-contained HTML file — no external JS dependencies (no frameworks)
- All CSS embedded in `<style>` tag; all JS in a `<script>` tag
- Data-driven: stages and content stored in a `STAGES` JS array; grid rendered dynamically via `renderGrid()`
- Grid uses CSS Grid with `grid-template-columns: 76px repeat(6, 1fr)` — 6 stage columns
- Overflow-x scrollable on small screens; min-width 960 px for the grid
- Responsive: panel goes full-width on mobile (`max-width: 768px`)
- Keyboard accessible: cards respond to Enter / Space; Escape closes panel
- XSS-safe: all user-facing strings passed through an `esc()` HTML-escape helper before insertion via `innerHTML`
- Font: Segoe UI (system font — no Google Fonts dependency required)
