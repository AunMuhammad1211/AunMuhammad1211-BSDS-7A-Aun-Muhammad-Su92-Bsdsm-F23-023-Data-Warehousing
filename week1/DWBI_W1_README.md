# DWBI Week 1 — Submission

**Name:** Aun Muhammad    **Roll No:** Su92-bsdsm-f23-023

## Files

| File | Task | Contents |
|---|---|---|
| `Task1_Messy_Sales_Log.ipynb` | 1 | Problems with evidence, owners, Beverages total with working |
| `Task2_OLTP_vs_OLAP.ipynb` | 2 | Classification, own scenarios, borderline case, checkout slowdown |
| `Task3_No_History_No_Single_Truth.ipynb` | 3 | Time-variant failure, three-numbers problem, non-volatile |
| `Task4_Architecture_Placement.ipynb` | 4 | Item placement, own architecture diagram, metaphor, Kimball goals, Excel source |
| `Task5_Regional_Sales_Matplotlib.ipynb` | 5 | Pre-load answers, relationships, matplotlib report with category slicing, validation checks |
| `task5_report.png` | 5 | Report page produced by the notebook |

## How to run

Place `DWBI_W1_Messy_Sales_Log.csv` and `DWBI_W1_Regional_Sales.xlsx` in the same folder as the notebooks, then run all cells (Python 3, `pandas`, `openpyxl`, `matplotlib`). Task 4 saves `task4_architecture.png` and Task 5 saves `task5_report.png`.

## Summary of answers

**Task 1.** Problems found: inconsistent branch spelling, text amounts (`Rs`, thousands separator), duplicate order, blank category, return as a negative row, an obviously wrong amount (1008 vs 1001), mixed date formats. Owners: ETL (branch, amount format, dates), source system (duplicate, blank category), business (return policy, which amount is correct). Beverages total: stepwise working in the notebook; confidence **Medium**. Preventable at entry: branch (dropdown from the Branch master) and blank category (mandatory, auto-filled from the Product master).

**Task 2.** OLTP: 1, 3, 5, 7. OLAP: 2, 4, 6, 8. The CEO's report slowed the counters because a full scan and aggregation competed with short indexed transactions for I/O, CPU, cache and locks on the same OLTP server.

**Task 3.** Ali's history breaks *time-variant*; the warehouse closes the old row and adds a new dated row (Type 2). The three sales figures differ by definition (orders placed, bookings, recognised revenue); one staging area and one owned definition fixes this. Non-volatile means loaded data is not changed by day-to-day transactions; changes are added as new records.

**Task 4.** Source: C, E. ETL/Staging: A, F. Presentation: D, H. BI Applications: B, G. HR Excel sheet accepted as a source system conditionally, with a named owner, locked template, versioning and validation.

**Task 5.** Region name comes from `Regions`, category from `Products`; both relationships are one (dimension) to many (`Sales`). The report is built with pandas and matplotlib; the category slicer is a filter on `Products.Category` with a card and chart per selection. The four validation checks are written as code. Report uses `Sales[UnitPrice]` (price at time of sale).

## Assumptions

- Task 1: a problem is reported only if the code shows it in the file. Returns are treated as reducing revenue (net), with the gross figure also shown. A wrong amount is corrected to Qty × the product's typical unit price, because the product's other rows agree on one price.
- Task 3: the reasons for the three department figures are plausible explanations, not facts about the actual systems.
- Task 4: HR holds the only copy of the staff data.
- Task 5: Power BI is replaced by pandas/matplotlib, so there is no `.pbix`. `Sales[UnitPrice]` is the sale-time price; `Products[UnitPrice]` is the current list price.
- All diagrams are my own (Task 4 drawn by code); no slide screenshots are used.
