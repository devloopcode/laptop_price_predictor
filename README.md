# 💻 Laptop Price Predictor

A machine learning project that performs **exploratory data analysis (EDA)** and **feature engineering** on a dataset of 1,303 laptops. The project cleans and transforms raw laptop specifications into meaningful numerical features, uncovers pricing insights through visualisations, and prepares a modelling-ready dataset for price prediction.

---

## 📂 Project Structure

```
laptop_price_predictor/
├── laptop_price_predicted.ipynb   # Main Jupyter Notebook (EDA + feature engineering + modelling)
├── laptop_data.csv                # Dataset containing laptop specifications and prices
└── README.md
```

---

## 📊 Dataset

The dataset (`laptop_data.csv`) contains **1,303 laptop records** with the following features:

| Column             | Description                                      |
|--------------------|--------------------------------------------------|
| `Company`          | Laptop manufacturer (e.g. Apple, HP, Dell)       |
| `TypeName`         | Laptop type (e.g. Ultrabook, Notebook, Gaming)   |
| `Inches`           | Screen size in inches                            |
| `ScreenResolution` | Display resolution and panel type                |
| `Cpu`              | Processor details (brand, model, speed)          |
| `Ram`              | RAM size (e.g. 8GB, 16GB)                        |
| `Memory`           | Storage type and capacity (SSD/HDD/Hybrid)       |
| `Gpu`              | Graphics card details                            |
| `OpSys`            | Operating system                                 |
| `Weight`           | Laptop weight in kg                              |
| `Price`            | Price in INR (target variable)                   |

**Companies represented:** Apple, HP, Acer, Asus, Dell, Lenovo, Chuwi, MSI, Microsoft, Toshiba, Huawei, Xiaomi, Vero, Razer, Mediacom, Samsung, Google, Fujitsu, and LG.

---

## 🔍 Notebook Overview

The notebook (`laptop_price_predicted.ipynb`) covers:

### 1. Data Loading & Inspection
- Load CSV with `pandas`
- Inspect shape (`1303 × 12`), columns, and data types
- Check for null values (none found) and duplicate rows (29 duplicates found)
- Detailed `df.info()` summary

### 2. Data Cleaning
- Drop redundant index column (`Unnamed: 0`) → shape becomes `1303 × 11`
- Identify numerical vs categorical columns

### 3. Feature Engineering
- **Ram & Weight** — Strip units and convert `Ram` from string (e.g. `"8GB"`) to `int32` and `Weight` (e.g. `"1.37kg"`) to `float32`
- **TouchScreen** — Extract binary feature from `ScreenResolution` (1 if touchscreen, 0 otherwise)
- **IPS Panel** — Extract binary feature from `ScreenResolution` (1 if IPS panel, 0 otherwise)
- **Screen Resolution** — Parse `ScreenResolution` into separate `X_res` and `Y_res` integer columns
- **PPI (Pixels Per Inch)** — Compute pixel density: `√(X_res² + Y_res²) / Inches`
- **CPU Categorisation** — Extract and simplify CPU names into categories: `Intel Core i3`, `Intel Core i5`, `Intel Core i7`, `Other Intel Processor`, and `AMD Processor`
- **Memory / Storage** — Parse the composite `Memory` column (e.g. `"256GB SSD + 1TB HDD"`) into two layers:
  - Split on `+` to separate primary and secondary storage
  - Create binary indicator columns for each storage type (`HDD`, `SSD`, `Hybrid`, `Flash Storage`) per layer
  - Extract numeric capacity values (converting `TB` → `1000`) into `first` and `Second` integer columns
  - Combine layers into final aggregate columns: `HDD`, `SSD`, `Hybrid`, `Flash_Storage` (total capacity per type)
  - Drop all intermediate columns (`first`, `Second`, `Layer_*`, `ScreenResolution`)
  - Drop `Hybrid` and `Flash_Storage` due to near-zero correlation with price
- **GPU Brand** — Extract GPU manufacturer brand (`Intel`, `Nvidia`, `AMD`) from the full `Gpu` description; remove the single `ARM` GPU entry as an outlier; drop the original `Gpu` column
- **OS Categorisation** — Simplify the 9 distinct operating systems into 3 categories:
  - `Windows` (Windows 10, Windows 7, Windows 10 S)
  - `Mac` (macOS, Mac OS X)
  - `Other` (Linux, Chrome OS, No OS, Android)
- **Feature Dropping** — Remove low-correlation or redundant features (`TouchScreen`, `X_res`, `Y_res`, `Inches`, `Cpu`, `Gpu`, `Hybrid`, `Flash_Storage`) after deriving new features

