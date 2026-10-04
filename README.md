# Veda-Technology-Task-27
# Salesperson Performance Analysis (Excel)

**Task 27 | Veda Technology Internship | Data Analytics Track (Level 2, Day 27)**
---

## Problem Statement

| | |
|---|---|
| **Description** | Compare salespeople using sales, profit, growth, and average order value. |
| **Objective** | Evaluate performance fairly. |
| **Deliverables** | Ranking, Dashboard, Recommendations |
| **Hints followed** | Use multiple KPIs, consider territory differences |

Ranking people by total sales alone is unfair: a rep in a large or high-margin territory will always look better than a rep in a tougher one. This project fixes that with a weighted **Fair Score** that also compares each rep against their own region.

---

## Dataset

A **synthetic Superstore-style dataset** with the same columns as the well-known *Sample - Superstore* data, plus an added **Salesperson** column (the original dataset has no salesperson field).

| Item | Value |
|---|---|
| Line items | 5,201 |
| Orders | 3,047 |
| Period | 2014 to 2017 |
| Regions | West, East, Central, South |
| Salespeople | 8 (2 per region) |
| Columns | 22 (Order ID, Order Date, Region, Salesperson, Category, Sub-Category, Sales, Quantity, Discount, Profit, and more) |

> **Note:** The data is generated for practice. The numbers are not real company results.

---

## Approach

**1. Core KPIs per salesperson** (all with `SUMIFS`, `COUNTIFS`, `AVERAGEIFS`)
- Total Sales, Total Profit, Profit Margin
- Orders and Average Order Value (each order counted once using an *Order Flag* helper column)
- Average Discount
- YoY Growth (2017 vs 2016) and 3-year CAGR (2014 to 2017)

**2. Territory adjustment**
- *Share of Region Sales*: rep sales divided by total sales of the region
- *Margin vs Region*: rep margin minus the region margin

**3. Fair Score (0 to 100)**

Each KPI is scaled to 0 to 1 with min-max normalisation, then multiplied by its weight:

| KPI | Weight |
|---|---|
| Total Sales | 15% |
| Total Profit | 20% |
| Profit Margin | 15% |
| Growth (CAGR 14-17) | 15% |
| Avg Order Value | 10% |
| Share of Region Sales | 10% |
| Margin vs Region | 15% |

The weights are editable (blue cells), and the score, rank, tier and dashboard update automatically.

**4. Tiering:** Rank 1-2 = Star Performer, 3-5 = Solid Contributor, 6-8 = Needs Support.

**5. Supporting analysis:** region, category, sub-category, discount level and yearly trend.

---

## Key Results

| Rank | Salesperson | Region | Fair Score | Sales-only Rank | Tier |
|---|---|---|---|---|---|
| 1 | Divya Rao | South | 75.3 | 4 | Star Performer |
| 2 | Anita Verma | West | 75.1 | 1 | Star Performer |
| 3 | Rohan Mehta | West | 67.2 | 2 | Solid Contributor |
| 4 | Neha Gupta | Central | 51.8 | 5 | Solid Contributor |
| 5 | Priya Nair | East | 45.7 | 3 | Solid Contributor |
| 6 | Karan Malhotra | East | 37.4 | 8 | Needs Support |
| 7 | Vikram Singh | South | 29.7 | 7 | Needs Support |
| 8 | Sameer Khan | Central | 22.6 | 6 | Needs Support |

**Company totals:** Sales $6.56M, Profit $461K, Margin 7.0%, 3,047 orders, Avg Order Value $2,152.

The top two scores are very close (75.3 vs 75.1), so they are best treated as joint leaders.

---

## Key Insights

- **Fair ranking changes the story.** Divya Rao is only #4 on sales but #1 on the Fair Score because of fast growth (25.1% CAGR) and the highest average order value ($2,814).
- **Discounts destroy profit.** Items with 30% or more discount lost **$192,840** across 1,315 line items, while items with 20% or less discount earned **$654,316**.
- **Territory matters.** West margin is 9.9% versus only 3.7% in Central.
- **Loss-making sub-categories:** Tables, Machines, Bookcases and Supplies.
- **Profitability is slipping.** Sales grew from $1.49M (2014) to $1.72M (2017) but margin fell from 7.7% to 6.0%.
- **Sameer Khan** has strong growth but almost zero profit ($460 on $604K sales), which points to heavy discounting.

---

## Recommendations

1. **Reward on the Fair Score,** not on sales alone, and use the top performers as peer mentors.
2. **Cap discounts at 20%.** Require manager approval above 20% and stop deals above 30%.
3. **Fix loss-making products** (Tables, Machines, Bookcases, Supplies) through repricing or lower discounts.
4. **Coach the Central territory** and set region-specific margin targets.
5. **Invest in high-growth talent** such as Divya Rao.
6. **Investigate declining sales** for Anita Verma and Priya Nair in 2017.
7. **Raise order value** for Karan Malhotra through bundling and upselling.
8. **Reduce category concentration:** Technology drives about 72% of sales.
9. **Track margin monthly** alongside sales in the review process.

---


### Workbook sheets

| Sheet | Purpose |
|---|---|
| `Dashboard` | KPI cards, 6 charts and key insights |
| `Ranking` | Auto-sorted final ranking with tiers |
| `KPI Analysis` | Core KPIs, editable weights, normalised scores, Fair Score |
| `Region & Product` | Region, category, sub-category, discount and yearly analysis |
| `Data` | Source data plus `Year` and `Order Flag` helper columns |

---
