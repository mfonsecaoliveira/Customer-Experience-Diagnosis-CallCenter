# 📞 Customer Experience Diagnosis — Call Center 2020

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=power-bi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-512BD4?style=for-the-badge&logo=databricks&logoColor=white)
![Data Storytelling](https://img.shields.io/badge/Data_Storytelling-7C3AED?style=for-the-badge&logo=bookstack&logoColor=white)

**An end-to-end Power BI investigation that doesn't just answer questions — it builds an argument.**

> Instead of plotting charts to satisfy a brief, this report walks the reader through a diagnosis: a problem, a chain of eliminated suspects, a root cause, and a prioritized recommendation.

🔗 **[View the live interactive report](#)** ·  📂 **[Download the .pbix](./Storytelling_-_CallCenter.pbix)**

---

## 🎯 The Business Problem

A call center closed 2020 with customers in clear distress. The leadership question wasn't *"what happened?"* — it was the harder one:

> **Why are our customers so dissatisfied — and where should we act first?**

This report answers it with a dataset of **13,055 interactions** spanning Jan–Dec 2020, across four channels, six contact reasons, and the full United States.

---

## 🚨 The Headline Numbers

| Metric | Value | What it means |
|---|---|---|
| **NPS** | **−69** | Detractors outnumber promoters more than 10 to 1 |
| **Average CSAT** | **3.41 / 7** | Below "Neutral" — the average customer leaves unhappy |
| **Negative sentiment** | **51%** | Over half of all interactions |
| **Below SLA** | **24.5%** | 1 in 4 calls poorly handled |
| **Long calls (>20 min)** | **61%** | A slow operation |

---

## 🔍 The Investigation (start → middle → end)

The report is built as a **narrative**, one page per step. Each investigation page tests a hypothesis — and rules it out.

| Page | The question | The verdict |
|---|---|---|
| 🏠 **Overview** | How bad is it? | Critical: NPS −69, satisfaction systemically low |
| 💬 **Channel** | Is one channel to blame? | ❌ No — CSAT flat across all (3.3–3.5) |
| ❓ **Reason** | Is one reason to blame? | ❌ No — but Payment + Billing = **77%** of volume |
| 🗺️ **Geography** | Is one region/site to blame? | ❌ No — volume only tracks population |
| 📅 **Seasonality** | Is it seasonal? | ❌ No — volume flat all year (~1,090/month) |
| 🎯 **Root Cause** | So what *is* it? | ✅ A **systemic operational** problem |
| 💡 **Action** | Where do we act first? | Fix efficiency + deflect money-related demand |

**The key insight:** no single segment stood out *because the problem affects them all equally*. The uniformity **is** the finding — dissatisfaction is the operation's baseline, not a local weak spot.

---

## 📊 The Dashboard

| Cover | Overview ("The Alarm") |
|---|---|
|<img width="967" height="547" alt="Cover" src="https://github.com/user-attachments/assets/a5e883ad-04b7-4a8d-842d-d8411bd2339f" /> |<img width="972" height="552" alt="Overview" src="https://github.com/user-attachments/assets/2ef2af5e-b111-41b6-b350-bd81d1fa0f31" />|

| Root Cause | Recommendations |
|---|---|
|<img width="962" height="547" alt="Root Cause" src="https://github.com/user-attachments/assets/82717342-d9ef-485c-afce-fd056ef725b7" /> |<img width="967" height="547" alt="Action" src="https://github.com/user-attachments/assets/42137563-6916-47fc-af0c-9da7c24a6b40" />|

---

## 🛠️ Technical Highlights

This wasn't drag-and-drop. A few decisions worth calling out:

### Data model
- **Star schema** — fact table (`Call Center Data`) connected to dimensions (`Channel`, `Reason`, `CSAT`, `NPS`) plus a dedicated **Calendar** table for time intelligence.
- Dedicated **`_Measures`** table to keep all DAX organized.

### DAX measures
A correctly built **NPS** measure that handles null scores — a subtle but important detail. In DAX, `BLANK()` is treated as `0`, so a naïve `<= 6` filter silently counts unanswered surveys as detractors, distorting the score from −69 to −78. The fix filters out blanks first:

```DAX
NPS =
VAR _Valid = FILTER('Call Center Data', NOT ISBLANK('Call Center Data'[NPS Score]))
VAR _Total = COUNTROWS(_Valid)
VAR _Prom  = COUNTROWS(FILTER(_Valid, 'Call Center Data'[NPS Score] >= 9))
VAR _Det   = COUNTROWS(FILTER(_Valid, 'Call Center Data'[NPS Score] <= 6))
RETURN DIVIDE(_Prom - _Det, _Total) * 100
```

Other measures: `% Below SLA`, `% Long Calls`, `% Negative Sentiment`, `Avg CSAT`, `Avg Handle Time`, `Calls MoM %`.

### Interactivity
- **Drill-through** — right-click any state on the map to open a filtered detail page for that state.
- **Page navigation** via a custom sidebar.

### Honest visualization
- Axes anchored at zero on the seasonality charts, so the visuals don't exaggerate variation that isn't there.
- CSAT consistently labeled on its true **0–7 scale** to avoid implying a misleadingly "okay" score.

---

## 💡 Recommendations

1. **Fix operational efficiency** — 61% of calls run past 20 min and 24.5% breach SLA. Streamlining handling lifts every channel and reason at once.
2. **Deflect money-related demand** — Payment + Billing drive 77% of contacts. Stronger self-service cuts volume at its source.
3. **Monitor satisfaction with targets** — turn this one-off diagnosis into ongoing, target-driven tracking.

---

## 📁 Repository Structure

https://www.kaggle.com/datasets/mesumraza/real-world-fake-dataset-for-practice
---

## 🧰 Tools & Skills Demonstrated

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat&logo=power-bi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-512BD4?style=flat)
![Power Query](https://img.shields.io/badge/Power_Query-2C5F2D?style=flat)
![Data Modeling](https://img.shields.io/badge/Data_Modeling-185FA5?style=flat)

Data modeling (star schema) · DAX (including null-safe NPS) · Power Query · drill-through · data storytelling · honest data visualization.

---

## 📫 Let's Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ofonsecamarcelo)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:marcelo.dafonsecaoliveira@gmail.com)

---

*Dataset provided as part of a Data Visualization course exercise. The narrative, analysis, design, and recommendations are my own work.*
