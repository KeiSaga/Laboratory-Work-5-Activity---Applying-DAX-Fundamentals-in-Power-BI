# 📊 IS 107 — Laboratory Work 5
## Applying DAX Fundamentals in Power BI: From Measures to Contextual Analysis

> **Course:** IS 107 - Management Information Systems  
> **Activity:** Laboratory Work 5  
> **Date Submitted:** April 29, 2026  
> **Reference Tutorial:** https://www.youtube.com/watch?v=waG_JhBgUpM&t=385s

---

## 📁 Submission Contents

```
IS107_LW5_Submission/
│
├── 📄 README.md                              ← This file
│
├── 📊 Datasets/
│   ├── LW5_Orders.xlsx                       ← 700 transaction records (Fact Table)
│   ├── LW5_Customers.xlsx                    ← 5 customer records (Dimension Table)
│   └── LW5_Cookie_Types.xlsx                 ← 6 cookie product types (Lookup Table)
│
├── 📝 Report/
│   └── IS107_LW5_Final_Report.docx           ← Complete lab report (all 8 guided questions)
│
└── 💼 Power BI Files/
    └── LW5_DAX_Cookie_Sales.pbix             ← [Save your Power BI file here]
```

---

## 🎯 Objective
Execute the step-by-step implementation of DAX (Data Analysis Expressions) in Power BI using Orders, Customers, and Cookie Types datasets — creating Calculated Columns, building Measures, and generating business insights through an interactive dashboard.

---

## 📊 Dataset Summary

| File | Type | Rows | Key Column |
|------|------|------|------------|
| LW5_Orders.xlsx | Fact Table | 700 | Order ID (PK) |
| LW5_Customers.xlsx | Dimension Table | 5 | Customer ID (PK) |
| LW5_Cookie_Types.xlsx | Lookup Table | 6 | Cookie Type (PK) |

---

## ⚙️ Power BI Setup Steps

### Step 1 — Import All Three Files
```
Home → Get Data → Excel Workbook → Select each .xlsx → Load
```

### Step 2 — Set Data Types (Power Query Editor)
- `Orders[Date]` → Date type (Using Locale: English, United States)
- `Orders[Units Sold]` → Whole Number
- `Orders[Revenue]`, `Orders[Cost]` → Decimal Number
- `Cookie_Types[Revenue Per Cookie]`, `[Cost Per Cookie]` → Decimal Number

### Step 3 — Define Relationships (Model View)
```
Customers[Customer ID]       →  Orders[Customer ID]    (1 : N)
Cookie_Types[Cookie Type]    →  Orders[Product]        (1 : N)
```
> ⚠️ Relationships MUST be set before writing any RELATED() formulas

---

## 🧮 Calculated Columns

```dax
-- In Orders table (requires Cookie_Types relationship)
Revenue Per Cookie = Orders[Units Sold] * RELATED(Cookie_Types[Revenue Per Cookie])

-- In Orders table (requires Customers relationship)  
Customer Name = RELATED(Customers[Name])
```

---

## 📐 DAX Measures

```dax
Total Revenue    = SUM(Orders[Revenue])
Total Cost       = SUM(Orders[Cost])
Total Profit     = [Total Revenue] - [Total Cost]
Profit Margin %  = DIVIDE([Total Profit], [Total Revenue], 0)
Total Units Sold = SUM(Orders[Units Sold])
Total Orders     = COUNTROWS(Orders)
```

---

## 📈 Key Results (Full Dataset — No Filters)

| Measure | Value |
|---------|-------|
| **Total Revenue** | $4,690,250.50 |
| **Total Cost** | $1,973,186.13 |
| **Total Profit** | $2,717,064.38 |
| **Profit Margin %** | 57.93% |
| **Total Units Sold** | 1,125,806 |
| **Total Orders** | 700 |

### Revenue by Product
| Product | Revenue | Profit | Orders |
|---------|---------|--------|--------|
| Chocolate Chip | $1,691,197.50 | $1,014,718.50 | 202 |
| White Choc Macadamia | $974,547.00 | $527,879.63 | 109 |
| Oatmeal Raisin | $776,575.00 | $434,882.00 | 94 |
| Snickerdoodle | $587,384.00 | $367,115.00 | 93 |
| Sugar | $506,349.00 | $295,370.25 | 109 |
| Fortune Cookie | $154,198.00 | $77,099.00 | 93 |

### Revenue by Customer
| Customer | Revenue | Profit |
|----------|---------|--------|
| ACME Bites | $1,431,191.00 | $828,377.40 |
| Wholesome Foods | $1,108,643.00 | $639,674.55 |
| ABC Groceries | $903,407.00 | $523,315.43 |
| Park & Shop | $725,758.50 | $423,499.63 |
| Tres Delicious | $521,251.00 | $302,197.38 |

---

## ❓ Guided Questions Summary

| # | Topic | Key Answer |
|---|-------|-----------|
| 1 | DAX vs Excel | DAX uses column references + dynamic filter context; Excel uses fixed cell positions |
| 2 | Why DAX exists | Fills the gap between static raw data and dynamic, interactive business calculations |
| 3 | Storage difference | Calculated Columns store values per row (increases file size); Measures store only the formula |
| 4 | Filter Context | Determines which rows a Measure evaluates — changes automatically with every slicer/visual click |
| 5 | RELATED function | Traverses table relationships to access columns from related tables; requires Model View relationships |
| 6 | Formula anatomy | `MeasureName = FUNCTION(Table[Column])` — table name prevents ambiguity across multi-table models |
| 7 | Negative profit | Signals a real business loss, not a broken formula — verify by spot-checking raw data |
| 8 | Measure vs Column for % | Measure always wins: context-aware, memory-efficient, scalable, and analytically correct |

---

## 📚 References
- Tutorial: https://www.youtube.com/watch?v=waG_JhBgUpM&t=385s
- Microsoft DAX Documentation: https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-quickstart-learn-dax-basics
- DAX Guide: https://dax.guide/
- Russo, M., Ferrari, A., & Webb, C. (2021). *Artificial Intelligence with Power BI*. Packt Publishing.

---
*IS 107 — Management Information Systems | Laboratory Work 5*
