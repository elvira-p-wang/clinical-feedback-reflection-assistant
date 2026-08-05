# Clinical Feedback to Action 🩺✨

[![License: MIT](https://img.shields.io/badge/license-MIT-6b4a34.svg)](LICENSE)
![No dependencies](https://img.shields.io/badge/dependencies-none-6b4a34.svg)
![Offline-first](https://img.shields.io/badge/offline--first-yes-6b4a34.svg)

Turns placement feedback into reflections you'll actually finish writing.

A single-file, offline-first educational technology tool that turns raw
feedback from a Clinical Educator, preceptor, or supervisor into a
categorized breakdown, a prioritized action list, and a concise reflective
journal draft — built for students on *any* clinical placement: nursing,
physiotherapy, occupational therapy, pharmacy, dentistry, medicine, and more.

No installation. No backend. No account. Open `index.html` and go.

## Table of Contents

- [Why](#why)
- [Features](#features)
- [Usage](#usage)
- [How it works](#how-it-works)
- [Scope & disclaimer](#scope--disclaimer)
- [Why no AI?](#why-no-ai)
- [Tech stack](#tech-stack)
- [Privacy](#privacy)
- [Project history](#project-history)
- [Contributing](#contributing)
- [License](#license)

## Why

Clinical placement feedback is easy to receive and hard to act on. It
usually arrives as a wall of loosely-structured bullet points (or plain
paragraphs) mixing praise, corrections, compliance warnings, and one-off
observations. Turning that into a genuinely useful reflective journal entry
— the kind that actually changes what you do next time — takes more effort
than most students have time for between patients.

This tool does the sorting for you: paste the feedback, get back what
matters, ranked by urgency, with a reflection draft you only need to add
your real feelings to.

## Features

- **Paste anything** — bullet points (`•`, `-`, `*`), numbered lists, blank-line-separated paragraphs, or a single wall of plain prose. The parser figures out how to split it.
- **Auto-categorization** into eight placement-relevant themes: professionalism & compliance, patient safety & escalation, history taking & medical complexity, documentation & medico-legal notes, clinical skills & treatment planning, patient & family communication, patient education & preventive advice, and case complexity & time management.
- **Sentiment tagging** — each point is flagged as a Strength, a Growth Area, or plain Context.
- **Condition-aware follow-up questions** — mentions of epilepsy, asthma, diabetes, or allergy in a growth area auto-generate a tailored follow-up question checklist for that condition.
- **Priority-ranked action list** — growth areas ranked by urgency (compliance and patient safety first), each with a one-line rationale and a concrete next step.
- **Concise, keyword-driven reflective draft** — Went Well / Needs Improvement / Action Plan / Feelings / Key Takeaway. Distilled to the key point per item, short enough to scan in seconds, fully editable, with an explicit prompt to add your own genuine feelings (no tool can generate that part for you).
- **History & trends** — saved entries are tracked in local storage, surfacing which themes keep recurring across placements over time.
- **Copy / download / export** — grab the reflection as plain text, or export your whole history as JSON for backup.
- **Score Tracker** — log each session's ratings against a weighted rubric (default: University of Sydney BOH2/BOH3, 4 domains) and see a running weighted-average grade, verified against the university's own worked example.
- **Competency Tracker** — a checklist of clinical competencies, grouped by category, with a running completion percentage.
- **Configurable rubric/competency profile** — the rating scale, weighted domains, and competency list all live in one swappable `ACTIVE_PROFILE` object, so a different placement's rubric and competency book can replace the default without touching the rest of the app.
- **Outlook CE feedback import** — paste a Clinical Educator feedback email (the Power Automate template) straight into the Feedback box and it's recognized automatically: domain ratings are pre-filled into the Score Tracker, achieved competencies are matched against the checklist and staged for completion, critical-error flags are surfaced, and the free-text comments flow through the normal parser — all confirmed together with one click of Save. Matching favors the CE's written description over a typed competency code, since codes get mistyped more often than procedures get misdescribed, and section boundaries are found by locating the next known field label rather than relying on blank lines, since real Outlook-to-textarea pastes can drop them entirely.

## Usage

1. Download or clone this repo.
2. Open `index.html` in any browser — double-click it, or drag it into a tab.
3. Paste your feedback, click **Parse & Generate Reflection**.

To develop further, just open the folder in your editor of choice — it's
plain HTML/CSS/JS with zero dependencies and no build tooling required.

Want a shareable link instead of a local file? Enable **GitHub Pages** on
this repo (Settings → Pages → Deploy from branch → `main`) and you'll get a
live URL.

## How it works

Everything runs client-side, in three passes over the pasted text:

1. **Split** — the text is broken into individual feedback points, detecting whichever format was used (bullets, numbers, paragraphs, or prose).
2. **Classify** — each point is scored against a keyword dictionary for eight categories, and tagged as a Strength, Growth Area, or Context based on linguistic cues (e.g. "please ensure," "breach," "well done").
3. **Distill** — text is cleaned up (stray symbols, repeated punctuation, filler openers stripped) and trimmed to a key phrase, so the breakdown and the reflection draft show the gist, not a wall of quotes.
4. **Synthesize** — growth areas are ranked by category priority and used to generate both the priority action list and the reflective journal draft, with condition-specific detail inserted where relevant.

## Scope & disclaimer

The feedback parser, categorization, and reflection draft (sections 01–06)
are discipline-agnostic and work for any clinical placement out of the box.

The **Score Tracker** and **Competency Tracker** (sections 07–08) are a
different story: they currently ship with the University of Sydney BOH2/BOH3
rubric and competency book (2026 cohort) as the tool's one built-in default,
read through a single swappable `ACTIVE_PROFILE` object. Support for
generating a custom profile for other professions', cohorts', or
institutions' rubrics and competency books — from their own PDFs — is on the
roadmap but **not yet available**. Until then, the Score Tracker and
Competency Tracker are only meaningful if your rubric and competency list
actually match the built-in default; everyone else should treat sections
01–06 as the useful part.

Pass thresholds and rubric weights shown are defaults set from the public
BOH2/BOH3 rubric and should be confirmed against your own unit outline —
this project isn't an official University of Sydney tool and carries no
institutional endorsement.

## Why no AI?

This is deliberately **not** an AI product. Classification and summarization
run on transparent, inspectable string rules — no LLM, no cloud API, no
model calls. You can read every rule that decides your category in
`index.html` yourself.

That's a trade-off, not an oversight: real natural-language understanding
(especially across languages) would need a hosted model, which means your
feedback would leave your browser and travel to a third-party API. For a
tool that handles other people's private assessments of your clinical
performance, offline and inspectable felt like the right default. If you
want to fork this and bolt on an LLM for true multilingual summarization,
the parsing/classification layer is small and easy to swap out.

## Tech stack

Vanilla HTML, CSS, and JavaScript. No frameworks, no package manager, no
build step. Data persistence uses the browser's `localStorage`.

## Privacy

There is no server component and no account — everything runs in your
browser. All data (pasted feedback, saved history, scores, competency
progress) stays in your browser's local storage on your own device. Nothing
is sent to me, and no AI provider is ever involved in classification or
reflection generation.

The one exception is the optional **Speak** (voice input) button: it uses
your browser's built-in speech recognition, which sends audio to your
browser vendor's speech service (e.g. Google, for Chrome) for transcription
— not local, and not this project's choice to make otherwise, since that's
how the browser API works. It's off by default and clearly labelled in the
app; typing/pasting stays fully offline as described above.

## Project history

Built incrementally; see the commit history for the full build order: data
model → parsing/classification → categorized breakdown → priority actions →
reflective draft generation → history/trends → utilities → flexible input
parsing → cross-discipline category taxonomy → voice input → visual redesign
→ configurable rubric/competency profile → Score Tracker → Competency
Tracker → Outlook CE feedback import.

## Contributing

This started as a personal tool, but issues and pull requests are welcome —
particularly more condition-specific question banks, additional placement
categories, or export formats.

## License

MIT — see [LICENSE](LICENSE).
