# nutrition-tracker

<div align="center">

**Personal recomposition dashboard — weight, calories, macros & deficit tracking**  
*Single-file · localStorage · JSON · Chart.js · No build step*

![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)
![Platform](https://img.shields.io/badge/platform-browser-blue?style=flat-square)
![Lang](https://img.shields.io/badge/language-HTML%20%7C%20CSS%20%7C%20JavaScript-informational?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

<br/>
<img src="assets/pixel-dumbbell.svg" alt="pixel dumbbell" width="480"/>

</div>

---

## About the project

**nutrition-tracker** is a zero-dependency personal dashboard for tracking a recomposition goal. It runs entirely in the browser — no server, no account, no cloud. Data lives in `localStorage` and can be exported / imported as a plain JSON file at any time.

### The problem

Most nutrition apps are bloated, require an account, or lock your data behind a subscription. Tracking a recomp (simultaneous fat loss + muscle retention) means monitoring not just calories but the **net deficit** between intake and actual expenditure — a metric most apps don't surface clearly.

### The solution

| Need | Solution |
|------|----------|
| Daily calorie & macro logging | Food log with per-entry macro breakdown |
| Net deficit tracking | Manual burn entry (from watch) → consumed vs burned |
| Weekly overview | Aggregated table + bar chart per ISO week |
| Weight progress | Weekly weigh-ins with target trajectory curve |
| Data ownership | Export / import via plain JSON — no lock-in |
| Zero setup | Single HTML file, open in browser and go |

---

## Architecture

```
Browser
   │
   ├── nutrition-dashboard_arthur.html   (UI + logic, self-contained)
   │        │
   │        ├── localStorage             (live data store)
   │        │        │
   │        │        └── recomp_*.json  (export / import, gitignored)
   │        │
   │        └── Chart.js (CDN)          (weight & weekly calorie charts)
   │
   └── No server · No build · No account
```

---

## Features

| Tab | What it does |
|-----|-------------|
| **Today** | Summary cards (weight, consumed, burned, net deficit) + macro bars + weight history chart |
| **Weight** | Add weekly weigh-ins, view chart with actual vs target trajectory and lean floor |
| **Nutrition** | Weekly averages table, consumed vs burned bar chart, full daily detail table |
| **Log** | Add meals by date (name, kcal, protein, carbs, fat) + daily burn from watch |
| **Data** | Export full history as JSON, import & merge, reset |

---

## Software stack

| Layer | Technology | Role |
|-------|-----------|------|
| UI | HTML5 + CSS3 | Layout, dark theme, responsive sidebar |
| Logic | Vanilla JavaScript | State management, weekly aggregation, chart rendering |
| Charts | Chart.js 4.4 (CDN) | Weight curve, weekly calorie bar chart |
| Storage | localStorage | Persistent in-browser data store |
| Data format | JSON | Portable export / import |

---

## Data format

Data is stored in `localStorage` under the key `recomp_v3` and can be exported as a JSON file at any time.

```json
{
  "profile": {
    "start": 0,
    "goal": 0,
    "goalDate": "",
    "lean": 0,
    "targets": { "kcal": 2000, "protein": 150, "carbs": 200, "fat": 65 }
  },
  "weights": {
    "2026-06-30": 95.9
  },
  "nutrition": {
    "2026-06-30": {
      "entries": [
        { "name": "Chicken rice", "kcal": 650, "p": 50, "c": 70, "f": 12 }
      ],
      "burned": 2900
    }
  }
}
```

- `profile` — personal goal and macro targets (kept private, not committed)
- `weights` — ISO date → kg, one entry per weigh-in
- `nutrition[date].entries` — list of meals logged that day
- `nutrition[date].burned` — total daily expenditure from a fitness watch (optional)

---

## Getting started

### Prerequisites

A modern browser. That's it.

### Usage

```bash
# 1. Clone the repo
git clone https://github.com/Doarf/nutrition-tracker.git
cd nutrition-tracker

# 2. Open the dashboard
#    Double-click nutrition-dashboard_arthur.html
#    or open it directly in your browser

# 3. First launch — import your data (optional)
#    Data → Load .json → select your recomp_*.json file

# 4. Log your meals
#    Log tab → fill in name, kcal, macros → Add
#    Enter daily burn from your watch

# 5. Add weigh-ins
#    Weight tab → pick date, enter weight → Save

# 6. Export a backup anytime
#    Data → Download .json   (or sidebar Export button)
```

> **Privacy note** — the JSON data file is gitignored. Your personal body metrics and food logs never leave your machine unless you explicitly share the exported file.

---

## Repository structure

```
nutrition-tracker/
├── nutrition-dashboard_arthur.html   # Full dashboard (UI + logic)
├── .gitignore                        # Excludes recomp_*.json
└── README.md
```

---

<div align="center">
  <sub>Personal project · nutrition-tracker · Recomp tracking dashboard</sub>
</div>
