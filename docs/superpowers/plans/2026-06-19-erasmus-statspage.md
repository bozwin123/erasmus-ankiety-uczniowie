# Erasmus+ Statspage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single `index.html` GitHub Pages site visualising 7 Erasmus+ survey PDFs with a tabbed dashboard in Polish.

**Architecture:** One self-contained `index.html` — inline CSS, Chart.js from CDN, all survey data as hardcoded JS constants, vanilla JS tab switching. No build step required.

**Tech Stack:** HTML5, CSS3 (flexbox/grid), Chart.js 4.x (CDN), vanilla JS ES6.

## Global Constraints

- Language: Polish throughout (labels, tooltips, headings)
- Primary colour: `#003DA5` (Erasmus+ blue); Accent: `#FFD700` (EU gold)
- Score colour gradient: 1=`#d32f2f`, 2=`#f57c00`, 3=`#fbc02d`, 4=`#689f38`, 5=`#2e7d32`
- Single file: `index.html` at repo root
- No external fonts, no build tools — Chart.js loaded from `https://cdn.jsdelivr.net/npm/chart.js`
- Responsive: mobile-first, tab bar scrolls on small screens
- GitHub Pages deployable: add `.nojekyll` at repo root

---

## File Structure

```
/
├── index.html          ← entire app (HTML + inline CSS + inline JS)
└── .nojekyll           ← tells GitHub Pages to skip Jekyll processing
```

---

## Survey Data Reference

All percentage values used in code below are pre-calculated from the PDFs.
Format: `[p1, p2, p3, p4, p5]` where each value is the % of respondents who chose that score.

### Survey 1 – Rekrutacja (n=24)
```
Q labels: [
  'Wartość merytoryczna dokumentów rekrutacyjnych',
  'Metody prowadzenia rekrutacji',
  'Jasność i przejrzystość zasad rekrutacji',
  'Kontakt Komisji Rekrutacyjnej z kandydatami',
  'Zachowanie zasady równości szans',
  'Zachowanie zasady niedyskryminacji',
  'Dostępność dokumentów rekrutacyjnych',
  'Jakość poinformowania o wynikach rekrutacji',
  'Kompleksowość działań rekrutacyjnych',
  'Bezpieczeństwo danych w toku rekrutacji',
]
Q data: [
  [4.2,  0,   0,   8.3,  87.5],
  [0,    0,   4.2, 12.5, 83.3],
  [0,    0,   4.2, 8.3,  87.5],
  [0,    0,   0,   4.2,  95.8],
  [0,    0,   4.2, 20.8, 75.0],
  [0,    0,   0,   8.3,  91.7],
  [0,    0,   0,   8.3,  91.7],
  [0,    0,   0,   4.2,  95.8],
  [0,    0,   4.2, 8.3,  87.5],
  [0,    0,   0,   4.2,  95.8],
]
```

### Survey 2 – Praca zespołu projektowego (n=15)
```
Q labels: [
  'Jakość dokumentów zespołu projektowego',
  'Metody pracy zespołu projektowego',
  'Jasność i przejrzystość zasad działania',
  'Kontakt zespołu z uczestnikami',
  'Zachowanie zasady równości szans',
  'Zachowanie zasady niedyskryminacji',
  'Dostępność i bezpieczeństwo informacji',
  'Zaangażowanie Partnera zagranicznego',
  'Kompleksowość działań zespołu',
]
Q data: [
  [0, 0,   0,   0,   100 ],
  [0, 0,   0,   0,   100 ],
  [0, 0,   0,   0,   100 ],
  [0, 0,   6.7, 6.7, 86.7],
  [0, 0,   6.7, 0,   93.3],
  [0, 0,   0,   6.7, 93.3],
  [0, 0,   0,   6.7, 93.3],
  [0, 6.7, 0,   0,   93.3],
  [0, 0,   0,   6.7, 93.3],
]
```

### Survey 3 – Angielski 10h (n=15)
```
Q labels: [
  'Wartość merytoryczna zajęć',
  'Metody prowadzenia zajęć',
  'Przygotowanie merytoryczne prowadzącego',
  'Kontakt z uczestnikami zajęć',
  'Jakość wykorzystywanych materiałów',
  'Jakość przeprowadzonych zajęć',
  'Skład merytoryczny dokumentów',
  'Różnorodność metod dydaktycznych',
  'Uniwersalność przekazywanych treści',
  'Kompleksowość przeprowadzonych zajęć',
  'Kompatybilność zajęć z celami projektu',
]
Q data: [
  [0, 0, 0,   6.7, 93.3],
  [0, 0, 0,   0,   100 ],
  [0, 0, 6.7, 0,   93.3],
  [0, 0, 0,   6.7, 93.3],
  [0, 0, 0,   0,   100 ],
  [0, 0, 0,   6.7, 93.3],
  [0, 0, 0,   6.7, 93.3],
  [0, 0, 0,   0,   100 ],
  [0, 0, 6.7, 0,   93.3],
  [0, 0, 6.7, 0,   93.3],
  [0, 0, 0,   6.7, 93.3],
]
yesNo: 100% tak
```

### Survey 4 – Włoski 4h (n=15)
```
Q labels: [
  'Wartość merytoryczna zajęć',
  'Metody prowadzenia zajęć',
  'Przygotowanie merytoryczne prowadzącego',
  'Kontakt z uczestnikami zajęć',
  'Jakość wykorzystywanych materiałów',
  'Jakość przeprowadzonych zajęć',
  'Skład merytoryczny dokumentów',
  'Różnorodność metod dydaktycznych',
  'Uniwersalność przekazywanych treści',
  'Kompleksowość przeprowadzonych zajęć',
  'Kompatybilność zajęć z celami projektu',
]
Q data: [
  [0, 0,   0,   13.3, 86.7],
  [0, 0,   0,   6.7,  93.3],
  [0, 0,   6.7, 0,    93.3],
  [0, 0,   0,   6.7,  93.3],
  [0, 0,   0,   6.7,  93.3],
  [0, 0,   0,   0,    100 ],
  [0, 0,   6.7, 0,    93.3],
  [0, 0,   6.7, 0,    93.3],
  [0, 0,   6.7, 6.7,  86.7],
  [0, 6.7, 0,   6.7,  86.7],
  [0, 0,   0,   6.7,  93.3],
]
yesNo: 100% tak
```

