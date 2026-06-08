# 💻 Laptop Dataset — Data Cleaning & Visualization Project

A complete end-to-end data science project that takes a raw laptop listings dataset, cleans it thoroughly, and extracts visual insights using Python.

---

## 📁 Project Files

| File | Description |
|------|-------------|
| `laptop.xlsx` | Raw input dataset (893 laptop listings) |
| `laptop_cleaned.xlsx` | Cleaned & processed dataset |
| `laptop_analysis.ipynb` | Main Jupyter Notebook (source) |
| `laptop_analysis_executed.ipynb` | Notebook with all outputs & charts embedded |
| `chart1_price_distribution.png` | Histogram + box plot of laptop prices |
| `chart2_brand_count_price.png` | Brand listing count vs average price |
| `chart3_price_by_ram.png` | Price distribution segmented by RAM |
| `chart4_os_share.png` | Operating system market share pie chart |
| `chart5_rating_vs_price.png` | Spec rating vs price scatter (coloured by RAM) |
| `chart6_correlation_heatmap.png` | Correlation matrix of numeric features |
| `chart7_brand_os_heatmap.png` | Avg price heatmap — top brands × OS |
| `chart8_ram_storage.png` | RAM and storage popularity bar charts |
| `chart9_display_vs_price.png` | Price by display size category |
| `chart10_dashboard.png` | 6-panel summary dashboard |
| `README.md` | This file |

---

## 📊 Dataset Overview

- **Source:** `laptop.xlsx`
- **Rows:** 893 laptop listings
- **Columns:** 18 (brand, name, price, spec_rating, processor, CPU, RAM, RAM type, ROM, ROM type, GPU, display size, resolution, OS, warranty)
- **Price range:** ₹9,999 – ₹4,50,039
- **Brands:** 30 unique brands (HP, Lenovo, Dell, Asus, Apple, Acer, MSI, Samsung, and more)

---

## 🧹 Data Cleaning Steps

### 1. Drop Redundant Columns
Removed `Unnamed: 0` and `Unnamed: 0.1` (leftover index artifacts from export).

### 2. Normalize OS Values
The `OS` column had 14 raw variants including trailing spaces, tabs (`\t`), and alternate spellings:
- `'Windows 11  OS'`, `'Windows 11 OS'` → `Windows 11`
- `'Mac OS'`, `'Mac Catalina OS'`, `'Mac High Sierra OS'`, `'Mac 10.15.3\t OS'` → `macOS`
- `'DOS OS'`, `'DOS 3.0 OS'` → `DOS`
- All cleaned into 8 canonical categories stored in `OS_clean`

### 3. Extract Numeric RAM and ROM
- `Ram` (e.g., `'8GB'`, `'16GB'`) → `Ram_GB` (int)
- `ROM` (e.g., `'512GB'`, `'1TB'`) → `ROM_GB` (int, TB × 1024)

### 4. Outlier Detection — Price
Used the IQR method (Q1 − 1.5×IQR, Q3 + 1.5×IQR) to flag price outliers.  
Outliers were **flagged** (not dropped) since high-end laptops are real market entries.

### 5. Handle Zero Warranty
6 rows had `warranty = 0` (unknown/missing). These were replaced with the **median warranty** (1 year).

---

## 📈 Visualizations

| Chart | What it shows |
|-------|--------------|
| Price Distribution | Right-skewed; majority < ₹1L, premium outliers up to ₹4.5L |
| Brand Analysis | HP & Lenovo lead in count; Apple commands highest avg price |
| Price by RAM | Clear positive relationship — 32GB/64GB configs are premium |
| OS Share | Windows 11 dominates (~60%); DOS appears in budget segment |
| Rating vs Price | Positive trend with high variance; brand premium is significant |
| Correlation Heatmap | RAM and spec_rating are top price predictors |
| Brand × OS Heatmap | Apple macOS commands 4–5× the price of DOS budget laptops |
| RAM & Storage | 8GB RAM and 512GB SSD are the market sweet spots |
| Display vs Price | Larger screens (16–19″) skew towards gaming/professional segment |
| Dashboard | 6-panel summary for quick stakeholder communication |

---

## 🔍 Key Insights

1. **Price is right-skewed** — most laptops cluster under ₹1L; the market is budget-driven.
2. **HP & Lenovo dominate** by volume; Apple has fewer models but at a major price premium.
3. **Windows 11 is the default OS** (~60%). DOS laptops occupy the sub-₹20K budget space.
4. **8GB RAM / 512GB SSD** is the most popular configuration, reflecting mainstream demand.
5. **Spec rating correlates with price**, but brand identity adds its own premium on top.
6. **Larger displays** (16–19″) target gaming and professional users at higher price points.
7. **Apple's macOS** laptops have an average price **2–3× higher** than equivalent-spec Windows laptops.

---

## 🛠 Requirements

```
pandas
numpy
matplotlib
seaborn
openpyxl
jupyter
```

Install all dependencies:
```bash
pip install pandas numpy matplotlib seaborn openpyxl jupyter
```

---

## ▶️ How to Run

```bash
# Clone or download the project folder
# Make sure laptop.xlsx is in the same directory

jupyter notebook laptop_analysis.ipynb
```

Then run all cells top to bottom (`Kernel → Restart & Run All`).

All charts will be saved as PNG files in the same directory, and `laptop_cleaned.xlsx` will be written as the cleaned output.

---

## 📌 Notes

- All cleaning decisions are documented inline in the notebook with rationale.
- No rows were deleted — outliers are flagged with a boolean column (`price_outlier`).
- The cleaned file retains all original columns plus derived columns: `OS_clean`, `Ram_GB`, `ROM_GB`, `price_outlier`, `display_bin`.
