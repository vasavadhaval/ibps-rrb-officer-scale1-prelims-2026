# 10 October 2026 — Day 2: Excel and accurate MIS reporting

Today’s goal: turn ward records into a checked report and explain your checks.

## Study order — approximately four hours

- [ ] 30 minutes: repeat your introduction and yesterday’s MIS answers aloud.
- [ ] 90 minutes: complete the Excel lesson below: formulas, lookups, cleaning, PivotTable and chart.
- [ ] 45 minutes: learn the accurate-reporting and portal workflow.
- [ ] 45 minutes: complete the practical assignment before reading its answer key.
- [ ] 30 minutes: practise today’s interview questions.

If you have only two hours: spend 90 minutes on Excel and the assignment, then 30 minutes on data-quality answers. Use yesterday’s sheet or enter the dataset below.

## Excel: learn by doing

Use Excel if available. The dataset and formulas below are original fictional practice material, **not Rajpipla's actual data**.

### A. Enter this dataset

Create a sheet named `Practice`. Put the following into cells A1:H7. If pasting puts everything in one column, use Data → Text to Columns → Delimited → Comma. This is inline sample data, not an additional file you must download.

```text
Date,Ward,Households,Covered,Segregating,WasteKg,ProcessedKg,Complaints
2026-10-09,1,200,180,140,500,400,5
2026-10-09,2,300,270,200,700,560,8
2026-10-09,3,250,225,175,600,450,4
2026-10-10,1,200,190,150,520,430,3
2026-10-10,2,300,260,195,680,540,7
2026-10-10,3,250,230,180,610,480,5
```

For this exercise, `Covered` means households served that day; `Segregating` is a subset of covered households; `WasteKg` is waste collected that day; `ProcessedKg` is the portion of that day's collected waste processed. In actual reporting, define each field according to the required reporting format: processing may include earlier stock and collection is not necessarily generation.

The same ward population repeats on two dates. Summing `Households` across both dates gives household-day observations, not the city's unique households. This is a useful interview example of why reporting period and denominator matter.

### B. Basic formulas

Put `Coverage` in I1 and `SegregationAmongCovered` in J1.

```excel
=IF(C2=0,"Check denominator",D2/C2)
=IF(D2=0,"Check denominator",E2/D2)
```

Enter the first formula in I2, the second in J2 and fill down to row 7. Format valid numbers as percentages. Do not multiply by 100 as well as using Percentage format.

Useful practice formulas:

```excel
=SUM(F2:F7)
=AVERAGE(F2:F7)
=MAX(H2:H7)
=MIN(H2:H7)
=COUNT(F2:F7)
=COUNTA(B2:B7)
=COUNTIF(B2:B7,2)
=SUMIF(B2:B7,2,F2:F7)
=SUMIFS(F2:F7,B2:B7,2)
=COUNTIFS(B2:B7,2,H2:H7,">5")
```

In order: total waste 3610 kg; mean waste per row approximately 601.67 kg; maximum complaints 8; minimum 3; numeric count 6; nonempty ward count 6; two Ward 2 rows; Ward 2 waste 1380 kg; again 1380 kg; two Ward 2 rows with complaints above 5.

