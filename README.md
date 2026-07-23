# 🚵 Singletrack Density Dashboard

An interactive trail advocacy tool for comparing singletrack trail access per capita across North American mountain bike destinations. Built for community planners, trail advocates, and municipal stakeholders who need data-driven comparisons to make the case for trail investment.

> Originally developed for the Castle Rock, CO trail advocacy campaign at Philip S. Miller Park and Ridgeline Open Space. Published at [Pinkbike.com](https://www.pinkbike.com) and embedded at [postmillenniumrenaissance.com](https://www.postmillenniumrenaissance.com/singletrack-density/).

---

## Live Demo

🔗 **[View the Dashboard →](https://postmillennium-mtb.github.io/Singletrack-Density/)**

---

## What It Does

The dashboard answers one question: *How does your city's trail network compare to the best trail towns in North America — and what would it cost to close the gap?*

It ships with data for 26 cities ranging from micro trail towns (East Burke, VT; Crested Butte, CO) to large urban areas (Austin, TX; Boise, ID), and lets you add your own locations for custom comparisons.

---

## Features

### Charts

- **Miles per 10k Residents** — horizontal bar chart, sorted best-to-worst. Higher is better.
- **Population per Mile of Trail** — horizontal bar chart, sorted best-to-worst. Lower is better.
- **Scatter Plot** — population (log scale) vs. trail miles, with a log-linear regression trend line. Shows where a city sits relative to its peer group, with a detail readout on selection.

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
- **Estimated investment range** based on customizable cost-per-mile inputs
- Toggle the target metric between Mi/10k and Pop/Mile

### Highlight City

Any city in the dataset can be set as the "highlighted" city (default: Castle Rock, CO). The highlighted city:

- Appears in **orange** across all charts, scatter plot, and data table
- Serves as the **baseline** in the Trail Gap Calculator

### Add Custom Locations

Add any city not in the default dataset directly from the UI:

- Required: City Name, Population, Trail Miles
- Optional: City Area (sq mi), 5-Year Growth (mi)
- All metrics (mi/10k, pop/mile, trail density) are auto-calculated and appended live to the charts and table

### Units

Toggle between **Imperial** (miles), **Metric** (km), and **Both** — affects charts, tooltips, and the data table simultaneously.

### Theme

**Dark mode** (forest green, default) and **Light mode** (neutral gray). Both use a color-blind-safe palette — blue + orange + indigo, no red/green distinction.

### Master Data Table

Sortable by any column:

| Column        | Description                                       |
| ------------- | -------------------------------------------------- |
| City          | Location name                                       |
| Population    | Estimated population                                 |
| Trail mi/km   | Maintained singletrack network estimate              |
| mi / 10k pop  | Miles per 10,000 residents (or km in metric mode)    |
| pop / mi      | Residents per trail mile (or per km)                 |
| Trail / sq mi | Trail density within municipal boundaries            |
| 5yr Growth    | Miles added in the past 5 years (user-entered)       |

Performance cells are color-coded: strong / moderate / below-average, matched to the theme's color-blind-safe palette.

---

## Default Dataset (26 Cities)

| City                    | Population | Trail Miles |
| ----------------------- | ---------- | ----------- |
| East Burke, VT          | 150        | 100         |
| Copper Harbor, MI       | 100        | 40          |
| Downieville, CA         | 200        | 80          |
| Crested Butte, CO       | 1,650      | 450         |
| Carrabassett Valley, ME | 750        | 80          |
| Oakridge, OR            | 3,200      | 350         |
| Crosby, MN              | 2,300      | 70          |
| Moab, UT                | 5,200      | 150         |
| Brevard, NC             | 7,700      | 300         |
| Park City, UT           | 8,400      | 450         |
| Sedona, AZ              | 9,600      | 200         |
| Fruita, CO              | 14,100     | 130         |
| Anniston, AL            | 21,000     | 35          |
| Marquette, MI           | 22,100     | 75          |
| Squamish, BC            | 24,000     | 200         |
| Helena, MT              | 34,000     | 85          |
| Harrisonburg, VA        | 51,000     | 110         |
| Bentonville, AR         | 64,800     | 300         |
| Ocala, FL               | 71,700     | 80          |
| **Castle Rock, CO**     | **84,000** | **35**      |
| Santa Fe, NM            | 89,000     | 115         |
| Duluth, MN              | 88,600     | 100         |
| Bellingham, WA          | 96,000     | 120         |
| Chattanooga, TN         | 184,000    | 125         |
| Boise, ID               | 236,000    | 190         |
| Austin, TX              | 980,000    | 150         |

---

## Getting Started

This is a single, self-contained HTML file — no build step, no dependencies, no npm install.

### Option 1 — View it live

Open the [live GitHub Pages demo](https://postmillennium-mtb.github.io/Singletrack-Density/). Nothing to install.

### Option 2 — Run it locally

1. Clone or download this repository
2. Open `index.html` directly in any browser

That's it — all HTML, CSS, and JavaScript live in the one file.

### Option 3 — Deploy your own copy

1. Fork this repository
2. Enable GitHub Pages from the repository Settings → Pages → deploy from the `main` branch
3. Your copy will be live at `https://yourusername.github.io/Singletrack-Density/`

### Option 4 — Embed elsewhere

Since it's a single static HTML file, it can be dropped into an `<iframe>` on any site — this is how it's embedded at [postmillenniumrenaissance.com](https://www.postmillenniumrenaissance.com/singletrack-density/).

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

To add a city permanently to the default dataset, edit the `SEED` array near the top of the `<script>` block in `index.html`:

```js
{ city:"Whistler, BC", population:12000, trails:155, areaSqMi:40.3, milesAdded5yr:null },
```

All derived metric fields (`milesper10k`, `popPerMile`, `trailsPerSqMi`) are computed automatically by the `enrich()` function — you only need to supply the raw values (`city`, `population`, `trails`, `areaSqMi`, `milesAdded5yr`).

To update an existing city (e.g., Castle Rock trail miles after a new phase opens), find the relevant entry in `SEED` and update the `trails` value. All derived metrics recalculate automatically on page load.

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

**Always verify figures with local trail organizations and municipal planning departments before citing in formal documents, grant applications, or public presentations.**

---

## Tech Stack

| Layer        | Technology                                    |
| ------------ | ---------------------------------------------- |
| Structure    | Plain HTML                                      |
| Styling      | Inline `<style>` block, CSS custom properties for theming, no build dependencies |
| Logic        | Vanilla JavaScript (no framework)               |
| Regression   | Custom log-linear regression (vanilla JS)       |
| Deployment   | GitHub Pages, embedded via iframe on Pinkbike / postmillenniumrenaissance.com |

No build tool, package manager, or framework required. Just a browser.

---

## Roadmap / Potential Enhancements

- [ ] Public land acreage field (`publicAcres`) for a cleaner trail-density metric
- [ ] Export to CSV / PDF for council presentations
- [ ] Shareable URL state (encode filter/highlight settings in query params)
- [ ] Log scale toggle for bar charts to reduce outlier distortion
- [ ] Year-over-year growth chart (sparklines per city)

---

## Contributing

Pull requests welcome. If you have accurate trail mileage data for a city not in the dataset, or corrections to existing figures, please open an issue with a source link.

For trail towns outside North America (UK, Australia, New Zealand, South Africa), the metric calculations work identically — just use km values and toggle to Metric mode.

---

## About

Built by **Jon** ([@redfoxrun](https://github.com/redfoxrun)) — trail advocate and community planner based in Castle Rock, CO.

This tool is part of an ongoing campaign to secure funding for new mountain bike and hiking trails at **Philip S. Miller Park** and **Ridgeline Open Space** in Castle Rock. If you live in Castle Rock and want more trails, email your Town Council.

Related tools in the Post Millennium Renaissance (PMR) suite:

- Trail Investment ROI Calculator
- Pump Track / Skatepark Municipal Investment Calculator
- MTB Price Inflation Dashboard
- MTB Patent Atlas
- Canadian Lift-Served Bike Park Guide (EN/FR)
- US Lift-Served Bike Park Guide (87+ parks)

---

## License

MIT License — free to use, adapt, and redistribute with attribution.

```
Copyright (c) 2025–2026 Jon / Post Millennium Renaissance
```
