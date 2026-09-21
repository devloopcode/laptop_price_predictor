# 💻 Laptop Price Predictor

A machine learning project that performs **exploratory data analysis (EDA)** and **price prediction** on a dataset of 1,303 laptops. The project cleans and analyses laptop specifications to uncover insights and build a model for predicting laptop prices.

---

## 📂 Project Structure

```
laptop_price_predictor/
├── laptop_price_predicted.ipynb   # Main Jupyter Notebook (EDA + modelling)
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
| `Price`            | Price (target variable)                          |

**Companies represented:** Apple, HP, Acer, Asus, Dell, Lenovo, MSI, Microsoft, Razer, Samsung, and more.

---

## 🔍 Notebook Overview

The notebook (`laptop_price_predicted.ipynb`) covers:

1. **Data Loading & Inspection**
   - Load CSV with `pandas`
   - Inspect shape, columns, and data types
   - Check for null values and duplicate rows (29 duplicates found)

2. **Data Cleaning**
   - Drop redundant index column (`Unnamed: 0`)
   - Identify numerical vs categorical columns

3. **Feature Engineering**
   - Strip units and convert `Ram` from string (e.g. `"8GB"`) to integer
   - Strip units and convert `Weight` from string (e.g. `"1.37kg"`) to float

4. **Exploratory Data Analysis (EDA)**
   - Explore unique values across all features
   - Price distribution histogram (`sns.displot`)
   - Count plots for `Company`, `TypeName`, `Ram`, and `OpSys`
   - Average price per company bar chart
   - Laptop type distribution count plot

5. **Price Prediction** *(planned — not yet started)*
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
- RAM values range from **2GB to 64GB**.
- Prices span a wide range, reflecting the variety of budget to premium laptops.
- Brands covered include **19 different manufacturers**.
- **6 laptop types** are present: Ultrabook, Notebook, Netbook, Gaming, 2-in-1 Convertible, and Workstation.

---

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).