### 4. Exploratory Data Analysis (EDA)
- **Price distribution** — histogram via `sns.displot`; log-transformed price distribution to check skewness
- **Count plots** for `Company`, `TypeName`, `Ram`, `OpSys`, `TouchScreen`, `IPS`, `CPU_name`, and `Gpu_brand`
- **Average price per company** — bar chart (`sns.barplot`)
- **Laptop type distribution** — count plot
- **Average price per laptop type** — bar chart
- **Screen size vs price** — scatter plot (`sns.scatterplot`)
- **TouchScreen vs price** — bar chart
- **IPS panel vs price** — bar chart
- **CPU category vs price** — bar chart
- **RAM distribution & average price per RAM tier** — count plot + bar chart
- **Storage type distribution** — value counts of `Memory` column
- **Screen resolution distribution** — value counts
- **GPU brand distribution & median price per GPU brand** — count plot + bar chart
- **OS category distribution & average price per OS** — count plot + bar chart (Mac: ₹83,340 > Windows: ₹63,388 > Other: ₹31,497)
- **Weight distribution & weight vs price** — histogram with KDE + scatter plot
- **Correlation heatmap** — `sns.heatmap` of all numeric features
- **Feature-target correlations** — correlation of each feature with `Price` (computed before and after PPI engineering to validate improvement)

### 5. Final Engineered Feature Set

After all transformations, the dataset contains **13 columns**:

| Feature          | Type        | Correlation with Price |
|------------------|-------------|------------------------|
| `Company`        | Categorical | —                      |
| `TypeName`       | Categorical | —                      |
| `Ram`            | int32       | **0.743**              |
| `OpSys`          | Categorical | —                      |
| `Weight`         | float32     | 0.210                  |
| `Price`          | float64     | 1.000 *(target)*       |
| `IPS`            | int64       | 0.253                  |
| `PPI`            | float64     | **0.475**              |
| `CPU_name`       | Categorical | —                      |
| `HDD`            | int64       | −0.097                 |
| `SSD`            | int64       | **0.671**              |
| `Gpu_brand`      | Categorical | —                      |

### 6. Price Prediction *(next step)*
- Build and evaluate regression models

---

## 🛠️ Tech Stack

- **Python 3.13**
- **pandas** — data manipulation & cleaning
- **NumPy** — numerical operations
- **Matplotlib** — data visualisation
- **Seaborn** — statistical plots & heatmaps
- **Jupyter Notebook** — interactive development environment (via Anaconda/conda)
- **scikit-learn** *(planned)* — model training & evaluation

---

## 🚀 Getting Started

### Prerequisites

Make sure you have Python 3.x and either `pip` or `conda` installed.

### 1. Clone the repository

```bash
git clone https://github.com/your-username/laptop_price_predictor.git
cd laptop_price_predictor
```

### 2. Install dependencies

Using pip:

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

Or using conda:

```bash
conda install pandas numpy matplotlib seaborn jupyter
```

### 3. Launch the notebook

```bash
jupyter notebook laptop_price_predicted.ipynb
```

---

## 📈 Key Findings (EDA)

- The dataset has **no missing values** across all 11 columns.
- **29 duplicate rows** were identified.
- RAM values range from **2 GB to 64 GB**, with 9 distinct values.
- Prices span a wide range, reflecting the variety of budget to premium laptops.
- The price distribution is **right-skewed**; a log transformation produces a more normal distribution.
- **19 manufacturers** are represented, with Apple, Dell, and Razer commanding the highest average prices.
- **6 laptop types** are present: Ultrabook, Notebook, Netbook, Gaming, 2-in-1 Convertible, and Workstation.
- Screen sizes range from **10.1″ to 18.4″** across 18 distinct values.
- **Touchscreen laptops** have a noticeably higher average price than non-touchscreen laptops.
- **IPS panel** laptops also tend to be priced higher.
- The engineered **PPI** feature shows a stronger correlation with price than raw resolution or screen size alone.
- After CPU categorisation, **Intel Core i7** laptops have the highest average price, followed by i5 and i3.
- **GPU brands** show clear price differentiation: Nvidia GPUs command the highest median price, followed by Intel and AMD.
- **Mac** laptops average ₹83,340, significantly above **Windows** (₹63,388) and **Other** OS (₹31,497).
- A single **ARM** GPU entry was removed as an outlier.
- **Hybrid** and **Flash Storage** columns were dropped due to negligible correlation with price (0.008 and ~0 respectively).

### Top Feature Correlations with Price (post-engineering)

| Feature | Correlation |
|---------|-------------|
| Ram     | **0.743**   |
| SSD     | **0.671**   |
| PPI     | **0.475**   |
| IPS     | 0.253       |
| Weight  | 0.210       |
| HDD     | −0.097      |

---

## 🗺️ Roadmap

- [x] Data loading & inspection
- [x] Data cleaning
- [x] Feature engineering (Ram, Weight, TouchScreen, IPS, PPI, CPU, Memory/Storage, GPU brand, OS category)
- [x] Exploratory data analysis with visualisations
- [x] Correlation analysis & feature selection
- [x] Feature dropping (Hybrid, Flash_Storage, TouchScreen, X_res, Y_res, Inches, Cpu, Gpu)
- [ ] Build regression models (Linear Regression, Random Forest, etc.)
- [ ] Model evaluation & comparison (R², MAE, RMSE)
- [ ] Hyperparameter tuning
- [ ] Export trained model with `pickle` / `joblib`

---

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.