`COUNT` counts numbers; `COUNTA` counts nonempty cells. `SUMIF` handles one condition; `SUMIFS` can handle several. In `SUMIFS`, the sum range comes first and ranges must align. Source: [Microsoft SUMIFS documentation](https://support.microsoft.com/en-us/excel/functions/sumifs-function).

For two conditions, put an actual Excel date for 9 October 2026 in L2, then use:

```excel
=SUMIFS(F2:F7,B2:B7,2,A2:A7,L2)
```

Expected result: **700 kg**, provided column A and L2 contain matching date values. A date stored as text may not match a real Excel date. Check types when a formula unexpectedly returns zero.

### C. Lookup a ward name

Put ward IDs 1, 2, 3 in N2:N4 and fictional names Ward One, Ward Two, Ward Three in O2:O4.

```excel
=XLOOKUP(B2,$N$2:$N$4,$O$2:$O$4,"Not found")
=IFERROR(VLOOKUP(B2,$N$2:$O$4,2,FALSE),"Not found")
```

These are alternatives. XLOOKUP is unavailable in Excel 2016 and 2019; use VLOOKUP where necessary. `FALSE` requests an exact VLOOKUP match; the lookup ID must be in the first column of its lookup range. `$` locks a reference when copying a formula. Source for XLOOKUP behaviour and version availability: [Microsoft XLOOKUP documentation](https://support.microsoft.com/en-gb/excel/functions/xlookup-function).

Do not use IFERROR to hide genuine reporting failures. A zero may be a real value, while “Not found” or “Check denominator” tells you to investigate.

### D. Sort, filter, clean and validate

1. Save a raw copy before making changes.
2. Select the complete dataset before sorting, so columns stay together.
3. Filter Ward 2; verify that two rows remain.
4. Check dates and numeric types. Keep phone numbers and IDs with leading zeroes as text where appropriate.
5. Flag missing mandatory fields and unexpected values.
6. For this exercise, check `Covered <= Households`, `Segregating <= Covered`, and nonnegative quantities.
7. Review potential duplicates using the expected key. Here it is Date + Ward; real systems may need route or shift as well.
8. Do not delete repeated wards across different dates; those are legitimate records.

For untidy names, `=TRIM(K2)` removes ordinary extra spaces; it does not resolve every possible hidden Unicode character. Use standard ward IDs and authorised master lists. Drop-down validation can reduce spelling variants. Conditional formatting can highlight missing values or low coverage, but it does not replace checking source documents.

### E. Create a PivotTable and chart

Select A1:H7 → Insert → PivotTable. Put Ward in Rows, WasteKg and ProcessedKg in Values, and Date in Filters. Check that numeric fields summarise by **Sum**, not Count. Filter to 9 October and check total collected waste is 1800 kg. Refresh after changes to the underlying data.

A PivotTable summarises records without rewriting the original rows. Microsoft explains choosing Sum, Count or Average in [its PivotTable documentation](https://support.microsoft.com/en-us/excel/sum-values-in-a-pivottable).

Make a simple column chart comparing collected and processed kilograms by ward for one date. Give it a title, date and units. Do not mix kilograms and percentages on an unexplained axis.

### F. Percentages you should be able to explain

- Collection coverage: covered households / eligible households for the same period and scope.
- Segregation: use the specified denominator; in this exercise, segregating / covered households.
- Complaint closure: resolved / total received in the defined cohort. Real reports may also include previous backlog; state the basis.
- Waste processing: use the official indicator's definition. Processing / generation differs from processing / collection.

Do not average ward percentages when ward sizes differ. Calculate the combined numerator divided by the combined denominator.

## Accurate MIS reporting and portal work

### The workflow to remember

**Collect → validate → reconcile → obtain approval → submit → retain evidence → follow up.**

Original example: field staff send a ward report, a collection register and a weighing record. You check date, ward, units and completeness, compare totals, clarify differences and record corrections. Prepare a summary for review. Upload approved figures through the authorised account, then retain the acknowledgement and evidence reference.

Before submission, check:

- Are the period, ward IDs and units correct?
- Is the data complete? Are missing records marked as pending rather than zero?
- Are totals supported by registers, weighing slips or other applicable source records?
- Are repeated records legitimate or duplicate entries?
- Has a large change been explained?
- Does the upload agree with the reviewed report?
- Are photographs/documents relevant, legible and linked to the right activity?
- Has the designated officer approved where required?
- Have you saved the submission reference and final version?

### Report template you can describe in the interview

Use a title such as “Daily Sanitation MIS — 9 October 2026 — Practice Only”. Include reporting period, data source, wards covered, collection and segregation indicators, waste quantities with units, pending complaints, missing data, exceptions, action owner and deadline, and prepared/reviewed details. Keep the officer's summary short; retain the detailed evidence separately.

Illustrative action note: “Ward 2 coverage is lower than the other practice wards on 10 October. Confirm the unserved locations with field staff and record the explanation before recommending follow-up.” Do not infer a vehicle failure from a number alone.

### File and evidence management

Use names such as `2026-10-09_Ward02_Collection_Reviewed_v1.xlsx`. Maintain separate raw, working and reviewed versions. An evidence index can contain date, ward, activity, file reference, source and review status. A correction log should record the original value, revised value, reason, supporting record and reviewer.

Use approved storage and access controls. Avoid placing citizen records in public links or personal accounts. Keep only the personal information needed for the authorised purpose. Confirm a file opens after saving/exporting and test recovery through the approved backup procedure.

### If you have never used a government portal

Say: “I have not used that particular portal yet. I understand the reporting process: confirm definitions, validate the data, obtain the required approval, enter it carefully and retain the acknowledgement. I would learn the portal through its authorised guidance and supervised practice.”

Never claim portal experience that you do not have. Publicly available SBM pages can help you understand reporting; do not try to access municipal accounts without authorisation.

## A practical assignment and its answers

Complete this on Day 2 without reading the answers first. Use the practice rows for **9 October only**, rows 2–4.

Tasks:

1. Total households, covered households and segregating households.
2. Overall coverage and segregation among covered households.
3. Total collected and processed kilograms; processing share of collected waste for this exercise.
4. Ward with the most complaints and number of complaints.
5. Write a three-sentence officer summary and one follow-up action.

### Answer key

- Households: **750**; covered: **675**; segregating: **515**.
- Coverage: **675/750 = 90%**.
- Segregation among covered households: **515/675 ≈ 76.30%**.
- Collected waste: **1800 kg**; processed: **1410 kg**.
- Processing share: **1410/1800 ≈ 78.33%**. This is not a certified SBM indicator or actual city performance.
- Complaints: **17 total**; Ward 2 has the most, **8**.

Sample summary: “For the fictional 9 October dataset, 675 of 750 households were served, giving 90% coverage. Segregation among served households was 76.30%, and 1410 of 1800 collected kilograms were recorded as processed. Ward 2 had eight complaints, the highest in this sample, so complaint types and evidence should be reviewed before assigning corrective action.”

Now use 10 October only: households **750**, covered **680**, segregating **525**, collected **1810 kg**, processed **1450 kg**, complaints **15**. Coverage **90.67%**, segregation among covered **77.21%**, processing share **80.11%**.

For both dates, total collected waste is **3610 kg** and processed waste **2860 kg**. Unique households in the fictional three wards remain **750**, not 1500. Combined coverage across both days, if defined as household-day service coverage, is **1355/1500 ≈ 90.33%**. Always label the measure.

## Today's interview questions and answers

**9. Which Excel skills are useful here?** Sort/filter, totals, conditional formulas, lookups, validation, PivotTables and simple charts. Explain one that you have actually practised.

**10. SUMIF versus SUMIFS?** SUMIF sums records using one condition. SUMIFS can use multiple conditions, such as ward and date, with aligned ranges.

**11. Why use a PivotTable?** It quickly summarises many records by ward or period. I check field types, aggregation and filters and refresh it when source data changes.

**12. What is data validation?** Checks that entries match required types or rules; for example, an authorised ward list and a valid reporting date. Spreadsheet validation helps prevent errors but source verification remains necessary.

**13. How do you find duplicates?** First define the expected unique key. Then flag matching keys and inspect source records. I would not delete repeated ward names if they represent different dates or shifts.

**14. Missing data versus zero?** Zero means confirmed absence of the measured quantity. Missing means unknown or not received. I mark it pending and seek the record rather than report zero.

**15. How do you calculate overall coverage?** Total covered households divided by total eligible households for the same scope and period. Averaging ward percentages can be wrong when ward sizes differ.

**16. A formula returns zero unexpectedly. What do you check?** Criteria, selected range, date/text types, spaces, numeric types and filters. I compare a small manually checked example before trusting the whole report.

**17. Field and portal figures disagree. What do you do?** Compare scope, dates, units, source records and versions. Clarify with the responsible staff, document the correction and update only through the approved process.

## End-of-day check

- [ ] I can explain SUMIF, SUMIFS and a lookup.
- [ ] I can create and refresh a PivotTable.
- [ ] I can calculate combined coverage from total numerator and denominator.
- [ ] I distinguish missing data, zero and duplicate records.
- [ ] I can describe checks, approval and evidence before portal submission.
- [ ] I completed the assignment: 750 households, 675 covered, 90% coverage.

Excel task I can demonstrate:
Mistake I corrected:
My weakest topic:

Next: [11 October — IT and scenarios](./2026-10-11_Day_3_IT_and_Scenarios.md).

Preparation material organised from the [complete researched guide](./Interview_Preparation_09_to_13_October_2026.md). Suggested topics and questions are not an official interview syllabus.