### Survey 5 – Spotkania organizacyjne 2h (n=15)
```
Q labels: [
  'Wartość merytoryczna zajęć',
  'Metody prowadzenia zajęć',
  'Przygotowanie merytoryczne prowadzącego',
  'Kontakt z uczestnikami zajęć',
  'Jakość wykorzystywanych materiałów',
  'Jakość przeprowadzonych zajęć',
  'Różnorodność metod dydaktycznych',
  'Uniwersalność przekazywanych treści',
  'Kompleksowość przeprowadzonych zajęć',
  'Kompatybilność zajęć z celami projektu',
]
Q data: [
  [0, 0, 0,   0,    100 ],
  [0, 0, 0,   6.7,  93.3],
  [0, 0, 0,   6.7,  93.3],
  [0, 0, 6.7, 6.7,  86.7],
  [0, 0, 0,   13.3, 86.7],
  [0, 0, 0,   6.7,  93.3],
  [0, 0, 0,   6.7,  93.3],
  [0, 0, 0,   6.7,  93.3],
  [0, 0, 0,   13.3, 86.7],
  [0, 0, 6.7, 0,    93.3],
]
yesNo: 100% tak
```

### Survey 6 – Spotkania kulturowe 2h (n=15)
```
Q labels: [
  'Wartość merytoryczna zajęć',
  'Metody prowadzenia zajęć',
  'Przygotowanie merytoryczne prowadzącego',
  'Kontakt z uczestnikami zajęć',
  'Jakość wykorzystywanych materiałów',
  'Jakość przeprowadzonych zajęć',
  'Skład merytoryczny dokumentów',
  'Różnorodność metod dydaktycznych',
  'Uniwersalność przekazywanych treści',
  'Kompleksowość przeprowadzonych zajęć',
  'Kompatybilność zajęć z celami projektu',
]
Q data: [
  [0, 0,   0,   0,    100 ],
  [0, 0,   6.7, 6.7,  86.7],
  [0, 0,   0,   0,    100 ],
  [0, 0,   0,   6.7,  93.3],
  [0, 0,   0,   6.7,  93.3],
  [0, 0,   0,   6.7,  93.3],
  [0, 0,   0,   6.7,  93.3],
  [0, 0,   6.7, 6.7,  86.7],
  [0, 0,   0,   0,    100 ],
  [0, 0,   0,   0,    100 ],
  [0, 0,   0,   13.3, 86.7],
]
yesNo: 100% tak
```

### Survey 7 – Ankieta ewaluacyjna po mobilności (n=15)

**Part A – Komunikacja w języku angielskim**
Scale: 1=Zdecydowanie nie … 5=Zdecydowanie tak
```
labels: [
  'Lepsza umiejętność rozumienia ang. ze słuchu',
  'Swobodne porozumiewanie się po angielsku',
  'Pewność siebie w mówieniu po angielsku',
  'Wzbogacenie słownictwa angielskiego',
  'Motywacja do nauki angielskiego',
  'Szansa na lepszy wynik matury z ang.',
  'Chęć do egzaminu certyfikacyjnego (FCE/CAE)',
]
data: [
  [0, 0, 0,    26.7, 73.3],
  [0, 0, 6.7,  13.3, 80  ],
  [0, 0, 6.7,  6.7,  86.7],
  [0, 0, 13.3, 20,   66.7],
  [0, 0, 0,    20,   80  ],
  [0, 0, 0,    6.7,  93.3],
  [0, 0, 20,   6.7,  73.3],
]
```

**Part B – Świadomość międzykulturowa**
```
labels: [
  'Lepsza znajomość kultury i tradycji Włoch',
  'Większa otwartość na kontakty z innymi',
  'Efektywna współpraca w międzynar. zespole',
  'Radzenie sobie w nowych sytuacjach',
  'Lepsze rozumienie UE i jej możliwości',
  'Wzmocnienie tolerancji kulturowej',
  'Chęć angażowania się w projekty międzynar.',
]
data: [
  [0, 0, 0,   0,    100 ],
  [0, 0, 0,   13.3, 86.7],
  [0, 0, 0,   26.7, 73.3],
  [0, 0, 6.7, 0,    93.3],
  [0, 0, 6.7, 33.3, 60  ],
  [0, 0, 6.7, 6.7,  86.7],
  [0, 0, 0,   26.7, 73.3],
]
```

**Part C – Organizacja i przebieg mobilności**
```
labels: [
  'Dobre przygotowanie przez szkołę',
  'Ciekawe i angażujące zajęcia',
  'Poczucie bezpieczeństwa z opiekunami',
  'Zakwaterowanie i wyżywienie',
  'Dobrze zorganizowany program',
  'Poleciłbym/-abym wyjazd innym',
]
data: [
  [0, 0, 0,   13.3, 86.7],
  [0, 0, 6.7, 6.7,  86.7],
  [0, 0, 0,   0,    100 ],
  [0, 0, 6.7, 26.7, 66.7],
  [0, 0, 0,   6.7,  93.3],
  [0, 0, 0,   6.7,  93.3],
]
```

**Part E – Ogólna ocena mobilności**
```
labels: [
  'Ogólna jakość mobilności',
  'Własny rozwój językowy',
  'Własny rozwój osobisty',
  'Przygotowanie przez szkołę',
]
data: [
  [0, 0, 0,   13.3, 86.7],
  [0, 0, 0,   13.3, 86.7],
  [0, 0, 6.7, 20,   73.3],
  [0, 0, 0,   13.3, 86.7],
]
```

**Part F – Plany po powrocie (%)**
```
labels: [
  'Egzamin certyfikacyjny (FCE/CAE)',
  'Rozszerzona matura z angielskiego',
  'Szkolne koło językowe/debatanckie',
  'Kolejny projekt Erasmus+ / międzynar.',
  'Kontakty z uczniami za granicą',
  'Nauka języka włoskiego',
  'Wolontariat lub inicjatywy międzynar.',
]
values: [40, 46.7, 16.7, 66.7, 26.7, 20, 20]
```

---

## Task 1: HTML Scaffold + CSS

**Files:**
- Create: `index.html`

**Interfaces:**
- Produces: DOM structure consumed by Tasks 2–5

- [ ] **Step 1: Create `index.html` with full scaffold**

