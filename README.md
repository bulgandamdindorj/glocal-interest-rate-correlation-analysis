# Macroeconomic Correlation Analysis — Interest Rates & Canadian Firm Financial Performance

**Organization:** GLOCAL — Canadian nonprofit (volunteer analytics project)
**Focus:** How changes in Treasury bill and bond yields flow through to the revenues, expenses, profit, and balance sheets of Canadian firms

---

## Executive Summary

| | |
|---|---|
| **Role** | Volunteer data analyst |
| **Scope** | Data cleaning · time-series merging · correlation analysis · dashboarding |
| **Data** | 2,092 cleaned financial-statement observations (Statistics Canada, 2010–2025) merged with Bank of Canada T-bill and bond yield series |
| **Key finding** | Interest expense rises with yields faster than interest revenue does — meaning higher rates squeeze firm profitability even as they earn more on cash |
| **Output** | A Python correlation model + an interactive Tableau workbook GLOCAL can use to explore any financial variable against interest rate movements |

## The Question

A market interest rate is made up of three parts: the risk-free rate (proxied by T-bill yields), an inflation premium, and a risk premium. When the risk-free rate moves, it pulls broader market rates with it. GLOCAL wanted to understand, concretely, how that shows up in the financial statements of Canadian businesses — not just in theory.

## The Data

- **Statistics Canada, Table 33-10-0224** — quarterly balance sheet and income statement ratios, all industries, Canada (6,986 raw rows → 2,092 after removing non-reported values)
- **Bank of Canada Treasury bill yields** — weekly, resampled to quarterly averages
- **Bank of Canada bond yield series** — 1–3yr, 3–5yr, 5–10yr, 10yr+, and individual 2yr–Long/RRB government bond yields

## Methodology

1. **Cleaned and prepared the data in Python (pandas, Google Colab)** — removed nulls, standardized date formats, and resampled the daily/weekly rate series to quarterly averages to match the financial statement reporting cadence.
2. **Solved a timing mismatch:** Q1 financial statements are released in April but reflect the prior quarter's results, so statement dates were shifted to align with the correct rate environment — without this, the correlations would have been measuring the wrong period against each other.
3. **Merged** the three cleaned datasets into a single quarterly panel.
4. **Computed correlations** between every financial statement line item and each yield series, then ranked all variables by strength of relationship.
5. **Visualized** the ranked correlations as a heatmap (Python/seaborn) and built a companion **Tableau workbook** so a non-technical reviewer at GLOCAL could explore any individual variable against yields over time — the heatmap shows strength, but not the trend or timing that matters for a narrative.

## Key Findings

- **Interest expense** is strongly and positively correlated with both T-bill and bond yields — firms' borrowing costs move in near lock-step with rates.
- **Interest revenue** also rises with yields, but by less than expenses do, which compresses margins as rates climb.
- **Operating profit** is *negatively* correlated with the 1-year T-bill yield — the extra interest income firms earn on cash doesn't offset the higher cost of servicing debt.
- **Derivative assets** are negatively correlated with T-bill yields, consistent with discounted-cash-flow theory: a higher risk-free rate lowers the present value of future cash flows.
- On the balance sheet, **liabilities grew faster than equity** in high-yield periods (notably 2018 and 2022), while asset growth slowed.

## Visuals

<img width="865" height="772" alt="Screenshot 2026-07-07 at 11 16 50 AM" src="https://github.com/user-attachments/assets/230a9b81-2cf4-4d43-9fa6-a227280dac5f" />

## Tools

Python (pandas, NumPy, Matplotlib, seaborn) in Google Colab · Tableau · Statistics Canada & Bank of Canada public data

## If I Did This Today

Pull the source data directly via the StatsCan and Bank of Canada APIs instead of manual CSV downloads, add CPI as a variable to more cleanly separate the "inflation premium" from the risk-free rate in the model, and publish the workbook to Tableau Public so GLOCAL has a live, shareable link rather than a static file.

---

**Bulgan Damdindorj** · Vancouver, BC · MBA, University Canada West (2026)
[LinkedIn](https://www.linkedin.com/in/bulgan-damdindorj-915451289/) · [GitHub](https://github.com/bulgandamdindorj)
