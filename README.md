# 🔍 Discount or Deceit?
## Uncovering Retail Fraud Patterns with Hierarchical Clustering

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.3+-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.0+-150458?style=flat&logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-1.11+-8CAAE6?style=flat&logo=scipy&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-2A9D8F?style=flat)

---

## 📌 Project Description

This project applies **Agglomerative Hierarchical Clustering** to 9,994 retail
transactions from the Sample Superstore dataset (2014–2017) to segment customers
by purchasing behaviour and surface hidden anomalies in the data.

What began as a customer segmentation exercise uncovered something far more
significant: a statistically improbable pattern of maximum-level discount abuse
concentrated exclusively in one geographic region — a strong indicator of
internal misconduct.

The project demonstrates how unsupervised machine learning, when applied
thoughtfully, goes beyond clustering to become a fraud detection tool — surfacing
signals that traditional reporting would never flag.

---

## 🚨 Key Finding

> **All 300 orders with the maximum 80% discount originated exclusively from the
> Central region — specifically Texas (200 orders) and Illinois (100 orders).
> Zero maximum-discount orders came from any other region across 4 years.**

This concentration is statistically impossible by chance and points strongly to
systematic discount policy violations by one or more individuals with
discount-override access in the Central region.

---

## 📊 Dataset

| Attribute | Detail |
|---|---|
| **Source** | Sample Superstore (widely used retail analytics dataset) |
| **Period** | 2014 – 2017 |
| **Total Transactions** | 9,994 order line items |
| **Unique Customers** | 793 |
| **Total Revenue** | $2,297,201 |
| **Net Profit** | $286,397 |
| **Categories** | Furniture, Office Supplies, Technology |
| **Regions** | Central, East, South, West |

---

## 🔢 Critical Statistics

| Metric | Value |
|---|---|
| Loss-making orders | 1,871 (18.7%) |
| Total losses recorded | $156,131 |
| Discount-related losses | $97,065 |
| Orders at max 80% discount | 300 |
| Region of all 80% disc. orders | **Central only** |
| Central avg discount | 24% (vs West: 11%) |
| Central loss-making order rate | 31.9% (vs West: 9.9%) |
| Worst sub-category | Tables (−$17,725 total profit) |

---

## 🧠 Methodology

```
Raw Data (9,994 rows)
        │
        ▼
Feature Engineering ──► Aggregate to 793 customer-level rows
        │                 Total Sales · Total Profit
        │                 Total Quantity · Avg Discount
        ▼
Pre-processing ──────► StandardScaler (distance-based algorithm)
        │
        ▼
Hopkins Statistic ───► Validate cluster tendency before fitting
        │
        ▼
Linkage Matrix ──────► Ward linkage (minimises within-cluster variance)
        │
        ▼
Dendrogram ──────────► Visual merge history + Cophenetic Correlation check
        │
        ▼
Silhouette Sweep ────► Test k = 2 to 8, select optimal k
        │
        ▼
AgglomerativeClustering ► Fit final model, assign cluster labels
        │
        ▼
Cluster Profiling ───► Mean stats, segment distribution, feature heatmap
        │
        ▼
Fraud Investigation ─► Discount anomalies, geographic risk, high-loss accounts
```

---

## 📁 Project Structure

```
discount-or-deceit/
│
├── 📓 ML_Hierarchical_Clustering.ipynb   # Main analysis notebook (Google Colab)
├── 📊 Sample_Superstore.xlsx             # Source dataset
├── 📄 Superstore_BI_Fraud_Report.docx   # Full business intelligence report
├── 📑 Superstore_Fraud_Presentation.pptx # Executive presentation (10 slides)
└── 📖 README.md                          # This file
```

---

## 📓 Notebook Structure

| Section | Description |
|---|---|
| 1. Install & Imports | All dependencies, dark matplotlib theme |
| 2. Load & Explore | Shape, dtypes, nulls, descriptive stats |
| 3. Feature Engineering | Customer-level aggregation from order rows |
| 4. Pre-processing | StandardScaler, feature matrix |
| 5. Hopkins Statistic | Cluster tendency validation |
| 6. Linkage & Dendrogram | Ward linkage matrix + Cophenetic Correlation |
| 7. Silhouette Sweep | k=2 to 8 evaluation loop |
| 8. Final Model | AgglomerativeClustering fit + label assignment |
| 9. Cluster Visualisation | Scatter plots: Sales vs Profit, Qty vs Discount |
| 10. Cluster Profiling | Mean stats table, segment distribution, heatmap |
| 11. Fraud Signal — Regional | Central vs all regions: discount, profit, loss rate |
| 12. Fraud Signal — Customers | High-risk accounts: Sales vs Loss, Discount vs Loss bubble |

---

## 📈 Results Summary

### Clustering

| Metric | Value |
|---|---|
| Algorithm | Agglomerative Hierarchical Clustering |
| Linkage method | Ward |
| Optimal k | 2 |
| Silhouette Score | 0.2325 |
| Cophenetic Correlation | ~0.85+ |