```html
<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Erasmus+ Ankiety – Liceum w Dubience</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  :root {
    --blue: #003DA5;
    --gold: #FFD700;
    --bg: #f4f6fb;
    --card: #ffffff;
    --text: #1a1a2e;
    --muted: #6b7280;
    --c1: #d32f2f;
    --c2: #f57c00;
    --c3: #fbc02d;
    --c4: #689f38;
    --c5: #2e7d32;
    --radius: 12px;
    --shadow: 0 2px 12px rgba(0,0,0,0.08);
  }
  body { font-family: system-ui, -apple-system, sans-serif; background: var(--bg); color: var(--text); }

  /* HEADER */
  header {
    background: var(--blue);
    color: #fff;
    padding: 24px 32px 20px;
    border-bottom: 4px solid var(--gold);
  }
  header .eu-flag { font-size: 2rem; margin-bottom: 6px; }
  header h1 { font-size: 1.4rem; font-weight: 700; line-height: 1.3; }
  header .sub { font-size: 0.8rem; opacity: 0.75; margin-top: 4px; }

  /* TAB BAR */
  .tab-bar {
    background: #fff;
    border-bottom: 1px solid #e5e7eb;
    display: flex;
    overflow-x: auto;
    scrollbar-width: none;
    position: sticky;
    top: 0;
    z-index: 10;
  }
  .tab-bar::-webkit-scrollbar { display: none; }
  .tab-btn {
    flex-shrink: 0;
    padding: 14px 20px;
    border: none;
    background: none;
    cursor: pointer;
    font-size: 0.85rem;
    font-weight: 500;
    color: var(--muted);
    border-bottom: 3px solid transparent;
    transition: color 0.2s, border-color 0.2s;
    white-space: nowrap;
  }
  .tab-btn.active { color: var(--blue); border-bottom-color: var(--blue); }
  .tab-btn:hover:not(.active) { color: var(--text); }

  /* PANELS */
  .tab-panel { display: none; padding: 32px 24px; max-width: 1100px; margin: 0 auto; }
  .tab-panel.active { display: block; }

  /* KPI ROW */
  .kpi-row { display: flex; flex-wrap: wrap; gap: 16px; margin-bottom: 32px; }
  .kpi-card {
    background: var(--card);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    padding: 20px 24px;
    flex: 1 1 160px;
    min-width: 140px;
  }
  .kpi-card .label { font-size: 0.75rem; color: var(--muted); text-transform: uppercase; letter-spacing: 0.05em; margin-bottom: 6px; }
  .kpi-card .value { font-size: 2rem; font-weight: 700; color: var(--blue); }
  .kpi-card .unit { font-size: 0.85rem; color: var(--muted); margin-top: 2px; }

  /* CHART CARDS */
  .chart-card {
    background: var(--card);
    border-radius: var(--radius);
    box-shadow: var(--shadow);
    padding: 24px;
    margin-bottom: 24px;
  }
  .chart-card h3 { font-size: 1rem; font-weight: 600; margin-bottom: 16px; color: var(--text); }
  .chart-card h4 { font-size: 0.85rem; font-weight: 600; margin-bottom: 12px; color: var(--muted); text-transform: uppercase; letter-spacing: 0.05em; }

  /* SCORE LEGEND */
  .score-legend { display: flex; gap: 16px; flex-wrap: wrap; margin-bottom: 16px; font-size: 0.75rem; }
  .score-legend span { display: flex; align-items: center; gap: 5px; }
  .score-legend i { width: 12px; height: 12px; border-radius: 2px; display: inline-block; }

  /* DONUT ROW */
  .donut-row { display: flex; flex-wrap: wrap; gap: 24px; align-items: center; }
  .donut-wrap { position: relative; width: 120px; height: 120px; }
  .donut-label { text-align: center; font-size: 0.8rem; color: var(--muted); margin-top: 8px; max-width: 120px; }

  /* QUOTE CARDS */
  .quotes { display: flex; flex-wrap: wrap; gap: 12px; }
  .quote {
    background: var(--bg);
    border-left: 3px solid var(--gold);
    padding: 10px 14px;
    border-radius: 0 8px 8px 0;
    font-size: 0.85rem;
    font-style: italic;
    color: var(--text);
    flex: 1 1 200px;
  }

  /* YES/NO BADGE */
  .yesno-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: #e8f5e9;
    border: 1px solid var(--c5);
    border-radius: 100px;
    padding: 8px 18px;
    font-weight: 600;
    color: var(--c5);
    font-size: 0.9rem;
    margin-top: 8px;
  }

  /* SECTION DIVIDER */
  .section-divider {
    border: none;
    border-top: 1px solid #e5e7eb;
    margin: 28px 0;
  }

  @media (max-width: 600px) {
    header { padding: 16px; }
    header h1 { font-size: 1.1rem; }
    .tab-panel { padding: 16px 12px; }
    .kpi-card .value { font-size: 1.5rem; }
  }
</style>
</head>
<body>

<header>
  <div class="eu-flag">🇪🇺</div>
  <h1>Erasmus+ w Liceum w Dubience<br><span style="font-weight:400;font-size:1rem">Nowe Możliwości dla Uczniów i Nauczycieli</span></h1>
  <div class="sub">nr projektu: 2025-1-PL01-KA122-SCH-000322073 &nbsp;·&nbsp; Wyniki ankiet ewaluacyjnych</div>
</header>

<nav class="tab-bar" role="tablist">
  <button class="tab-btn active" data-tab="overview" role="tab">📊 Podsumowanie</button>
  <button class="tab-btn" data-tab="rekrutacja" role="tab">Rekrutacja</button>
  <button class="tab-btn" data-tab="zespol" role="tab">Praca zespołu</button>
  <button class="tab-btn" data-tab="angielski" role="tab">Angielski 10h</button>
  <button class="tab-btn" data-tab="wloski" role="tab">Włoski 4h</button>
  <button class="tab-btn" data-tab="organizacyjne" role="tab">Org. 2h</button>
  <button class="tab-btn" data-tab="kulturowe" role="tab">Kulturowe 2h</button>
  <button class="tab-btn" data-tab="ewaluacja" role="tab">Po wyjeździe 🇮🇹</button>
</nav>

<div id="overview" class="tab-panel active"></div>
<div id="rekrutacja" class="tab-panel"></div>
<div id="zespol" class="tab-panel"></div>
<div id="angielski" class="tab-panel"></div>
<div id="wloski" class="tab-panel"></div>
<div id="organizacyjne" class="tab-panel"></div>
<div id="kulturowe" class="tab-panel"></div>
<div id="ewaluacja" class="tab-panel"></div>

<script>
// ── TAB SWITCHING ──────────────────────────────────────────────────────────
document.querySelectorAll('.tab-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
    document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
    btn.classList.add('active');
    document.getElementById(btn.dataset.tab).classList.add('active');
  });
});

// ── SHARED COLOURS ─────────────────────────────────────────────────────────
const SCORE_COLORS = ['#d32f2f','#f57c00','#fbc02d','#689f38','#2e7d32'];
const SCORE_LABELS = ['1 – niedostatecznie','2 – mało zad.','3 – dostatecznie','4 – dobrze','5 – bardzo dobrze'];

// PLACEHOLDER FOR DATA + RENDER CALLS (Tasks 2–5)
</script>
</body>
</html>
```

