# Screen Time & You

**Computational Practices: Visualisation and Sensing**

**Live site:** https://controlmyspace.github.io/Computational-Practices-Visualisation-and-Sensing/

---

## About

An interactive, scrollable data story exploring what the world's largest school study (OECD PISA 2022), covering 690,000 students across 81 countries, actually says about screen time in correlation to academic performance.

The central question: **is screen time hurting students, or is the picture more complicated?**

The site guides the reader through five sections, each revealing a different layer of the data: classroom distraction rates by country, the relationship between leisure screen time and maths scores, a scrollytelling D3 chart showing the "sweet spot" effect, a quiz, and a belonging index explorer. It ends with an honest critical audit of the dataset's limitations.

---

## Repository contents

| File | About |
|---|---|
| `index.html` | The full interactive visualisation — single-file HTML/CSS/JS |
| `pisa_analysis.ipynb` | Jupyter notebook: data cleaning, analysis, and export using pandas |
| `pisa_data.json` | Cleaned dataset exported from the notebook, loaded by the site via Fetch API |
| `raw data.xlsx` | Original PISA 2022 data extracted from OECD Excel tables (Figures 2, 3, II.3.4) |
| `fig1_distraction_analysis.png` | Exploratory chart: distraction rates by country |
| `fig3_scores_by_screentime.png` | Exploratory chart: maths scores by screen time bracket |
| `fig_belonging.png` | Exploratory chart: sense of belonging index |
| `portfolio_documentation.docx` | Full portfolio write-up (process, decisions, reflections) |

---

## How to open

A single HTML file, so no build tools or dependencies are needed.  


## Data source

**OECD PISA 2022 Results, Volume II** — Students' Learning Environment
OECD (2023). doi: [10.1787/53f23881-en](https://doi.org/10.1787/53f23881-en)

Specific figures used:
- **Figure II.3.4** — Percentage of students distracted by digital devices in most maths lessons, by country
- **Figure 2** — Average maths scores by daily learning screen time bracket (6 brackets)
- **Figure 3** — Average maths scores by daily leisure screen time bracket, by activity type (5 brackets)
- **Tables 43 & 44** — Sense of belonging index by screen time bracket

The raw Excel file was downloaded from the OECD iLibrary. The notebook (`pisa_analysis.ipynb`) handles all cleaning: renaming columns, filtering OECD averages, reshaping wide tables into tidy format (Wickham, 2014), and exporting `pisa_data.json` for the frontend code.

---

## Technical overview

### Frontend (`index.html`)
- **D3.js v7** — scrollytelling line chart with animated path drawing, interactive tooltips, and a highlighted "sweet spot" zone
- **Scrollama v3** — scroll-driven step activation that progressively reveals chart layers
- **Tone.js v14** — sonification: maths scores are mapped to audio frequency (220–440 Hz) so you can *hear* the score change as you drag the slider
- **Vanilla JS** — everything else: classroom animation, country explorer with Fetch API, score slider, belonging mood panel, quiz engine
- **CSS custom properties** — full design system (colour tokens, typography scale, responsive layout)
- No frameworks, no bundler — runs in any modern browser

### Data pipeline (`pisa_analysis.ipynb`)
- **pandas** — data loading from Excel, column renaming, filtering, reshaping
- **matplotlib** — exploratory visualisations (the three `.png` files in the repo)
- Output: `pisa_data.json` with a `distraction_by_country` array consumed by the frontend's country explorer via `fetch()`

### Narrative structure
The site follows Freytag's Pyramid (introduced in Week 4 of the course):
- **Exposition** — classroom distraction rates
- **Rising action** — scores drop with more screen time
- **Climax** — the sweet spot chart (not all screen time is equal)
- **Resolution** — connection, belonging, and what the data can't tell us

---

## Critical data practice

The site includes an explicit audit section applying feminist data practice principles (D'Ignazio & Klein, 2020):

- **Who is this data for?** PISA only surveys 15-year-olds in formal schools — it excludes dropouts, home-schooled students, and regions that didn't participate
- **Correlation ≠ causation** — students with lower scores may use screens more because they're already disengaged, not the other way around; the OECD acknowledges this
- **What's missing?** Only maths scores are measured; creativity, wellbeing, and social skills aren't captured; screen time content isn't disaggregated by class, gender, or race
- **One suggested redesign** — filtering by country income group, since access to devices is a privilege in many lower-income contexts, which would change the story considerably

---

## Libraries and credits

| Library | Version | Purpose |
|---|---|---|
| D3.js | 7.9.0 | Chart rendering, scales, axes, path animation |
| Scrollama | 3.2.0 | Scroll-driven storytelling |
| Tone.js | 14.8.49 | Data sonification |
| Google Fonts | — | Fraunces (display) + DM Sans (body) |

All loaded from CDN — no npm install needed.

---

## References

Cairo, A. (2012). *The Functional Art*. Peachpit Press.

D'Ignazio, C. and Klein, L.F. (2020). *Data Feminism*. MIT Press.

Feigenbaum, A. and Alamalhodaei, A. (2020). *The Data Storytelling Workbook*. Routledge.

Fry, B. (2008). *Visualising Data*. O'Reilly Media.

McKinney, W. (2022). *Python for Data Analysis*, 3rd ed. O'Reilly Media. Available at: https://wesmckinney.com/book/

Meeks, E. and Dufour, A.M. (2024). *D3.js in Action*. Simon & Schuster.

Murray, S. (2017). *Interactive Data Visualization for the Web*. O'Reilly Media.

OECD (2023). *PISA 2022 Results Volume II: Students' Learning Environment*. OECD Publishing. doi: 10.1787/53f23881-en

Pecnut (no date). *Data Processing with Pandas*. GitHub. Available at: https://github.com/Pecnut/course-pandas

Tufte, E. (2001). *The Visual Display of Quantitative Information*, 2nd ed. Graphics Press.

Wickham, H. (2014). Tidy Data. *Journal of Statistical Software*, 59(10). Available at: https://r4ds.had.co.nz/tidy-data.html

Yau, N. (2011). *Visualise This*. John Wiley & Sons.
