# Erasmus+ Statspage — Design Spec
**Date:** 2026-06-19
**Project:** Erasmus+ w Liceum w Dubience: Nowe Możliwości dla Uczniów i Nauczycieli
**Project no.:** 2025-1-PL01-KA122-SCH-000322073

---

## Overview

A single `index.html` GitHub Pages site that visualises survey results from 7 evaluation PDFs collected during the Erasmus+ KA122-SCH mobility programme at Liceum Ogólnokształcące im. 27 Wołyńskiej Dywizji AK w Dubience.

Language: **Polish** (matches source documents).
Deployment: GitHub Pages, no build step required.

---

## Data Sources

All data is read from PDFs in `/files/` and hardcoded as JS constants in `index.html`.

| Survey | Respondents | Questions |
|--------|-------------|-----------|
| Rekrutacja | 24 | 10 scale + 2 open |
| Praca zespołu projektowego | 15 | 9 scale + 1 open |
| Przygotowanie językowe – angielski (10h) | 15 | 11 scale + 2 open + 1 yes/no |
| Przygotowanie językowe – włoski (4h) | 15 | 11 scale + 2 open + 1 yes/no |
| Spotkania organizacyjne (2h) | 15 | 10 scale + 2 open + 1 yes/no |
| Spotkania kulturowe (2h) | 15 | 11 scale + 2 open + 1 yes/no |
| Ankieta ewaluacyjna – Włochy | 15 | Parts A–F (multi-section) |

---

## Architecture

Single file: `index.html`
- Inline CSS (no external stylesheet)
- Chart.js loaded from CDN (`https://cdn.jsdelivr.net/npm/chart.js`)
- All survey data as hardcoded JS constants
- Vanilla JS tab switching

---

## Visual Design

**Colour palette:**
- Primary blue: `#003DA5` (Erasmus+/EU)
- Accent gold: `#FFD700`
- Background: `#f4f6fb`
- Card background: `#ffffff`
- Score gradient: `#d32f2f` (1) → `#f57c00` (2) → `#fbc02d` (3) → `#689f38` (4) → `#2e7d32` (5)

**Header:** Project title, EU emblem colours, project number in small print.

**Tab bar:** 8 tabs — Podsumowanie + one per survey. Active tab highlighted in primary blue.

---

## Tab Designs

### Tab 0 — Podsumowanie (Overview)
- 7 stat cards (one per survey): survey name, respondent count, average score across all questions
- One horizontal bar chart comparing average scores across all 7 surveys

### Tabs 1–6 — Individual Surveys (scale 1–5)
Per tab:
- KPI row: respondent count, average score, % who gave 5
- One **horizontal stacked bar per question**: segments coloured by score 1–5, labelled with percentages
- Yes/No questions (where present): **donut chart** (e.g. "100% tak")
- Open-ended answers: **styled quote cards** with the collected text

### Tab 7 — Ankieta ewaluacyjna – Włochy
- Grouped by parts A (English), B (Intercultural), C (Organisation), E (Overall)
- Same stacked bar layout per section
- Part F (post-return plans): horizontal bar chart showing % per intention

---

## Responsiveness

- Mobile-first, uses CSS flexbox/grid
- Tab bar scrolls horizontally on small screens
- Charts use `max-width: 100%` and `responsive: true` in Chart.js config

---

## Constraints & Non-Goals

- No server-side logic; fully static
- No PDF parsing at runtime — data is hardcoded from pre-read PDFs
- No filtering, sorting, or user input beyond tab switching
- No authentication