- [ ] **Step 2: Verify file renders in browser**

Open `index.html` directly in a browser (`open index.html` on macOS or `start index.html` on Windows). Expected: blue Erasmus+ header, 8 tabs in nav bar, blank white body. No console errors.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: scaffold Erasmus+ statspage HTML/CSS and tab switching"
```

---

## Task 2: Survey Data Constants

**Files:**
- Modify: `index.html` — replace the `// PLACEHOLDER FOR DATA` comment with the JS constants block below

**Interfaces:**
- Produces: global `SURVEYS` array consumed by Tasks 3–5

- [ ] **Step 1: Replace the placeholder comment with the data block**

Find the line:
```javascript
// PLACEHOLDER FOR DATA + RENDER CALLS (Tasks 2–5)
```

Replace it with:

```javascript
// ── SURVEY DATA ────────────────────────────────────────────────────────────
// Each survey: { id, title, n, questions:[{label,pct:[p1,p2,p3,p4,p5]}], yesNo, openQ }
// pct values are percentages (sum to ~100 per question)

const SURVEYS = [
  {
    id: 'rekrutacja',
    title: 'Procedura rekrutacyjna',
    n: 24,
    questions: [
      { label: 'Wartość merytoryczna dokumentów rekrutacyjnych',      pct: [4.2,  0,   0,   8.3,  87.5] },
      { label: 'Metody prowadzenia rekrutacji',                        pct: [0,    0,   4.2, 12.5, 83.3] },
      { label: 'Jasność i przejrzystość zasad rekrutacji',             pct: [0,    0,   4.2, 8.3,  87.5] },
      { label: 'Kontakt Komisji Rekrutacyjnej z kandydatami',          pct: [0,    0,   0,   4.2,  95.8] },
      { label: 'Zachowanie zasady równości szans',                     pct: [0,    0,   4.2, 20.8, 75.0] },
      { label: 'Zachowanie zasady niedyskryminacji',                   pct: [0,    0,   0,   8.3,  91.7] },
      { label: 'Dostępność dokumentów rekrutacyjnych',                 pct: [0,    0,   0,   8.3,  91.7] },
      { label: 'Jakość poinformowania o wynikach rekrutacji',          pct: [0,    0,   0,   4.2,  95.8] },
      { label: 'Kompleksowość działań rekrutacyjnych',                 pct: [0,    0,   4.2, 8.3,  87.5] },
      { label: 'Bezpieczeństwo danych w toku rekrutacji',              pct: [0,    0,   0,   4.2,  95.8] },
    ],
    yesNo: null,
    openQ: [
      { q: 'Najbardziej podobało mi się', answers: ['atmosfera','rozmowa kwalifikacyjna','ogólnie fajnie','wszystko mi się podobało','przemiła atmosfera','bardzo miłe zachowanie','rozmowa kwalifikacyjna','miła atmosfera i super koordynatorki','test pisemny','atmosfera panująca podczas rekrutacji','duch rywalizacji','angielski'] },
      { q: 'Najbardziej nie podobało mi się', answers: ['nic','nic','niedostanie się'] },
    ],
  },
  {
    id: 'zespol',
    title: 'Praca zespołu projektowego',
    n: 15,
    questions: [
      { label: 'Jakość dokumentów przygotowanych przez zespół',  pct: [0, 0,   0,   0,   100 ] },
      { label: 'Metody pracy zespołu projektowego',              pct: [0, 0,   0,   0,   100 ] },
      { label: 'Jasność i przejrzystość zasad działania',        pct: [0, 0,   0,   0,   100 ] },
      { label: 'Kontakt zespołu z uczestnikami',                 pct: [0, 0,   6.7, 6.7, 86.7] },
      { label: 'Zachowanie zasady równości szans',               pct: [0, 0,   6.7, 0,   93.3] },
      { label: 'Zachowanie zasady niedyskryminacji',             pct: [0, 0,   0,   6.7, 93.3] },
      { label: 'Dostępność i bezpieczeństwo informacji',         pct: [0, 0,   0,   6.7, 93.3] },
      { label: 'Zaangażowanie Partnera zagranicznego',           pct: [0, 6.7, 0,   0,   93.3] },
      { label: 'Kompleksowość działań zespołu',                  pct: [0, 0,   0,   6.7, 93.3] },
    ],
    yesNo: null,
    openQ: [
      { q: 'Uwagi do pracy zespołu projektowego', answers: ['bardzo dobry kontakt'] },
    ],
  },
  {
    id: 'angielski',
    title: 'Przygotowanie językowe – angielski (10h)',
    n: 15,
    questions: [
      { label: 'Wartość merytoryczna zajęć',               pct: [0, 0, 0,   6.7, 93.3] },
      { label: 'Metody prowadzenia zajęć',                 pct: [0, 0, 0,   0,   100 ] },
      { label: 'Przygotowanie merytoryczne prowadzącego',  pct: [0, 0, 6.7, 0,   93.3] },
      { label: 'Kontakt z uczestnikami zajęć',             pct: [0, 0, 0,   6.7, 93.3] },
      { label: 'Jakość wykorzystywanych materiałów',       pct: [0, 0, 0,   0,   100 ] },
      { label: 'Jakość przeprowadzonych zajęć',            pct: [0, 0, 0,   6.7, 93.3] },
      { label: 'Skład merytoryczny dokumentów',            pct: [0, 0, 0,   6.7, 93.3] },
      { label: 'Różnorodność metod dydaktycznych',         pct: [0, 0, 0,   0,   100 ] },
      { label: 'Uniwersalność przekazywanych treści',      pct: [0, 0, 6.7, 0,   93.3] },
      { label: 'Kompleksowość przeprowadzonych zajęć',     pct: [0, 0, 6.7, 0,   93.3] },
      { label: 'Kompatybilność z celami projektu',         pct: [0, 0, 0,   6.7, 93.3] },
    ],
    yesNo: { tak: 100, question: 'Czy zajęcia pozytywnie wpłynęły na przygotowanie językowe?' },
    openQ: [
      { q: 'Najbardziej podobało mi się', answers: ['wszystko mi się podobało','zadania','dobrze wytłumaczone','inny sposób nauczania','organizacja','zadania','sposób przeprowadzania – materiały i zadania'] },
      { q: 'Najbardziej nie podobało mi się', answers: ['nic'] },
    ],
  },
  {
    id: 'wloski',
    title: 'Przygotowanie językowe – włoski (4h)',
    n: 15,
    questions: [
      { label: 'Wartość merytoryczna zajęć',               pct: [0, 0,   0,    13.3, 86.7] },
      { label: 'Metody prowadzenia zajęć',                 pct: [0, 0,   0,    6.7,  93.3] },
      { label: 'Przygotowanie merytoryczne prowadzącego',  pct: [0, 0,   6.7,  0,    93.3] },
      { label: 'Kontakt z uczestnikami zajęć',             pct: [0, 0,   0,    6.7,  93.3] },
      { label: 'Jakość wykorzystywanych materiałów',       pct: [0, 0,   0,    6.7,  93.3] },
      { label: 'Jakość przeprowadzonych zajęć',            pct: [0, 0,   0,    0,    100 ] },
      { label: 'Skład merytoryczny dokumentów',            pct: [0, 0,   6.7,  0,    93.3] },
      { label: 'Różnorodność metod dydaktycznych',         pct: [0, 0,   6.7,  0,    93.3] },
      { label: 'Uniwersalność przekazywanych treści',      pct: [0, 0,   6.7,  6.7,  86.7] },
      { label: 'Kompleksowość przeprowadzonych zajęć',     pct: [0, 6.7, 0,    6.7,  86.7] },
      { label: 'Kompatybilność z celami projektu',         pct: [0, 0,   0,    6.7,  93.3] },
    ],
    yesNo: { tak: 100, question: 'Czy zajęcia pozytywnie wpłynęły na przygotowanie językowe?' },
    openQ: [
      { q: 'Najbardziej podobało mi się', answers: ['wszystko po włosku','uczenie po włosku','sposób przeprowadzenia','poznawanie nowych uczniów i nauka języka','integracja','krajobraz, język i kultura'] },
      { q: 'Najbardziej nie podobało mi się', answers: ['nie ma takiej rzeczy','nic'] },
    ],
  },
  {
    id: 'organizacyjne',
    title: 'Spotkania organizacyjne (2h)',
    n: 15,
    questions: [
      { label: 'Wartość merytoryczna zajęć',               pct: [0, 0, 0,    0,    100 ] },
      { label: 'Metody prowadzenia zajęć',                 pct: [0, 0, 0,    6.7,  93.3] },
      { label: 'Przygotowanie merytoryczne prowadzącego',  pct: [0, 0, 0,    6.7,  93.3] },
      { label: 'Kontakt z uczestnikami zajęć',             pct: [0, 0, 6.7,  6.7,  86.7] },
      { label: 'Jakość wykorzystywanych materiałów',       pct: [0, 0, 0,    13.3, 86.7] },
      { label: 'Jakość przeprowadzonych zajęć',            pct: [0, 0, 0,    6.7,  93.3] },
      { label: 'Różnorodność metod dydaktycznych',         pct: [0, 0, 0,    6.7,  93.3] },
      { label: 'Uniwersalność przekazywanych treści',      pct: [0, 0, 0,    6.7,  93.3] },
      { label: 'Kompleksowość przeprowadzonych zajęć',     pct: [0, 0, 0,    13.3, 86.7] },
      { label: 'Kompatybilność z celami projektu',         pct: [0, 0, 6.7,  0,    93.3] },
    ],
    yesNo: { tak: 100, question: 'Czy zajęcia pozytywnie wpłynęły na wiedzę o logistyce wyjazdu?' },
    openQ: [
      { q: 'Najbardziej podobało mi się', answers: ['jasny przekaz informacji','to jak prowadzone są zajęcia','wszystko'] },
      { q: 'Najbardziej nie podobało mi się', answers: ['nic'] },
    ],
  },
  {
    id: 'kulturowe',
    title: 'Spotkania kulturowe (2h)',
    n: 15,
    questions: [
      { label: 'Wartość merytoryczna zajęć',               pct: [0, 0,   0,    0,    100 ] },
      { label: 'Metody prowadzenia zajęć',                 pct: [0, 0,   6.7,  6.7,  86.7] },
      { label: 'Przygotowanie merytoryczne prowadzącego',  pct: [0, 0,   0,    0,    100 ] },
      { label: 'Kontakt z uczestnikami zajęć',             pct: [0, 0,   0,    6.7,  93.3] },
      { label: 'Jakość wykorzystywanych materiałów',       pct: [0, 0,   0,    6.7,  93.3] },
      { label: 'Jakość przeprowadzonych zajęć',            pct: [0, 0,   0,    6.7,  93.3] },
      { label: 'Skład merytoryczny dokumentów',            pct: [0, 0,   0,    6.7,  93.3] },
      { label: 'Różnorodność metod dydaktycznych',         pct: [0, 0,   6.7,  6.7,  86.7] },
      { label: 'Uniwersalność przekazywanych treści',      pct: [0, 0,   0,    0,    100 ] },
      { label: 'Kompleksowość przeprowadzonych zajęć',     pct: [0, 0,   0,    0,    100 ] },
      { label: 'Kompatybilność z celami projektu',         pct: [0, 0,   0,    13.3, 86.7] },
    ],
    yesNo: { tak: 100, question: 'Czy zajęcia pozytywnie wpłynęły na przygotowanie kulturowe?' },
    openQ: [
      { q: 'Najbardziej podobało mi się', answers: ['kultura włoska','filmiki','materiały pokazane na zdjęciach','poznawanie nowych kultur','wszystko mi się podobało','szkoła'] },
      { q: 'Najbardziej nie podobało mi się', answers: ['nic'] },
    ],
  },
];

const EWALUACJA = {
  n: 15,
  partA: {
    title: 'Część A – Komunikacja w języku angielskim',
    questions: [
      { label: 'Lepsza umiejętność rozumienia ang. ze słuchu',     pct: [0, 0, 0,    26.7, 73.3] },
      { label: 'Swobodne porozumiewanie się po angielsku',          pct: [0, 0, 6.7,  13.3, 80  ] },
      { label: 'Pewność siebie w mówieniu po angielsku',            pct: [0, 0, 6.7,  6.7,  86.7] },
      { label: 'Wzbogacenie słownictwa angielskiego',               pct: [0, 0, 13.3, 20,   66.7] },
      { label: 'Motywacja do nauki angielskiego',                   pct: [0, 0, 0,    20,   80  ] },
      { label: 'Szansa na lepszy wynik matury z ang.',              pct: [0, 0, 0,    6.7,  93.3] },
      { label: 'Chęć do egzaminu certyfikacyjnego (FCE/CAE)',       pct: [0, 0, 20,   6.7,  73.3] },
    ],
  },
  partB: {
    title: 'Część B – Świadomość międzykulturowa',
    questions: [
      { label: 'Lepsza znajomość kultury Włoch',                    pct: [0, 0, 0,   0,    100 ] },
      { label: 'Większa otwartość na kontakty z innymi',            pct: [0, 0, 0,   13.3, 86.7] },
      { label: 'Efektywna współpraca w międzynar. zespole',         pct: [0, 0, 0,   26.7, 73.3] },
      { label: 'Radzenie sobie w nowych sytuacjach',                pct: [0, 0, 6.7, 0,    93.3] },
      { label: 'Lepsze rozumienie UE i jej możliwości',             pct: [0, 0, 6.7, 33.3, 60  ] },
      { label: 'Wzmocnienie tolerancji kulturowej',                 pct: [0, 0, 6.7, 6.7,  86.7] },
      { label: 'Chęć angażowania się w projekty międzynar.',        pct: [0, 0, 0,   26.7, 73.3] },
    ],
  },
  partC: {
    title: 'Część C – Organizacja i przebieg mobilności',
    questions: [
      { label: 'Dobre przygotowanie przez szkołę',      pct: [0, 0, 0,   13.3, 86.7] },
      { label: 'Ciekawe i angażujące zajęcia',          pct: [0, 0, 6.7, 6.7,  86.7] },
      { label: 'Poczucie bezpieczeństwa z opiekunami',  pct: [0, 0, 0,   0,    100 ] },
      { label: 'Zakwaterowanie i wyżywienie',           pct: [0, 0, 6.7, 26.7, 66.7] },
      { label: 'Dobrze zorganizowany program',          pct: [0, 0, 0,   6.7,  93.3] },
      { label: 'Poleciłbym/-abym wyjazd innym',         pct: [0, 0, 0,   6.7,  93.3] },
    ],
  },
  partE: {
    title: 'Część E – Ogólna ocena mobilności',
    questions: [
      { label: 'Ogólna jakość mobilności',   pct: [0, 0, 0,   13.3, 86.7] },
      { label: 'Własny rozwój językowy',     pct: [0, 0, 0,   13.3, 86.7] },
      { label: 'Własny rozwój osobisty',     pct: [0, 0, 6.7, 20,   73.3] },
      { label: 'Przygotowanie przez szkołę', pct: [0, 0, 0,   13.3, 86.7] },
    ],
  },
  partF: {
    title: 'Część F – Plany po powrocie',
    labels: [
      'Egzamin certyfikacyjny (FCE/CAE)',
      'Rozszerzona matura z angielskiego',
      'Szkolne koło językowe/debatanckie',
      'Kolejny projekt Erasmus+ / międzynar.',
      'Kontakty z uczniami za granicą',
      'Nauka języka włoskiego',
      'Wolontariat lub inicjatywy międzynar.',
    ],
    values: [40, 46.7, 16.7, 66.7, 26.7, 20, 20],
  },
  openQ: [
    { q: 'Największa wartość wyjazdu', answers: ['nauka rozmowy','kontakt z ludźmi','wyjazd za granicę','poznawanie nowej kultury i nowych smaków','użycie angielskiego w życiu codziennym','nauka angielskiego i włoskiego','poznanie nowych ludzi'] },
    { q: 'Co zmieniłbyś w programie?', answers: ['nic – było dobrze','więcej wycieczek','więcej czasu wolnego','hotel'] },
    { q: 'Czego się obawiałeś, a okazało się inne?', answers: ['włoska mafia','że jedzenie mi nie posmakuje','że się nie dogadam','atmosfera we włoskiej szkole','problemy z porozumiewaniem się','myślałam że ludzie będą mniej otwarci'] },
  ],
};

// PLACEHOLDER FOR RENDER CALLS (Tasks 3–5)
```

