# Customer-segmentation
Customer segmentation



# customer-behaviour-analytics
group the customer according the  behaviour


# Customer Behaviour Analytics — Targeted Marketing with ML

**Segment customers and predict campaign response to cut spend and lift ROI.**  
K-Means segments + Random Forest classification to target the right people with the right offer.

---

## 🚀 TL;DR
- **Business**: Stop blanket campaigns. Aim offers at customers who actually convert.
- **Approach**:  
  - **Segmentation**: K-Means (K=3) for behaviour-driven customer groups  
  - **Prediction**: Random Forest vs Logistic Regression → RF chosen for stronger response detection
- **Outcomes**: Actionable segments (VIPs, mid-tier, price-sensitive) and a response model to **reduce campaign waste** and **increase ROI**.

---

## 🧩 Problem & Goals
### Business Problem
Marketing dollars are spread across everyone, leading to low engagement and wasted budget.

### Goals
- **Business**: Personalize campaigns by segment; focus spend on likely responders.  
- **Analytical**: (1) Build segments that reflect real shopping behaviour; (2) Predict **who** will respond to a campaign.

---

## 📦 Data (overview)
- **Entities**: customer demographics, spend by category (wines, meat, fish, sweets, gold), channels (web/catalog/store), visits, past campaign responses.
- **Target (classification)**: `Target_Response` (1 if a customer accepted **any** past campaign; else 0).
- **Key prep**
  - Clean/encode, handle missing values
  - Generate **Age/Generation**, **Income_Bracket**, **Recency_Bin**
  - Normalize features for clustering
  - Split for classification: **70/15/15** train/val/test

---

## 🛠️ Feature Engineering
- Date → **year / month / day / weekday**, **recency bins**  
- Demographics → **generation**, **income brackets**  
- Behaviour → purchase counts (web/catalog/store), web visits/month, spend by category  
- Target construction → **`Target_Response`** from prior campaign flags

---

## 🔎 EDA: What Predicts Engagement?
- Higher **spend** (wine/meat/gold) and **multi-channel purchasing** align with higher campaign response.  
- **Web visits** and **catalog/store purchases** correlate with responsiveness.  
- Basic demographics matter less than **behavioural signals**.

---

## 🤖 Modeling (Classification)
**Models compared**: Logistic Regression, Random Forest  
**Metrics**: Accuracy, Precision, Recall (Sensitivity), Specificity, Balanced Accuracy, Confusion Matrix

- **Logistic Regression (validation snapshot)**  
  Accuracy ~**76.8%**, **Recall ~33.3%**, **Specificity ~90.8%**, Balanced Acc ~**62.1%**.  
  Interpretable, but recall is limited for catching true responders.

- **Random Forest (selected)**  
  Captures nonlinear interactions; **higher recall & precision** than LR and better overall balance.  
  Used to **score customers** and drive targeted outreach.

> **Why RF?** For marketing, **missing a true responder is costly**. RF provided materially better sensitivity and overall performance than LR.

---


## 👥 Segmentation (Unsupervised)
- **Algorithm**: K-Means on normalized features  
- **K = 3** (elbow method) with moderate separation (silhouette ≈ 0.14)

**Segments**
1) **High-Value Loyalists** — highest spend, respond to campaigns, active across channels  
2) **Mid-Tier Multi-Channel** — balanced spend/engagement, good growth potential  
3) **Price-Sensitive Browsers** — low spend and low response; target with low-cost re-engagement

> Also ran **Hierarchical (Ward.D2)** to study structure and validate K=3; clusters were less separated but directionally consistent.

---