> **Note:** The low Silhouette Score (0.23) is itself a meaningful finding — it
> confirms that Superstore customers form a **continuous spectrum** rather than
> discrete groups. This means boundary customers are highly vulnerable to being
> pushed from profitable to loss-making territory by small discount changes —
> exactly what the fraud investigation confirmed.

### Cluster Profiles

| Cluster | Size | Behaviour |
|---|---|---|
| **0 — High Value** | 375 customers | High sales, strong profit, low avg discount (13%) |
| **1 — Risk Group** | 418 customers | Lower sales, thin profit, higher avg discount (18%) |

### Regional Fraud Signal

| Region | Avg Discount | Total Profit | Loss-Making Orders |
|---|---|---|---|
| **Central** | **24%** | **$39,706** | **31.9%** |
| East | 15% | $91,523 | 19.4% |
| South | 15% | $46,749 | 16.0% |
| West | 11% | $108,418 | 9.9% |

### Top Loss-Making Customers (Engineered from Dataset)

| Customer | Total Sales | Total Profit | Avg Discount |
|---|---|---|---|
| Cindy Stewart | $5,690 | −$6,626 | 20% |
| Grant Thornton | $9,351 | −$4,109 | 25% |
| Luke Foster | $3,931 | −$3,584 | 32% |
| Sharelle Roach | $3,233 | −$3,334 | 37% |
| Sean Miller | $25,043 | −$1,981 | 25% |

---

## ⚙️ How to Run

### Option 1 — Google Colab (Recommended)

1. Open [Google Colab](https://colab.research.google.com)
2. Upload `ML_Hierarchical_Clustering.ipynb`
3. Mount Google Drive or use `files.upload()` to load `Sample_Superstore.xlsx`
4. Run all cells (`Runtime → Run all`)

### Option 2 — Local Jupyter

```bash
# Clone the repository
git clone https://github.com/yourusername/discount-or-deceit.git
cd discount-or-deceit

# Install dependencies
pip install scikit-learn scipy matplotlib seaborn openpyxl pandas numpy

# Launch notebook
jupyter notebook ML_Hierarchical_Clustering.ipynb
```

### Dependencies

```txt
pandas>=2.0
numpy>=1.24
matplotlib>=3.7
seaborn>=0.12
scikit-learn>=1.3
scipy>=1.11
openpyxl>=3.1
```

---

## 🧩 Key Concepts Demonstrated

| Concept | Application |
|---|---|
| **Feature Engineering** | Row-level → customer-level aggregation |
| **Hopkins Statistic** | Pre-clustering validation of data structure |
| **Ward Linkage** | Minimising within-cluster variance at each merge |
| **Cophenetic Correlation** | Dendrogram faithfulness diagnostic |
| **Silhouette Score** | Optimal k selection without ground truth labels |
| **Fraud Analytics** | Pattern recognition in discount + profit data |
| **Business Storytelling** | Translating ML output into executive-ready findings |

---

## 📋 Deliverables

- ✅ **Jupyter Notebook** — Full reproducible analysis (Google Colab compatible)
- ✅ **BI Fraud Report** — 7-section Word document with executive KPI dashboards,
  geographic risk maps, cluster profiles, and tiered recommendations
- ✅ **PowerPoint Presentation** — 10-slide executive deck with native editable
  charts, all data engineered directly from the source dataset

---

## 🎯 Business Recommendations

### Immediate (< 30 Days)
- Audit all 300 maximum-discount orders in Texas and Illinois
- Identify which staff accounts approved each transaction
- Suspend single-user discount override above 40% pending investigation

### Short-Term (30–90 Days)
- Implement tiered approval: reps ≤20%, managers ≤40%, VP sign-off above
- Set automated margin alerts before order confirmation
- Conduct pricing review for Tables sub-category (63.6% loss-making order rate)

### Strategic (90+ Days)
- Link sales commissions to profit contribution, not just revenue
- Deploy real-time discount monitoring dashboard by region and rep
- Re-run clustering quarterly with enriched features (return rate, order frequency)

---

## 🛠️ Tools & Stack

| Tool | Purpose |
|---|---|
| Python 3.10+ | Core analysis language |
| Pandas | Data manipulation and feature engineering |
| NumPy | Numerical operations |
| Scikit-learn | AgglomerativeClustering, StandardScaler, Silhouette Score |
| SciPy | Linkage matrix, dendrogram, Cophenetic Correlation |
| Matplotlib / Seaborn | Visualisations |
| Google Colab | Cloud notebook environment |
| Python-docx | BI report generation |
| PptxGenJS | Presentation generation |

---

## 👤 Author

**Efa Godspower**
Data Scientist · NLP/GenAI · Credit Modelling · Behavioural Analytics

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/yourprofile)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=flat&logo=github&logoColor=white)](https://github.com/yourusername)

---

## 📄 License

This project is licensed under the MIT License.
The Sample Superstore dataset is publicly available and widely used for
educational and portfolio purposes.

---

> *"The patterns are too consistent, too geographically concentrated, and too
> financially significant to be explained by normal business variation."*
> — BI Fraud Report, Conclusion
