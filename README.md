# 🚵 Singletrack Density Dashboard

An interactive trail advocacy tool for comparing singletrack trail access per capita across North American mountain bike destinations. Built for community planners, trail advocates, and municipal stakeholders who need data-driven comparisons to make the case for trail investment.

> Originally developed for the Castle Rock, CO trail advocacy campaign at Philip S. Miller Park and Ridgeline Open Space. Published at [Pinkbike.com](https://www.pinkbike.com) and hosted via GitHub Pages.

---

## Live Demo

🔗 **[View the Dashboard →](https://redfoxrun.github.io/singletrack-density)** *(update with your GitHub Pages URL)*

---

## What It Does

The dashboard answers one question: *How does your city's trail network compare to the best trail towns in North America — and what would it cost to close the gap?*

It ships with data for 26 cities ranging from micro trail towns (East Burke, VT; Crested Butte, CO) to large urban areas (Austin, TX; Boise, ID), and lets you add your own locations for custom comparisons.

---

## Features

### Charts
- **Miles per 10k Residents** — horizontal bar chart, sorted best-to-top. Higher is better.
- **Population per Mile of Trail** — horizontal bar chart, sorted best-to-top. Lower is better.
- **Scatter Plot** — population (log scale) vs. trail miles, with a log-linear regression trend line. Shows where a city sits relative to its peer group.

### Population Tier Filter
Multi-select filter to scope comparisons to a meaningful peer group:
- **< 5k** — micro trail towns (Crested Butte, Moab, Park City)
- **5k – 50k** — small trail communities (Brevard, Fruita, Squamish)
- **50k – 150k** — mid-size cities (Castle Rock's peer group)
- **150k+** — large cities (Chattanooga, Boise, Austin)

Multiple tiers can be active simultaneously. Filtering the charts does not hide data from the master table.

### Trail Gap Calculator
Select any benchmark city and see exactly what it would take for your highlighted city to match that ratio:
- **Miles needed** to reach parity
- **Estimated investment range** based on customizable cost-per-mile inputs ($50k–$150k/mi default)
- **Population context note** — flags comparisons where a large population difference makes per-capita ratios misleading
- Supports both Mi/10k and Pop/Mile metrics

### Highlight City
Any city in the dataset can be set as the "highlighted" city (default: Castle Rock, CO). The highlighted city:
- Appears in **orange** across all charts, scatter plot, and data table
- Serves as the **baseline** in the Trail Gap Calculator
- Shows a live stats card when selected in the Highlight tab

### Add Custom Locations
Add any city not in the default dataset:
- Required: City Name, Population, Trail Miles
- Optional: City Area (sq mi), 5-Year Growth (mi)
- All metrics (mi/10k, pop/mile, trail density) are auto-calculated and appended live

### Units
Toggle between **Imperial** (miles), **Metric** (km), and **Both** — affects charts, tooltips, and the data table simultaneously.

### Theme
**Dark mode** (forest green, default) and **Light mode** (neutral gray). Both use a color-blind safe palette — blue + orange + indigo, no red/green distinction.

### Master Data Table
Sortable by any column:

| Column | Description |
|---|---|
| City | Location name |
| Population | Estimated population |
| Trail mi/km | Maintained singletrack network estimate |
| mi / 10k pop | Miles per 10,000 residents (or km in metric mode) |
| pop / mi | Residents per trail mile (or per km) |
| Trail / sq mi | Trail density within municipal boundaries |
| 5yr Growth | Miles added in the past 5 years (user-entered) |

Performance cells are color-coded: **blue** = strong, **light blue** = moderate, **muted** = below average.

---

## Default Dataset (26 Cities)

| City | Population | Trail Miles |
|---|---|---|
| East Burke, VT | 150 | 100 |
| Copper Harbor, MI | 100 | 40 |
| Downieville, CA | 200 | 80 |
| Crested Butte, CO | 1,650 | 450 |
| Carrabassett Valley, ME | 750 | 80 |
| Oakridge, OR | 3,200 | 350 |
| Crosby, MN | 2,300 | 70 |
| Moab, UT | 5,200 | 150 |
| Brevard, NC | 7,700 | 300 |
| Park City, UT | 8,400 | 450 |
| Sedona, AZ | 9,600 | 200 |
| Fruita, CO | 14,100 | 130 |
| Anniston, AL | 21,000 | 35 |
| Marquette, MI | 22,100 | 75 |
| Squamish, BC | 24,000 | 200 |
| Helena, MT | 34,000 | 85 |
| Harrisonburg, VA | 51,000 | 110 |
| Bentonville, AR | 64,800 | 300 |
| Ocala, FL | 71,700 | 80 |
| **Castle Rock, CO** | **84,000** | **35** |
| Santa Fe, NM | 89,000 | 115 |
| Duluth, MN | 88,600 | 100 |
| Bellingham, WA | 96,000 | 120 |
| Chattanooga, TN | 184,000 | 125 |
| Boise, ID | 236,000 | 190 |
| Austin, TX | 980,000 | 150 |

---

## Getting Started

### Option 1 — Use in a Claude Artifact (no setup)
This component is designed to run as a React artifact in [Claude.ai](https://claude.ai). Paste the contents of `singletrack-density.jsx` into a Claude conversation and ask it to render the artifact.

### Option 2 — Embed in a React Project

**Requirements:** Node.js 18+, a React project with Recharts installed.

```bash
# Install dependency
npm install recharts

# Copy the component into your project
cp singletrack-density.jsx src/components/
```

Then import and use it:

```jsx
import Dashboard from './components/singletrack-density';

function App() {
  return <Dashboard />;
}
```

### Option 3 — GitHub Pages (standalone)

1. Fork this repository
2. Set up a minimal Vite or Create React App wrapper
3. Enable GitHub Pages from the repository Settings → Pages → deploy from `gh-pages` branch
4. The dashboard will be live at `https://yourusername.github.io/singletrack-density`

---

## Key Metrics Explained

**Miles per 10,000 Residents**
```
mi_per_10k = trail_miles / (population / 10,000)
```
Normalizes trail access to population size. Higher = more trail per capita. Small towns with large surrounding trail networks will score extremely high on this metric — use the Population Tier Filter to compare like-for-like.

**Population per Mile of Trail**
```
pop_per_mile = population / trail_miles
```
Inverse measure of access — how many people share each mile of trail. Lower = less crowded. Large urban areas naturally score worse regardless of trail investment.

**Trail Density (Trail / sq mi)**
```
trail_density = trail_miles / city_area_sq_mi
```
Uses municipal boundary area. Note: small incorporated towns often have trails extending well beyond city limits into adjacent national forest or BLM land, which inflates this figure.

**Trail Gap (Gap Calculator)**
```
# Miles per 10k parity:
target_miles = benchmark_mi_per_10k × (home_population / 10,000)
gap = target_miles − current_trail_miles

# Population per mile parity:
target_miles = home_population / benchmark_pop_per_mile
gap = target_miles − current_trail_miles
```

---

## Adding or Updating Data

To add a city permanently to the default dataset, edit the `SEED` array near the top of `singletrack-density.jsx`:

```js
{ city: "Whistler, BC", population: 12000, trails: 155, areaSqMi: 40.3, milesAdded5yr: null },
```

All five metric fields (`milesper10k`, `popPerMile`, `trailsPerSqMi`, `growthPct`) are computed automatically by the `enrich()` function — you only need to supply the four raw values.

To update an existing city (e.g., Castle Rock trail miles after a new phase opens), find the relevant entry in `SEED` and update the `trails` value. All derived metrics recalculate automatically.

---

## Data Sources and Methodology

Trail mileage figures are estimates compiled from:
- Local trail organization websites and Trailforks listings
- Municipal parks and recreation department publications
- IMBA and regional trail coalition reports
- Community-contributed data and Pinkbike forum sources

Population figures are based on recent municipal estimates and U.S./Canadian census data.

**These are approximate estimates, not official figures.** Methodology notes:

- Trail mileage typically represents the maintained singletrack network. It may include trails on adjacent lands managed by different jurisdictions (national forest, BLM, county open space, state land).
- City area data (`areaSqMi`) uses approximate municipal boundary measurements. Small incorporated towns whose trail systems extend significantly onto surrounding public lands will show inflated trail-density scores.
- Population labels (village / town / city) in the Gap Calculator context note are informal readability designations only — not official classifications.

**Always verify figures with local trail organizations and municipal planning departments before citing in formal documents, grant applications, or public presentations.**

---

## Tech Stack

| Layer | Technology |
|---|---|
| UI framework | React 18 (functional components, hooks) |
| Charts | [Recharts](https://recharts.org) — BarChart, ScatterChart |
| Styling | Inline styles (no build dependencies) |
| Regression | Custom log-linear regression (vanilla JS) |
| Deployment | GitHub Pages / Claude Artifacts |

No build tool is strictly required for the artifact version. For standalone deployment, Vite is recommended.

---

## Roadmap / Potential Enhancements

- [ ] Public land acreage field (`publicAcres`) for a cleaner trail-density metric
- [ ] Export to CSV / PDF for council presentations
- [ ] Shareable URL state (encode filter/highlight settings in query params)
- [ ] Log scale toggle for bar charts to reduce outlier distortion
- [ ] Year-over-year growth chart (sparklines per city)
- [ ] Embed mode with reduced chrome for Pinkbike / iframe deployment

---

## Contributing

Pull requests welcome. If you have accurate trail mileage data for a city not in the dataset, or corrections to existing figures, please open an issue with a source link.

For trail towns outside North America (UK, Australia, New Zealand, South Africa), the metric calculations work identically — just use km values and toggle to Metric mode.

---

## About

Built by **Jon** ([@redfoxrun](https://github.com/redfoxrun)) — trail advocate and community planner based in Castle Rock, CO.

This tool is part of an ongoing campaign to secure funding for new mountain bike and hiking trails at **Philip S. Miller Park** and **Ridgeline Open Space** in Castle Rock. If you live in Castle Rock and want more trails, email your Town Council.

Related tools in the RedFoxRun suite:
- Trail Investment ROI Calculator (v2.1)
- Pump Track / Skatepark Municipal Investment Calculator
- MTB Price Inflation Dashboard
- Canadian Lift-Served Bike Park Guide (EN/FR)
- US Lift-Served Bike Park Guide (60+ parks)

---

## License

MIT License — free to use, adapt, and redistribute with attribution.

```
Copyright (c) 2025 Jon / RedFoxRun
```
