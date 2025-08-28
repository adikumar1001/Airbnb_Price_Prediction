# 🏡 Airbnb Price Prediction — Bozeman, Montana (Listings + Reviews)

End‑to‑end project to **predict nightly prices** for Airbnb listings by combining **structured attributes** (bedrooms, bathrooms, amenities, location) with **review sentiment**. Includes robust cleaning, feature engineering, clustering, model benchmarking, and business recommendations.

> Highlights: strongest signals were **bedrooms, bathrooms, amenities, and location**; **Neural Network and Random Forest** performed best among tested models. fileciteturn2file0

---

## 🔎 What’s inside
- **Exploratory Data Analysis & Cleaning** for `listings`, `reviews`, and `calendar` datasets.
- **Feature engineering**: amenities parsing → binary flags, geo‑clustering from lat/long, date‑derived features (e.g., `host_since_days`), VIF & correlation‑based multicollinearity pruning. fileciteturn2file0
- **Sentiment analysis** of reviews using **VADER** with a **custom lexicon**; merged per‑listing sentiment back to the model table. fileciteturn2file1
- **Models compared**: Linear Regression, Random Forest, XGBoost, Neural Network; **NN ~0.62 R² (test)**, RF/XGB around **~0.54–0.55 R² (test)** in the reported runs. fileciteturn2file0

---

## 📂 Repository structure (suggested)
```
.
├─ notebooks/
│  └─ Airbnb Price prediction.ipynb            # Full pipeline: EDA → FE → modeling → plots
├─ docs/
│  ├─ Airbnb Price prediction.pdf              # Written report
│  └─ Final Project Presentation - Group 11.pptx
├─ data/
│  ├─ listings.xlsx
│  ├─ reviews.xlsx
│  └─ calendar.xlsx
├─ README.md
└─ requirements_airbnb.txt
```

> File names mirror your current assets; if your Excel files use slightly different names, update the notebook’s data‑loading cell.

---

## ⚙️ Quickstart
```bash
# 1) Create & activate a virtual env
python -m venv .venv && source .venv/bin/activate     # (Windows) .venv\Scripts\activate

# 2) Install deps
pip install -r requirements_airbnb.txt

# 3) Run the notebook
jupyter lab  # or: jupyter notebook
# Open notebooks/Airbnb Price prediction.ipynb and run cells top→bottom
```

**Colab:** upload the notebook + Excel files (or mount Drive) and `pip install -r` content in the first cell.

---

## 🧹 Data prep & feature engineering
- **Cleaning**: drop high‑NA columns; impute key fields (e.g., price, review scores); cap outliers (e.g., `price`, `minimum_nights`). fileciteturn2file1  
- **Text → features**: parse **amenities** into binary indicators (e.g., `hot_tub`, `air_conditioning`, `elevator`, `netflix`). fileciteturn2file1  
- **Dates → features**: `host_since_days`, `first_review_days`, `last_review_days`. fileciteturn2file0  
- **Geo‑clusters**: K‑Means on `(lat, long)` to capture neighborhood effects. fileciteturn2file0  
- **Multicollinearity controls**: remove highly‑correlated pairs (|r| ≥ 0.75) and iteratively drop features with **VIF > 20**. fileciteturn2file0

---

## 💬 Review sentiment
- **VADER** polarity with **custom lexicon** (domain tweaks like “cozy”, “cancelled”).  
- Per‑listing **average sentiment** merged back to listings; used as a price predictor. fileciteturn2file1

---

## 🤖 Modeling
- **Linear Regression** — baseline; interpretable coefficients.  
- **Random Forest** — nonlinear, interaction‑aware; strong baseline.  
- **XGBoost** — regularized boosting, robust to outliers; good test R² (~0.545). fileciteturn2file0  
- **Neural Network** — captured the most variance on test (**R² ≈ 0.62**). fileciteturn2file0

**Frequently important features** across models: **bedrooms, bathrooms**, minimum nights, availability metrics, review volume, and **average sentiment**; location via **geo‑clusters** also contributes. fileciteturn2file0

---

## 🧪 QA checklist
- Column types (dates, numeric flags) validated after import.  
- No data leakage: fit scalers/encoders on **train only**.  
- Train/test split is stratified or randomly seeded; metrics reported on **held‑out** test.  
- Review that **amenities parsing** is case‑insensitive and robust to punctuation.

---

## 🔮 Ideas / next steps
- Add **regularized linear** (Lasso/Ridge/ElasticNet) and **CatBoost/LightGBM** comparisons.  
- SHAP for model explainability; partial‑dependence plots for top features.  
- Incorporate **seasonality** (calendar features) and spatial encodings (H3 grid).

---

## 📚 Documentation
- Full write‑up in **`docs/Airbnb Price prediction.pdf`** with methods, figures, and detailed metrics. fileciteturn2file0

---

## 👤 Authors
Aditya Kumar · Mariappan · Timothy — shared EDA/cleaning; model ownership: **LR/RF** (Mariappan), **XGBoost** (Timothy), **Neural Network** (Aditya). fileciteturn2file0

