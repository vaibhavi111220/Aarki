# Aarki
End-to-end analytics project solving Aarki’s Product Analyst Challenge includes data cleaning, exploratory analysis, statistical modeling, and business recommendations using Python (pandas, statsmodels, matplotlib). Focused on understanding lead quality trends and actionable levers for improvement.
## 📊 Problem Overview

The dataset (~8,800 leads) tracks leads across various campaigns, ad creatives, and partners.  
Each lead has a final `CallStatus` (e.g., *Closed*, *EP Sent*, *Unable to Contact*, *Invalid Profile*, etc.), as well as contextual metadata such as ad widget, campaign, partner, scores, and state.

The assignment required answering three core questions:

1. Are we seeing any **lead quality trends over time**? Are they statistically significant?  
2. What can we learn about the **drivers of lead quality** (by ad, source, audience, etc.)?  
3. If the advertiser offered a **CPL increase (30 → 33)** for a **20% lift in quality (8.0% → 9.6%)**, what opportunities exist to reach that goal?

---

## 🧠 Approach & Methodology

### 1. Data Cleaning
- Parsed dates (`LeadCreated`, `WeekStart`)  
- Normalized `CallStatus` and derived flags:
  - `IsGoodLead` = 1 for *Closed*, *EP Sent/Received/Confirmed*
  - `IsClosed` = 1 for *Closed* only
- Ensured numeric conversions for `AddressScore`, `PhoneScore`

### 2. Exploratory Analysis
- Weekly aggregation to measure **lead quality rate (Good / Total)**  
- Visualized time trends (`weekly_quality_rate.png`)  
- Fitted **logistic regression** (`IsGoodLead ~ week`) to test statistical trend significance

### 3. Segmentation & Drivers
- Grouped leads by key dimensions (`WidgetName`, `Partner`, `PublisherCampaignName`, `AdvertiserCampaignName`, `State`, etc.)  
- Computed segment-level quality rates and volumes  
- Performed **Chi-square tests** to assess significance of categorical differences  
- Visualized AddressScore & PhoneScore vs quality

### 4. Optimization & Strategy Simulation
- Identified high-performing segments ≥9.6% quality  
- Simulated filtering on high-quality Address/Phone scores (≥4)  
- Estimated trade-offs between volume reduction and quality uplift

---

## 📈 Results Summary

| Metric | Value |
|---------|--------|
| Total Leads | 8,819 |
| Good Leads | 393 |
| Good Rate | 4.46% |
| Closed Leads | 245 |
| Close Rate | 2.78% |
| Trend | No significant change over time (p > 0.05) |

- Quality is stable over time (no improving trend).  
- Major differences exist across **ad creatives (WidgetName)**, **partners**, and **lead sources**.  
- **Higher Address/Phone scores** strongly correlate with higher-quality leads.  
- Filtering or reallocating traffic can improve quality without hurting advertiser ROI.

---

## 🛠️ Tech Stack

- **Language:** Python 3  
- **Libraries:** pandas, numpy, matplotlib, seaborn, statsmodels, scipy  
- **Environment:** Jupyter / VS Code  
- **Outputs:** CSV summaries, charts, and statistical results in `/lead_analysis_outputs/`

---