- [ ] **Step 2: Reload browser, open console**

`open index.html`. Open DevTools → Console. Expected: no errors, `SURVEYS` and `EWALUACJA` are defined (type `SURVEYS.length` → `6`).

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add all survey data constants"
```

---

## Task 3: Overview Tab + Helper Functions

**Files:**
- Modify: `index.html` — replace `// PLACEHOLDER FOR RENDER CALLS (Tasks 3–5)` with the code below

**Interfaces:**
- Consumes: `SURVEYS`, `EWALUACJA`, `SCORE_COLORS`, `SCORE_LABELS`
- Produces: `avgScore(questions)`, `renderStackedBar(canvasId, questions)`, `renderDonut(canvasId, tak)`, helper functions used by Tasks 4–5; renders Overview tab

- [ ] **Step 1: Replace placeholder with helpers + overview renderer**

```javascript
// ── HELPERS ────────────────────────────────────────────────────────────────
function avgScore(questions) {
  const totals = questions.map(q =>
    q.pct.reduce((sum, p, i) => sum + p * (i + 1), 0) / 100
  );
  return (totals.reduce((a, b) => a + b, 0) / totals.length).toFixed(2);
}

function renderStackedBar(canvasId, questions) {
  const ctx = document.getElementById(canvasId).getContext('2d');
  const labels = questions.map(q => q.label);
  const datasets = SCORE_LABELS.map((lbl, i) => ({
    label: lbl,
    data: questions.map(q => q.pct[i]),
    backgroundColor: SCORE_COLORS[i],
    borderWidth: 0,
    borderRadius: i === 0 ? { topLeft: 4, bottomLeft: 4 } : i === 4 ? { topRight: 4, bottomRight: 4 } : 0,
  }));
  new Chart(ctx, {
    type: 'bar',
    data: { labels, datasets },
    options: {
      indexAxis: 'y',
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { display: false },
        tooltip: {
          callbacks: {
            label: ctx => `${ctx.dataset.label}: ${ctx.parsed.x > 0 ? ctx.parsed.x.toFixed(1) + '%' : '0%'}`,
          },
        },
      },
      scales: {
        x: { stacked: true, max: 100, ticks: { callback: v => v + '%' }, grid: { color: '#f0f0f0' } },
        y: { stacked: true, ticks: { font: { size: 11 } } },
      },
    },
  });
}

function renderDonut(canvasId, tak) {
  const ctx = document.getElementById(canvasId).getContext('2d');
  new Chart(ctx, {
    type: 'doughnut',
    data: {
      labels: ['Tak', 'Nie'],
      datasets: [{ data: [tak, 100 - tak], backgroundColor: ['#2e7d32', '#e5e7eb'], borderWidth: 0 }],
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      cutout: '72%',
      plugins: {
        legend: { display: false },
        tooltip: { callbacks: { label: ctx => `${ctx.label}: ${ctx.parsed}%` } },
      },
    },
  });
}

function scoreLegendHTML() {
  return `<div class="score-legend">${SCORE_LABELS.map((l, i) =>
    `<span><i style="background:${SCORE_COLORS[i]}"></i>${l}</span>`
  ).join('')}</div>`;
}

function quotesHTML(openQ) {
  return openQ.map(o => `
    <div class="chart-card">
      <h3>${o.q}</h3>
      <div class="quotes">${o.answers.map(a => `<div class="quote">${a}</div>`).join('')}</div>
    </div>`).join('');
}

// ── OVERVIEW TAB ──────────────────────────────────────────────────────────
(function renderOverview() {
  const allSurveys = [
    ...SURVEYS,
    { id: 'ewaluacja', title: 'Ankieta ewaluacyjna – Włochy', n: 15,
      questions: [...EWALUACJA.partA.questions, ...EWALUACJA.partB.questions,
                  ...EWALUACJA.partC.questions, ...EWALUACJA.partE.questions] }
  ];

  const cards = allSurveys.map(s => {
    const avg = avgScore(s.questions);
    return `<div class="kpi-card">
      <div class="label">${s.title}</div>
      <div class="value">${avg}</div>
      <div class="unit">/ 5.00 &nbsp;·&nbsp; n = ${s.n}</div>
    </div>`;
  }).join('');

  const overallData = allSurveys.map(s => parseFloat(avgScore(s.questions)));
  const overallLabels = allSurveys.map(s => s.title);

  document.getElementById('overview').innerHTML = `
    <h2 style="font-size:1.2rem;margin-bottom:20px;color:var(--blue)">Wyniki wszystkich ankiet</h2>
    <div class="kpi-row">${cards}</div>
    <div class="chart-card">
      <h3>Średnia ocena (skala 1–5) – porównanie ankiet</h3>
      <div style="height:320px"><canvas id="overviewChart"></canvas></div>
    </div>
    <p style="font-size:0.8rem;color:var(--muted);margin-top:16px">
      Projekt współfinansowany przez Unię Europejską ze środków Europejskiego Funduszu Społecznego Plus
      w Programie Fundusze Europejskie dla Rozwoju Społecznego 2021–2027 na zasadach Programu Erasmus+.
    </p>`;

  new Chart(document.getElementById('overviewChart').getContext('2d'), {
    type: 'bar',
    data: {
      labels: overallLabels,
      datasets: [{
        label: 'Średnia ocena',
        data: overallData,
        backgroundColor: '#003DA5',
        borderRadius: 6,
      }],
    },
    options: {
      indexAxis: 'y',
      responsive: true,
      maintainAspectRatio: false,
      plugins: { legend: { display: false }, tooltip: { callbacks: { label: c => `Średnia: ${c.parsed.x.toFixed(2)} / 5.00` } } },
      scales: {
        x: { min: 4, max: 5, ticks: { stepSize: 0.2 }, grid: { color: '#f0f0f0' } },
        y: { ticks: { font: { size: 11 } } },
      },
    },
  });
})();

// PLACEHOLDER FOR TABS 1–6 AND TAB 7 (Tasks 4–5)
```

