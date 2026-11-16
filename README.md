# Global Adolescent Girls Demographic Analysis (2023 Snapshot)
An exploratory data analysis (EDA) and visualization project utilizing UNICEF's Statistical Data and Metadata eXchange (SDMX) dataset to evaluate the global distribution of adolescent girls (aged 10–19) and identify high-priority regions for international development and policy investment.

---

## 📌 Project Overview

Understanding where the world's adolescent population is concentrated is critical for allocating funding toward secondary education, healthcare, digital literacy, and child protection. 

In this project, raw SDMX demographic records (`adolescent girls.csv`) were cleaned, stripped of macro-level regional and income-bracket aggregations, mapped to standardized ISO country identifiers, and visualized to uncover actionable policy insights for UNICEF stakeholders.

### Key Research Questions
1. Which individual countries hold the largest populations of adolescent girls globally?
2. How do macro-level regional and income-bracket aggregations distort raw country-level rankings in SDMX datasets?
3. Where are the most critical demographic windows and youth surges occurring across South Asia and Sub-Saharan Africa?

---

## 📊 Key Findings & Policy Insights

* **Global Epicenter in Lower-Middle Income Economies:** Macro-level filtering revealed that **World Bank Lower-Middle Income (`WB_LMI`)** countries and **South Asia (`UNSDG_SOUTHASIA`)** represent the largest global concentration of adolescent girls.
* **India’s Unprecedented Scale & Demographic Dividend:** Ranking #1 globally with over **121.07 million** adolescent girls, India represents a pivotal demographic window. Strategic investments in secondary education, digital literacy, and adolescent health are essential to transition this cohort into a strong economic engine.
* **Nigeria’s Rapid Youth Surge:** Anchoring Sub-Saharan Africa's demographic boom alongside major Asian populations (India, China, and Pakistan), Nigeria sits on a steeply rising youth curve—requiring scalable social, health, and educational infrastructure to prevent systemic bottlenecks.
* **Pivotal Frontlines for Global Targets:** Achieving international equity and development targets relies heavily on policy execution and targeted funding across South Asia and Sub-Saharan Africa.

---

## 🛠️ Data Pipeline & Methodology

Working with UN/SDMX global datasets presents specific structural challenges that were resolved through a reproducible Python pipeline:

1. **Metadata Pruning & Whitespace Sanitization:**
   * Stripped hidden leading/trailing whitespace across string fields (`INDICATOR`, `REF_AREA`, `SEX`).
   * Dropped low-value administrative tracking columns (`STRUCTURE`, `STRUCTURE_ID`, `ACTION`) while retaining critical statistical provenance (`DATA_SOURCE`).
   * Preserved conditionally populated columns (`LOWER_BOUND`, `UPPER_BOUND`) rather than dropping nulls globally.
2. **Type Casting & Snapshot Verification:**
   * Cast `OBS_VALUE` and `TIME_PERIOD` from string objects to numeric types (`pd.to_numeric`) to enable accurate sorting and filtering.
   * Verified temporal granularity, confirming the extract represents a cross-sectional **2023 snapshot** (~641.3 million adolescent girls globally).
3. **Isolating Individual Countries (The Underscore Rule):**
   * UN SDMX files bundle macro-aggregates (e.g., `WORLD`, `WB_LMI`, `UNSDG_SOUTHASIA`, `UNICEF_SA`) alongside individual nations.
   * Applied regex filtering (`~clean_data['REF_AREA'].str.contains('_', na=False)`) combined with manual global-code exclusions to isolate true ISO 3166-1 alpha-3 country codes.
4. **Visualization:**
   * Built publication-ready horizontal bar charts using `matplotlib` and `seaborn` with direct data-label annotations.

---

## 💻 Tech Stack

* **Language:** Python 3.x
* **Data Manipulation:** `pandas`, `numpy`
* **Data Visualization:** `matplotlib`, `seaborn`
* **Environment:** Jupyter Notebook

---

## 📁 Repository Structure

```text
├── data/
│   ├── raw/
│   │   └── adolescent girls.csv          # Raw UNICEF SDMX dataset extract
│   └── processed/
│       └── cleaned_country_adolescent_2023.csv  # Filtered country-level 2023 dataset
├── notebooks/
│   └── unicef_adolescent_girls_eda.ipynb # Complete data cleaning, diagnostics & plotting
├── visuals/
│   └── top_10_countries_adolescent_girls_2023.png # Final Seaborn visualization
└── README.md

##check the "Release" to download the csv file
