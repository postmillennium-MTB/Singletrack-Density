# 🚵 Singletrack Density Dashboard

An interactive trail advocacy tool for comparing singletrack trail access per capita across North American mountain bike destinations. Built for community planners, trail advocates, and municipal stakeholders who need data-driven comparisons to make the case for trail investment.

> Originally developed for the Castle Rock, CO trail advocacy campaign at Philip S. Miller Park and Ridgeline Open Space. Published at [Pinkbike.com](https://www.pinkbike.com) and embedded at [postmillenniumrenaissance.com](https://www.postmillenniumrenaissance.com/singletrack-density/).

---

## Live Demo

🔗 **[View the Dashboard →](https://postmillennium-mtb.github.io/Singletrack-Density/)**

---

## What It Does

The dashboard answers one question: *How does your city's trail network compare to the best trail towns in North America — and what would it cost to close the gap?*

It ships with data for **38 cities** ranging from micro trail towns (East Burke, VT; Crested Butte, CO) to large urban areas (Austin, TX; Anchorage, AK), spanning the lower 48 plus **Alaska and Hawaii**, and lets you add your own locations for custom comparisons.

---

## Features

### Charts

- **Miles per 10k Residents** — horizontal bar chart, sorted best-to-worst. Higher is better.
- **Population per Mile of Trail** — horizontal bar chart, sorted best-to-worst. Lower is better.
- **Scatter Plot** — population (log scale) vs. trail miles, with a log-linear regression trend line. Shows where a city sits relative to its peer group, with a detail readout on selection.

### Location Map

A hand-built inline-SVG map of the United States with a dot for every city, projected from real latitude/longitude. **Alaska and Hawaii appear in insets** in the lower-left. The highlighted city is drawn in orange, and hovering or tapping any dot shows that city's population, trail miles, and per-capita access. No external mapping library — the map is pure SVG and works fully offline.

> A city appears on the map only if it has `lat`/`lng` coordinates in its data record (see [Updating & Adding Data](#updating--adding-data)). Cities added through the in-app **Add Location** form are not plotted on the map, since the form doesn't collect coordinates.

### Population Tier Filter

Multi-select filter to scope comparisons to a meaningful peer group:

- **< 5k** — micro trail towns (Crested Butte, Moab, Makawao)
- **5k – 25k** — small trail communities (Brevard, Fruita, Durango, Golden)
- **25k – 50k** — small-mid cities (Helena, Prescott, Poway)
- **50k – 150k** — mid-size cities (Castle Rock's peer group — Draper, Bend, Flagstaff, Grand Junction)
- **150k+** — large cities (Chattanooga, Boise, Reno, Anchorage, Austin)

Multiple tiers can be active simultaneously. Filtering the charts does not hide data from the master table.

### Trail Gap Calculator

Select any benchmark city and see exactly what it would take for your highlighted city to match that ratio:

- **Miles needed** to reach parity
- **Estimated investment range** based on customizable cost-per-mile inputs
- Toggle the target metric between Mi/10k and Pop/Mile

### Highlight City

Any city in the dataset can be set as the "highlighted" city (default: Castle Rock, CO). The highlighted city:

- Appears in **orange** across all charts, the scatter plot, the location map, and the data table
- Serves as the **baseline** in the Trail Gap Calculator

### Castle Rock Trail Mileage Card

A collapsible reference card (collapsed by default) breaking down Castle Rock's ~41 miles of dirt, natural-surface trail open to mountain biking — town-managed systems (Ridgeline, Philip S. Miller Park, Metzler, Quarry Mesa/Rhyolite, Santa Fe Quarry) and regional MTB-legal trails (Macanta, Hidden Mesa). Sourced from [crgov.com](https://www.crgov.com).

### Add Custom Locations

Add any city not in the default dataset directly from the UI:

- Required: City Name, Population, Trail Miles
- Optional: City Area (sq mi), 5-Year Growth (mi)
- All metrics (mi/10k, pop/mile, trail density) are auto-calculated and appended live to the charts and table

> Cities added this way are session-only (they reset on reload) and do not appear on the location map. To add a city **permanently** — and put it on the map — edit the `SEED` array in `index.html` (see below).

### Share & Export

- **Copy Link** — encodes the current view (units, theme, active population tiers, highlighted city, benchmark, chart mode, and cost inputs) into the URL. Anyone opening that link lands on the same configuration.
- **Export PDF** — opens a print-optimized, ink-friendly report with all sections expanded and a summary banner of the active selections. Use your browser's "Save as PDF" in the print dialog.
- **PMR Home** — a link in the top-right back to [postmillenniumrenaissance.com](https://www.postmillenniumrenaissance.com).

### Units

Toggle between **Imperial** (miles), **Metric** (km), and **Both** — affects charts, tooltips, and the data table simultaneously.

### Color Schemes

Three themes, named for trail surfaces and ordered light → dark:

- **Chalk** — light (pale, high-contrast)
- **Granite** — neutral gray (**default**)
- **Loam** — dark (rich forest-floor dark mode)

All three use a color-blind-safe palette — blue + orange + indigo, no red/green distinction — and the selected theme is preserved in shared links.

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

## Default Dataset (38 Cities)

| City                    | Population | Trail Miles |
| ----------------------- | ---------- | ----------- |
| Copper Harbor, MI       | 100        | 40          |
| East Burke, VT          | 150        | 100         |
| Downieville, CA         | 200        | 80          |
| Carrabassett Valley, ME | 750        | 80          |
| Crested Butte, CO       | 1,650      | 450         |
| Crosby, MN              | 2,300      | 70          |
| Oakridge, OR            | 3,200      | 350         |
| Moab, UT                | 5,200      | 150         |
| Makawao, HI (Maui)      | 7,400      | 15          |
| Brevard, NC             | 7,700      | 300         |
| Park City, UT           | 8,400      | 450         |
| Sedona, AZ              | 9,600      | 200         |
| Fruita, CO              | 14,100     | 130         |
| Durango, CO             | 19,500     | 40          |
| Golden, CO              | 20,400     | 35          |
| Anniston, AL            | 21,000     | 35          |
| Marquette, MI           | 22,100     | 75          |
| Squamish, BC            | 24,000     | 200         |
| Helena, MT              | 34,000     | 85          |
| Prescott, AZ            | 46,000     | 50          |
| Poway, CA               | 48,000     | 30          |
| Harrisonburg, VA        | 51,000     | 110         |
| Draper, UT              | 51,000     | 65          |
| Carson City, NV         | 58,600     | 40          |
| Bentonville, AR         | 64,800     | 300         |
| Grand Junction, CO      | 66,000     | 55          |
| Ocala, FL               | 71,700     | 80          |
| Flagstaff, AZ           | 76,800     | 60          |
| **Castle Rock, CO**     | **84,000** | **41.3**    |
| Duluth, MN              | 88,600     | 100         |
| Santa Fe, NM            | 89,000     | 115         |
| Bellingham, WA          | 96,000     | 120         |
| Bend, OR                | 104,000    | 100         |
| Chattanooga, TN         | 184,000    | 125         |
| Boise, ID               | 236,000    | 190         |
| Reno, NV                | 268,000    | 90          |
| Anchorage, AK           | 291,000    | 110         |
| Austin, TX              | 980,000    | 150         |

Trail-mile values reflect dirt, natural-surface singletrack open to mountain biking within or immediately adjacent to city limits. See [Data Sources and Methodology](#data-sources-and-methodology) for caveats.

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

## Updating & Adding Data

All of the dashboard's built-in data lives in a single `SEED` array near the top of the `<script>` block in `index.html`. Every city is one object; all derived metrics (`milesper10k`, `popPerMile`, `trailsPerSqMi`, `growthPct`) are computed automatically by the `enrich()` function on page load. **You only ever edit the raw fields** — never the calculated ones.

### City record fields

```js
{
  city:"Castle Rock, CO",   // Name + state/province — must be unique
  population:84000,          // Estimated population (integer)
  trails:41.3,              // Dirt singletrack miles open to MTB (number; decimals OK)
  areaSqMi:34.8,            // Municipal area in sq mi — or null if unknown/misleading
  milesAdded5yr:null,       // Miles added in the last 5 years — or null if unknown
  lat:39.37, lng:-104.86,   // Coordinates — required for the city to appear on the map
  region:"conus"            // Optional: "ak" or "hi" to plot in the Alaska/Hawaii inset;
                            //   omit (or "conus") for the lower 48 + Canada
}
```

### Updating trail mileage or population for an existing city

When a new trail phase opens, a re-count happens, or a census update lands:

1. Find the city's object in the `SEED` array.
2. Change the `trails` value (for new/updated mileage) and/or the `population` value.
3. Save. That's it — every chart, ratio, gap calculation, and table cell recalculates automatically on the next page load. No other edits are needed.

Example — Castle Rock opens 6 new miles at Ridgeline:

```js
// before
{ city:"Castle Rock, CO", population:84000, trails:41.3, areaSqMi:34.8, milesAdded5yr:null, lat:39.37, lng:-104.86 },
// after
{ city:"Castle Rock, CO", population:84000, trails:47.3, areaSqMi:34.8, milesAdded5yr:6, lat:39.37, lng:-104.86 },
```

(Setting `milesAdded5yr` also lights up the "5yr Growth" column for that city.)

### Adding a new city

Add a new object anywhere in the `SEED` array — order doesn't matter, since the app sorts dynamically:

```js
{ city:"Whistler, BC", population:14000, trails:155, areaSqMi:94.5, milesAdded5yr:null, lat:50.12, lng:-122.95 },
```

Checklist for a new city:

- **`city`** — include the state/province abbreviation and keep it unique.
- **`trails`** — count dirt, natural-surface singletrack that is open to mountain biking and within (or immediately adjacent to) city limits. Be conservative and cite a source in your commit message or a PR.
- **`areaSqMi`** — use the municipal land area. Set it to `null` when the boundary is so large it makes trail density meaningless (e.g., Anchorage's ~1,700 sq mi municipality).
- **`lat` / `lng`** — decimal degrees (west longitudes are negative). **Without these the city works everywhere except the map.** A quick way to get them: right-click the spot in Google Maps and copy the coordinates.
- **`region`** — add `region:"ak"` for Alaska or `region:"hi"` for Hawaii so the dot lands in the correct inset. Leave it off for everywhere else.

After saving, the header's city count, all filters, charts, the map, and the table update automatically — no other code changes required.

### A note on tiers

Population tiers are defined once in the `TIERS` array (just below `SEED`). New cities slot into the right tier automatically based on their `population`. You only touch `TIERS` if you want to change the tier boundaries themselves.

---

## Data Sources and Methodology

Trail mileage figures are estimates compiled from:

- Local trail organization websites and Trailforks listings
- Municipal parks and recreation department publications (e.g., crgov.com for Castle Rock)
- IMBA and regional trail coalition reports
- Community-contributed data and Pinkbike forum sources

Population figures are based on recent municipal estimates and U.S./Canadian census data.

**These are approximate estimates, not official figures.** Methodology notes:

- Trail mileage targets dirt, natural-surface singletrack open to mountain biking. It may include trails on adjacent lands managed by different jurisdictions (national forest, BLM, county open space, state land).
- City area data (`areaSqMi`) uses approximate municipal boundary measurements. Small incorporated towns whose trail systems extend significantly onto surrounding public lands will show inflated trail-density scores, and very large municipalities (e.g., Anchorage) may have `areaSqMi` set to `null` to avoid a misleadingly low density.

**Always verify figures with local trail organizations and municipal planning departments before citing in formal documents, grant applications, or public presentations.**

---

## Tech Stack

| Layer        | Technology                                    |
| ------------ | ---------------------------------------------- |
| Structure    | Plain HTML                                      |
| Styling      | Inline `<style>` block, CSS custom properties for theming (Chalk / Granite / Loam), no build dependencies |
| Logic        | Vanilla JavaScript (no framework)               |
| Map          | Hand-built inline SVG, lat/lng projected in vanilla JS — no mapping library |
| Regression   | Custom log-linear regression (vanilla JS)       |
| Sharing      | URL query-string state via the History API; print-to-PDF via native browser print |
| Deployment   | GitHub Pages, embedded via iframe on Pinkbike / postmillenniumrenaissance.com |

No build tool, package manager, or framework required. Just a browser.

---

## Roadmap / Potential Enhancements

- [x] Export to PDF for council presentations
- [x] Shareable URL state (encode filter/highlight settings in query params)
- [x] Location map with per-city dots (incl. Alaska & Hawaii insets)
- [ ] Public land acreage field (`publicAcres`) for a cleaner trail-density metric
- [ ] Coordinates field in the in-app Add Location form (so custom cities appear on the map)
- [ ] Log scale toggle for bar charts to reduce outlier distortion
- [ ] Year-over-year growth chart (sparklines per city)

---

## Contributing

Pull requests welcome. If you have accurate trail mileage data for a city not in the dataset, or corrections to existing figures, please open an issue with a source link. When adding a city, include `lat`/`lng` (and `region` for AK/HI) so it shows up on the map — see [Updating & Adding Data](#updating--adding-data).

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
