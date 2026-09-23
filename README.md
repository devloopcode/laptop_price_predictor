# 💻 Laptop Price Predictor

A machine learning project that performs **exploratory data analysis (EDA)**, **feature engineering**, and **price prediction** on a dataset of 1,303 laptops. The project cleans and transforms laptop specifications to uncover insights and prepare features for predicting laptop prices.

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
- **Feature Dropping** — Remove low-correlation or redundant features (`TouchScreen`, `X_res`, `Y_res`, `Inches`, `Cpu`) after deriving new features

### 4. Exploratory Data Analysis (EDA)
- **Price distribution** — histogram via `sns.displot`
- **Count plots** for `Company`, `TypeName`, `Ram`, `OpSys`, `TouchScreen`, `IPS`, and `CPU_name`
- **Average price per company** — bar chart (`sns.barplot`)
- **Laptop type distribution** — count plot
- **Average price per laptop type** — bar chart
- **Screen size vs price** — scatter plot (`sns.scatterplot`)
- **TouchScreen vs price** — bar chart
- **IPS panel vs price** — bar chart
- **CPU category vs price** — bar chart
- **Screen resolution distribution** — value counts
- **Correlation heatmap** — `sns.heatmap` of all numeric features
- **Feature-target correlations** — correlation of each feature with `Price` (computed before and after PPI engineering to validate improvement)

### 5. Price Prediction *(in progress)*
- Build and evaluate regression models

---

## 🛠️ Tech Stack

- **Python 3.13**
- **pandas** — data manipulation
- **NumPy** — numerical operations
- **Matplotlib** — data visualisation
- **Seaborn** — statistical plots
- **Jupyter Notebook** — interactive development environment (via Anaconda/conda)

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
- **19 manufacturers** are represented, with Apple, Dell, and Razer commanding the highest average prices.
- **6 laptop types** are present: Ultrabook, Notebook, Netbook, Gaming, 2-in-1 Convertible, and Workstation.
- Screen sizes range from **10.1″ to 18.4″** across 18 distinct values.
- **9 operating systems** are represented, including Windows 10, macOS, Linux, Chrome OS, and others.
- Screen resolutions show a wide variety, with **40 distinct resolution/panel combinations**.
- **Touchscreen laptops** have a noticeably higher average price than non-touchscreen laptops.
- **IPS panel** laptops also tend to be priced higher.
- The engineered **PPI** feature shows a stronger correlation with price than raw resolution or screen size alone.
- After CPU categorisation, **Intel Core i7** laptops have the highest average price, followed by i5 and i3.

---

## 🗺️ Roadmap

- [x] Data loading & inspection
- [x] Data cleaning
- [x] Feature engineering (Ram, Weight, TouchScreen, IPS, PPI, CPU)
- [x] Exploratory data analysis with visualisations
- [x] Correlation analysis & feature selection
- [ ] Build regression models (Linear Regression, Random Forest, etc.)
- [ ] Model evaluation & comparison (R², MAE, RMSE)
- [ ] Hyperparameter tuning
- [ ] Export trained model with `pickle` / `joblib`

---

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.

---

## 📄 Licence

This project is open-source and available under the [MIT Licence](https://opensource.org/licenses/MIT).
