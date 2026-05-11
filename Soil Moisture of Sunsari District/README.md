# 🌱 Soil Moisture Proxy — Sunsari District, Nepal

A Google Earth Engine (GEE) + Python pipeline that derives a long-term **soil moisture proxy** for Sunsari District, Nepal using Sentinel-1 SAR backscatter data. The notebook combines ascending and descending orbit passes, applies speckle filtering and land masking, and performs trend analysis over the 2014–2025 period.

---

## 📍 Study Area

| Parameter | Value |
|-----------|-------|
| District | Sunsari, Nepal |
| Bounding box | 87.06°E – 87.36°E, 26.60°N – 26.95°N |
| Analysis window | 87.12°E – 87.18°E, 26.70°N – 26.76°N |
| Time range | 2014-01-01 → 2025-12-31 |

---

## 🛠️ How It Works

The pipeline runs in eight steps:

1. **Initialize** — Authenticates and initializes the GEE Python API.
2. **Define area & time range** — Sets the study polygon and chart area as GEE geometries.
3. **Build SAR collections** — Filters the `COPERNICUS/S1_GRD` collection for IW mode, VV polarisation, then splits into ascending and descending orbit sub-collections.
4. **Pre-process** — Creates 10-day composites, converts dB to sigma-naught (linear backscatter), applies a 30 m focal-mean speckle filter, and masks out water/built-up areas using Dynamic World land cover.
5. **Normalise** — Min-max normalises each collection to produce a 0–1 soil moisture proxy.
6. **Extract time series** — Reduces each composite to a mean value over the chart area at 30 m scale and downloads the results as a Pandas DataFrame.
7. **Combine passes** — Snaps both orbits to the same 10-day window grid, merges on matching windows, and averages ascending + descending values into a single combined SM series.
8. **Analyse & plot** — Computes a linear trend (scipy `linregress`), a 90-day rolling mean, and produces a three-panel figure with a summary statistics printout.

---

## 📊 Output

**Figure: `sm_combined_trendline.png`** — A three-panel plot saved to the working directory:

| Panel | Content |
|-------|---------|
| Top | Ascending orbit raw scatter + rolling mean |
| Middle | Descending orbit raw scatter + rolling mean |
| Bottom | Combined SM, 90-day rolling mean, and linear trendline with R², p-value, and annual-change annotation |

**Console summary** — Prints data range, point count, mean SM, annual change (%), R², and significance of the trend.

---

## ⚙️ Requirements

```
earthengine-api
numpy
pandas
matplotlib
scipy
```

Install all dependencies with:

```bash
pip install earthengine-api numpy pandas matplotlib scipy
```

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

### 2. Authenticate with Google Earth Engine

```bash
earthengine authenticate
```

You will need a GEE-enabled Google Cloud project. Sign up at [earthengine.google.com](https://earthengine.google.com).

### 3. Set your project ID

Open `Soil_Moisture.ipynb` and update the initialisation cell:

```python
ee.Initialize(project='your-project-id')  # ← replace this
```

### 4. Run the notebook

```bash
jupyter notebook Soil_Moisture.ipynb
```

Data retrieval from GEE typically takes **1–2 minutes**. The final plot is saved as `sm_combined_trendline.png` in the working directory.

---

## 🔑 Key Parameters

These can be adjusted at the top of the notebook to adapt the analysis to a different region or time period:

| Variable | Description | Default |
|----------|-------------|---------|
| `sunsari` | Study area polygon | Sunsari District, Nepal |
| `chart_area` | Extraction rectangle | 87.12–87.18°E, 26.70–26.76°N |
| `start` / `end` | Date range | 2014-01-01 / 2025-12-31 |
| Composite interval | Days per composite | 10 |
| Speckle filter radius | Focal mean radius | 30 m |
| Rolling window | Rolling mean window | 9 composites (~90 days) |

---

## 📡 Data Sources

| Dataset | Description |
|---------|-------------|
| [`COPERNICUS/S1_GRD`](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S1_GRD) | Sentinel-1 C-band SAR Ground Range Detected imagery |
| [`GOOGLE/DYNAMICWORLD/V1`](https://developers.google.com/earth-engine/datasets/catalog/GOOGLE_DYNAMICWORLD_V1) | Dynamic World near-real-time land use/land cover |




