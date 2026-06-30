# nutrition-tracker

<div align="center">

**Personal recomposition dashboard — weight, calories, macros & deficit tracking**  
*Single-file · localStorage · GitHub Gist sync · Chart.js · No build step*

![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)
![Platform](https://img.shields.io/badge/platform-browser-blue?style=flat-square)
![Lang](https://img.shields.io/badge/language-HTML%20%7C%20CSS%20%7C%20JavaScript-informational?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

<br/>
<img src="assets/pixel-dumbbell.svg" alt="pixel dumbbell" width="480"/>

</div>

---

## About the project

**nutrition-tracker** is a zero-dependency personal dashboard for tracking a recomposition goal. It runs entirely in the browser — no server, no account, no cloud. Data lives in `localStorage`, can be exported as a plain JSON file, and optionally synced across devices via a private GitHub Gist.

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
| Multi-device sync | GitHub Gist push/pull via classic PAT |
| Zero setup | Single HTML file, open in browser and go |

---

## Architecture

```
Browser (PC 1)                          Browser (PC 2)
   │                                         │
   ├── nutrition-dashboard_arthur.html        ├── nutrition-dashboard_arthur.html
   │        │                                │        │
   │        ├── localStorage                 │        ├── localStorage
   │        │        │                       │        │
   │        └── Chart.js (CDN)              │        └── Chart.js (CDN)
   │                                         │
   └─────────────┐               ┌───────────┘
                 │    Push/Pull  │
           GitHub Gist (private)
           recomp_data.json
```

---

## Features

| Tab | What it does |
|-----|-------------|
| **Today** | Summary cards (weight, consumed, burned, net deficit) + macro bars + weight history chart |
| **Weight** | Add weekly weigh-ins, view chart with actual vs target trajectory and lean floor |
| **Nutrition** | Weekly averages table (most recent first), consumed vs burned bar chart, full daily detail |
| **Log** | Add meals by date (name, kcal, protein, carbs, fat) + daily burn from watch |
| **Data** | Export / import JSON · GitHub Gist push/pull · reset |

---

## Software stack

| Layer | Technology | Role |
|-------|-----------|------|
| UI | HTML5 + CSS3 | Layout, dark theme, responsive sidebar |
| Logic | Vanilla JavaScript | State management, weekly aggregation, chart rendering |
| Charts | Chart.js 4.4 (CDN) | Weight curve, weekly calorie bar chart |
| Storage | localStorage | Persistent in-browser data store |
| Sync | GitHub Gist API | Cross-device data sync via private Gist |
| Data format | JSON | Portable export / import / sync |

---

## Data format

Data is stored in `localStorage` under the key `recomp_v3` and synced to a private Gist as `recomp_data.json`.

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

---

## Multi-device sync (GitHub Gist)

Sync your data across devices without any server or cloud account — just a private GitHub Gist.

### Setup (once per device)

1. Generate a [classic personal access token](https://github.com/settings/tokens/new?scopes=gist&description=recomp-dashboard) with only the **`gist`** scope
2. Open the dashboard → **Data** tab
3. Paste the token in the **GitHub Personal Access Token** field

### First push (PC 1)

```
Data → Push to Gist
```

A private Gist is created automatically. Copy the **Gist ID** displayed in the field.

### First pull (PC 2)

```
Data → paste token → paste Gist ID → Pull from Gist
```

Data merges into localStorage. Token and Gist ID are saved locally — enter them only once per device.

### Daily workflow

```
End of session  →  Push to Gist
Start of session  →  Pull from Gist
```

---

> **Privacy note** — the JSON data file is gitignored. Your personal body metrics and food logs never leave your machine unless you explicitly export or push to your private Gist.

---

## Repository structure

```
nutrition-tracker/
├── nutrition-dashboard_arthur.html   # Full dashboard (UI + logic)
├── assets/
│   └── pixel-dumbbell.svg            # README image
├── .gitignore                        # Excludes recomp_*.json
└── README.md
```

---

<div align="center">
  <sub>Personal project · nutrition-tracker · Recomp tracking dashboard</sub>
</div>