- [ ] **Step 2: Verify overview renders**

Reload `index.html`. Expected: Podsumowanie tab shows 7 KPI cards with average scores between 4.7–5.0, and a horizontal bar chart comparing all surveys. No console errors.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: render overview tab with KPI cards and comparison chart"
```

---

## Task 4: Survey Tabs 1–6

**Files:**
- Modify: `index.html` — replace `// PLACEHOLDER FOR TABS 1–6 AND TAB 7 (Tasks 4–5)`

**Interfaces:**
- Consumes: `SURVEYS`, `renderStackedBar`, `renderDonut`, `scoreLegendHTML`, `quotesHTML`
- Produces: rendered tabs for the 6 pre-mobility surveys; `// PLACEHOLDER FOR TAB 7 (Task 5)` at end

- [ ] **Step 1: Replace placeholder with survey tab renderer**

```javascript
// ── SURVEYS TABS 1–6 ──────────────────────────────────────────────────────
SURVEYS.forEach(survey => {
  const avg = avgScore(survey.questions);
  const pct5 = survey.questions.reduce((sum, q) => sum + q.pct[4], 0) / survey.questions.length;
  const chartId = `chart_${survey.id}`;
  const barHeight = Math.max(220, survey.questions.length * 38);

  let yesNoHTML = '';
  if (survey.yesNo) {
    const donutId = `donut_${survey.id}`;
    yesNoHTML = `
      <div class="chart-card">
        <h3>${survey.yesNo.question}</h3>
        <div class="donut-row">
          <div>
            <div class="donut-wrap"><canvas id="${donutId}"></canvas></div>
            <div class="donut-label">Tak</div>
          </div>
          <div class="yesno-badge">✔ ${survey.yesNo.tak}% odpowiedziało <strong>TAK</strong></div>
        </div>
      </div>`;
  }

  document.getElementById(survey.id).innerHTML = `
    <div class="kpi-row">
      <div class="kpi-card"><div class="label">Liczba respondentów</div><div class="value">${survey.n}</div><div class="unit">osób</div></div>
      <div class="kpi-card"><div class="label">Średnia ocena</div><div class="value">${avg}</div><div class="unit">/ 5.00</div></div>
      <div class="kpi-card"><div class="label">Ocena „5" (bardzo dobrze)</div><div class="value">${pct5.toFixed(1)}%</div><div class="unit">udzielonych odpowiedzi</div></div>
    </div>
    <div class="chart-card">
      <h3>${survey.title} – rozkład ocen (skala 1–5)</h3>
      ${scoreLegendHTML()}
      <div style="height:${barHeight}px"><canvas id="${chartId}"></canvas></div>
    </div>
    ${yesNoHTML}
    ${quotesHTML(survey.openQ)}`;

  renderStackedBar(chartId, survey.questions);
  if (survey.yesNo) renderDonut(`donut_${survey.id}`, survey.yesNo.tak);
});

// PLACEHOLDER FOR TAB 7 (Task 5)
```

