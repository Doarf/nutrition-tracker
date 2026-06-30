# Nutrition Tracker

A personal recomposition dashboard to track weight, calories, and macros toward a fat loss goal.

## Features

- **Dashboard** — daily summary: weight, calories consumed, calories burned, net deficit
- **Weight tracking** — weekly weigh-ins with chart and target trajectory
- **Nutrition** — weekly and daily tables with averages for kcal, protein, carbs, and fat
- **Food log** — log meals by date with full macro breakdown
- **Calories burned** — manual entry from a fitness watch for net deficit calculation
- **Import / Export** — full JSON backup and restore

## Stack

Single HTML file + JSON data file. No build step, no dependencies except [Chart.js](https://www.chartjs.org/) via CDN.

## Usage

1. Open `nutrition-dashboard_arthur.html` in a browser
2. On first launch, import your data file via the **Data → Load .json** button
3. Log meals and daily burn in the **Log** tab
4. Add weekly weigh-ins in the **Weight** tab
5. Export a fresh JSON backup anytime from **Data → Download .json** or the sidebar button

## Data format

```json
{
  "profile": {
    "start": 100.9,
    "goal": 80,
    "goalDate": "2026-10-19",
    "lean": 71,
    "targets": { "kcal": 2100, "protein": 150, "carbs": 210, "fat": 80 }
  },
  "weights": {
    "2026-05-18": 100.9
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

## Goal

| | |
|---|---|
| Start | 100.9 kg |
| Goal | 80 kg |
| Deadline | October 19, 2026 |
| Target rate | −0.7 kg / week |
| Lean floor | 71 kg |
