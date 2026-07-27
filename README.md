# Clinical Feedback Reflection Assistant

A single-file, offline-first web app that turns raw Clinical Educator (CE)
feedback into a structured, high-signal reflective journal entry — built for
dental/medical students on clinical placement.

## What it does

1. **Paste** raw CE/educator feedback (bullet points or plain paragraphs).
2. **Auto-categorizes** each point into themes: professionalism & compliance,
   history taking & medical complexity, documentation & medico-legal notes,
   clinical skills & treatment planning, patient/parent communication, oral
   hygiene & preventive advice, and case complexity & time management.
3. **Flags** each point as a Strength, Growth Area, or Context. For growth
   areas involving a recognized medical condition (epilepsy, asthma,
   diabetes, allergy, etc.), it auto-generates a tailored follow-up question
   checklist.
4. **Ranks** growth areas by urgency (compliance/medico-legal first) into a
   Top Priority Actions list, each with a one-line rationale and a concrete
   action.
5. **Generates** a concise reflective journal draft (Went Well / Needs
   Improvement / Action Plan / Feelings / Key Takeaway) — short enough to
   scan in seconds, fully editable, with an explicit prompt to add your own
   genuine feelings (no tool can generate that part for you).
6. **Tracks history and trends** in the browser's local storage, so recurring
   themes across placements/appointments become visible over time.

No backend, no build step, no external services — everything runs
client-side in the browser.

## Usage

Open `index.html` directly in a browser (double-click, or drag into a
browser tab). To develop further, open this folder in VS Code — it's plain
HTML/CSS/JS with zero dependencies and no build tooling required.

You can also enable **GitHub Pages** on this repo (Settings → Pages → Deploy
from branch → `main`) to get a shareable live link.

## Privacy

All data (pasted feedback, saved history) stays in your browser's local
storage on your own device. Nothing is sent anywhere.

## Project history

This was built incrementally — see the commit history for the build order:
data model → parsing/classification → categorized breakdown → priority
actions → reflective draft generation → history/trends → utilities.
