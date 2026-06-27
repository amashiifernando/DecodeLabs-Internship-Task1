# Data Science Internship Project 1 
## Advanced EDA & Feature Engineering

**DecodeLabs Internship 2026 - Amashi Fernando**

## Overview
This project transforms a raw e-commerce orders dataset into a clean,
analysis-ready dataset using statistical data wrangling techniques.
The focus is on mathematical rigor- not just running code, but
applying the correct statistical method for each problem.

## Objectives
- Handle missing data using **statistical imputation**
- Detect and neutralize **outliers** using the **IQR method**
- Engineer **5 new predictive features** from existing columns

## Dataset
**Source:** `Dataset-online_store_orders.xlsx`
**Size:** 1,200 rows × 14 columns

| Column | Description |
|---|---|
| OrderID | Unique order identifier |
| Date | Order date |
| CustomerID | Unique customer identifier |
| Product | Product purchased |
| Quantity | Units purchased |
| UnitPrice | Price per unit |
| ShippingAddress | Delivery address |
| PaymentMethod | Payment type used |
| OrderStatus | Current order status |
| TrackingNumber | Shipment tracking ID |
| ItemsInCart | Number of items in cart at checkout |
| CouponCode | Coupon applied (if any) |
| ReferralSource | Marketing channel that drove the order |
| TotalPrice | Final order value |

## Methodology

### 1. Missing Value Treatment
`CouponCode` had **25.75%** missing values. Since this is a categorical
column representing "no coupon used," missing values were filled with
`"No Coupon"` — a domain-driven imputation rather than a statistical
guess.

### 2. Outlier Detection & Neutralization
Applied the **Interquartile Range (IQR)** method on `Quantity`,
`UnitPrice`, `ItemsInCart`, and `TotalPrice`:

```
Lower Bound = Q1 - 1.5 × IQR
Upper Bound = Q3 + 1.5 × IQR
```

Outliers were **capped (Winsorized)** using `numpy.clip()` rather than
deleted, preserving all 1,200 rows.

### 3. Feature Engineering
| New Feature | Formula / Logic |
|---|---|
| `RevenuePerItem` | `TotalPrice / Quantity` |
| `HasCoupon` | 1 if a coupon was used, else 0 |
| `OrderMonth` | Month extracted from `Date` |
| `OrderYear` | Year extracted from `Date` |
| `IsHighValueOrder` | 1 if `TotalPrice` > median, else 0 |

## Results
- **Final dataset:** 1,200 rows, 0 missing values
- **Target variable for future modeling:** `OrderStatus`
- Visual EDA confirms a balanced distribution across products,
  payment methods, and order statuses


## Repository Structure
```
DecodeLabs_Task1/
├── DecodeLabs_Task1.ipynb                     # Main analysis notebook
├── Dataset-online_store_orders.xlsx           # Raw input dataset
├── EDA_Visualizations.png                     # EDA visual summary
└── Cleaned_Datasets/
    ├── cleaned_dataset.csv                    # Encoded, ML-ready dataset
    └── cleaned_dataset_with_features.xlsx     # Readable dataset with new features
README.md
```

## How to Run

**Option 1 — Google Colab**
1. Open `Project1.ipynb` in [Google Colab](https://colab.research.google.com/)
2. Upload `Dataset-online_store_orders.xlsx` to the Colab session
   (or mount Google Drive if stored there)
3. Run all cells: **Runtime → Run all**

Required libraries (pre-installed on Colab, no setup needed):
```
pandas, numpy, matplotlib, seaborn, openpyxl
```

**Option 2 — VS Code**
1. Open the project folder in VS Code
2. Install the **Jupyter** extension (if not already installed)
3. Open `Project1.ipynb` and select your Python interpreter (e.g. Anaconda)
4. Make sure the dataset file is in the same folder as the notebook
5. Run all cells using the ▶️ **Run All** button at the top of the notebook

Install dependencies (if not using Anaconda's base environment):
```bash
pip install pandas numpy matplotlib seaborn openpyxl
```

## Tech Stack
- Python (Pandas, NumPy)
- Matplotlib, Seaborn
- Statistical methods: IQR, Winsorization, domain-based imputation

## Author
Amashi Fernando — DecodeLabs Data Science Internship, June 10 - July 10 2026