- [ ] **Step 2: Verify all 6 survey tabs**

Reload `index.html`. Click each of Rekrutacja, Praca zespołu, Angielski 10h, Włoski 4h, Org. 2h, Kulturowe 2h. Each should show: 3 KPI cards, a horizontal stacked bar chart with correct question count (colour-coded 1–5), a yes/no donut (where applicable), and quote cards. Check DevTools console — no errors.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: render survey tabs 1-6 with stacked bars, donut charts, quotes"
```

---

## Task 5: Post-Italy Evaluation Tab (Tab 7)

**Files:**
- Modify: `index.html` — replace `// PLACEHOLDER FOR TAB 7 (Task 5)`

**Interfaces:**
- Consumes: `EWALUACJA`, `renderStackedBar`, `scoreLegendHTML`, `quotesHTML`

- [ ] **Step 1: Replace placeholder with ewaluacja renderer**

```javascript
// ── TAB 7 – ANKIETA EWALUACYJNA ───────────────────────────────────────────
(function renderEwaluacja() {
  const { partA, partB, partC, partE, partF, openQ, n } = EWALUACJA;

  function partSection(part, idSuffix) {
    const h = Math.max(180, part.questions.length * 38);
    const cid = `eval_${idSuffix}`;
    return `
      <div class="chart-card">
        <h3>${part.title}</h3>
        ${scoreLegendHTML()}
        <div style="height:${h}px"><canvas id="${cid}"></canvas></div>
      </div>`;
  }

  const partFColors = ['#003DA5','#1565c0','#1976d2','#1e88e5','#42a5f5','#90caf9','#bbdefb'];

  const allPartQs = [...partA.questions, ...partB.questions, ...partC.questions, ...partE.questions];
  const allAvg = avgScore(allPartQs);

  document.getElementById('ewaluacja').innerHTML = `
    <div class="kpi-row">
      <div class="kpi-card"><div class="label">Liczba respondentów</div><div class="value">${n}</div><div class="unit">uczniów po mobilności</div></div>
      <div class="kpi-card"><div class="label">Średnia ocena (części A–E)</div><div class="value">${allAvg}</div><div class="unit">/ 5.00</div></div>
    </div>
    ${partSection(partA, 'A')}
    ${partSection(partB, 'B')}
    ${partSection(partC, 'C')}
    ${partSection(partE, 'E')}
    <div class="chart-card">
      <h3>${partF.title}</h3>
      <div style="height:260px"><canvas id="eval_F"></canvas></div>
    </div>
    ${quotesHTML(openQ)}`;

  renderStackedBar('eval_A', partA.questions);
  renderStackedBar('eval_B', partB.questions);
  renderStackedBar('eval_C', partC.questions);
  renderStackedBar('eval_E', partE.questions);

  new Chart(document.getElementById('eval_F').getContext('2d'), {
    type: 'bar',
    data: {
      labels: partF.labels,
      datasets: [{
        label: '% uczniów',
        data: partF.values,
        backgroundColor: partFColors,
        borderRadius: 6,
      }],
    },
    options: {
      indexAxis: 'y',
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { display: false },
        tooltip: { callbacks: { label: c => `${c.parsed.x}% uczniów` } },
      },
      scales: {
        x: { max: 100, ticks: { callback: v => v + '%' }, grid: { color: '#f0f0f0' } },
        y: { ticks: { font: { size: 11 } } },
      },
    },
  });
})();
```

