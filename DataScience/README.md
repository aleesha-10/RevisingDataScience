# python-data-projects

A collection of self-contained Python data science projects I built on the side — covering web scraping, unsupervised ML, and time-series forecasting. Each one is a standalone Jupyter notebook, runs fully in Google Colab, and goes a bit beyond the obvious approach.

---

## Projects

###  QuoteCrawler — Automated Web Scraping Pipeline
*Also could be called: WebHarvest · DataMiner · ScrapeSuite · PipelineCrawler · RawDataEngine*

Automated pipeline that crawls two live public sites end-to-end, extracts structured records from unstructured HTML, cleans the raw text, and persists the output to both CSV and SQLite. Built with retry logic and exponential backoff so it handles dropped connections without dying.

**Stack:** `requests` · `BeautifulSoup` · `pandas` · `sqlite3` · `plotly`

**Highlights:**
- Fault-tolerant crawler with retry + backoff on every request
- Validated against two structurally different sites (quotes + books) to prove the architecture generalizes
- Interactive Plotly analytics layer (tag treemap, author rankings, price distributions)
- Structured JSON run log printed at completion — pages crawled, records extracted, duplicates removed

---

###  CustomerLens — Unsupervised Customer Segmentation
*Also could be called: SegmentIQ · ClusterVision · BehaviorMapper · ShopperDNA · MarketSlice*

Clusters real customer data into behaviorally distinct segments using K-Means, cross-validated against Hierarchical clustering. Translates the math into named business personas with concrete marketing recommendations — not just cluster labels.

**Stack:** `scikit-learn` · `scipy` · `plotly` · `seaborn`

**Dataset:** Mall Customer Segmentation (Kaggle, 200 customers)

**Highlights:**
- Elbow Method + silhouette score to find optimal k (converged on k=4)
- Cross-validated K-Means against Agglomerative (Ward) clustering via Adjusted Rand Index
- Interactive 3D segment explorer, radar profile chart, PCA projection with marginals
- 4 named personas with segment-specific retention/marketing strategy per cluster

---

### FlightCast — Time-Series Forecasting & Interpretability
*Also could be called: TrendSense · SeriesLab · ForecastEngine · TemporalIQ · ProphetBoard*

Fits a Prophet forecasting model to historical airline passenger data, evaluates it properly (not just against itself — against a naive baseline too), and explains the forecast using a SHAP interpretability layer via an XGBoost surrogate.

**Stack:** `prophet` · `xgboost` · `shap` · `statsmodels` · `plotly`

**Dataset:** AirPassengers — monthly international airline passengers, 1949–1960

**Highlights:**
- ADF stationarity test + seasonal differencing pipeline before model fitting
- Prophet benchmarked against a naive seasonal baseline to quantify real model lift
- Rolling-origin cross-validation for a robust accuracy estimate (not just one train/test split)
- 24-month forward forecast beyond the dataset's actual end date
- SHAP TreeExplainer on XGBoost surrogate — `lag_12` found to dominate by 17x over any other feature

---

## How to Run

All notebooks run top to bottom in [Google Colab](https://colab.research.google.com/) — dependencies install in the first cell.

| Notebook | External file needed? |
|---|---|
| `Web_Scraping_Pipeline.ipynb` | No — data fetched live |
| `Customer_Segmentation_Clustering.ipynb` | Yes — upload `Mall_Customers.csv` ([Kaggle](https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python)) |
| `TimeSeries_Forecasting_SHAP.ipynb` | No — data fetched live |

---

## Stack Overview

```
python · pandas · numpy · matplotlib · seaborn · plotly
scikit-learn · scipy · statsmodels
prophet · xgboost · shap
requests · beautifulsoup4 · sqlite3
```