- [ ] **Step 2: Verify Tab 7**

Click "Po wyjeździe 🇮🇹" tab. Expected: 2 KPI cards, 4 stacked bar sections (A, B, C, E), a horizontal bar for Part F (plans), and 3 quote card groups. No console errors.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: render post-Italy evaluation tab with multi-section charts"
```

---

## Task 6: GitHub Pages Config + Final Polish

**Files:**
- Create: `.nojekyll`

- [ ] **Step 1: Create `.nojekyll`**

```bash
touch .nojekyll
```

- [ ] **Step 2: Test responsiveness on mobile viewport**

In Chrome DevTools, toggle device toolbar (Cmd+Shift+M), select "iPhone SE" (375px wide). Verify: tab bar scrolls horizontally, charts resize correctly, KPI cards wrap to 2 columns, no horizontal overflow on `<body>`.

- [ ] **Step 3: Test on Firefox**

Open `index.html` in Firefox. Verify all charts render correctly (Chart.js renders identically in all modern browsers, but confirm no layout regressions).

- [ ] **Step 4: Commit and push**

```bash
git add .nojekyll
git commit -m "chore: add .nojekyll for GitHub Pages"
git push origin main
```

- [ ] **Step 5: Enable GitHub Pages in repo settings**

Go to the repo on GitHub → Settings → Pages → Source: "Deploy from a branch" → Branch: `main`, folder: `/ (root)` → Save. After ~60 seconds visit `https://<username>.github.io/<repo>/` and verify the full page loads with all charts.

---

## Self-Review

**Spec coverage:**
- ✅ Single `index.html`, no build step
- ✅ Tab 0 Overview with 7 KPI cards + comparison chart
- ✅ Tabs 1–6 with stacked bars, yes/no donuts, quote cards
- ✅ Tab 7 post-Italy with Parts A, B, C, E, F
- ✅ Polish language throughout
- ✅ Erasmus+ blue + EU gold colour scheme
- ✅ Score gradient red→green
- ✅ Responsive (mobile tab scroll, flexible KPI cards)
- ✅ `.nojekyll` for GitHub Pages

**Placeholder scan:** None found.

**Type consistency:** `renderStackedBar(canvasId, questions)` and `renderDonut(canvasId, tak)` used consistently. `avgScore(questions)` called identically across Tasks 3–5.
