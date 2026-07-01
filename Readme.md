# Human Resources Dataset: Data Cleaning & Preprocessing Pipeline

## 📌 Project Overview
Real-world datasets are rarely ready for direct analysis or machine learning modeling. This project details a programmatic end-to-end data cleaning pipeline built using Python, `pandas`, and `numpy` inside a Jupyter Notebook environment. 

The pipeline ingests a highly chaotic and messy employee spreadsheet (`messy_dataset_50.csv`) and subjects it to advanced string parsing, formatting standardizations, categorical mappings, structural imputation, and statistical validation.

---

## 🛠️ The Data Cleaning Workflow & Methodology

The project follows a systematic approach to tackle varying dimensions of data dirtiness:

### 1. Text-to-Numeric Conversion
The raw data contained unstructured text mixtures where numerical inputs should reside:
* **Age Processing:** Replaced word-written age descriptions (e.g., converting `"twenty"` to `"20"`, `"thirty"` to `"30"`) and trimmed non-numeric text suffixes like `"years"`.
* **Salary Processing:** Handled text-based numbers (e.g., rewriting `"sixty thousand"` to `"60,000"`) and removed formatting commas to cast the field securely to numeric floats.

### 2. Fixing Capitalization & Formatting Inconsistencies
* **Name Fields:** Handled trailing/leading whitespace padding using `.str.strip()` and normalized letter casing using `.str.title()`. Also used a custom structural dictionary map to catch and fix human typos (e.g., mapping `"grac"` to `"grace"`).
* **Department Field:** Adjusted scattered abbreviations to clean uppercase formats (e.g., fixing `"It"` $\rightarrow$ `"IT"`, `"Hr"` $\rightarrow$ `"HR"`).
* **Email Field:** Consolidated varying capitalization structures to enforce a unified, professional lowercase email domain notation.

### 3. Handling Hidden/Explicit Missing Values
* Identified that missing metrics were masked behind varying textual representations (`"NULL"`, `"NaN"`, `"nan"`, `"None"`, `"NAN"`, `"NaT"`).
* Programmatically re-coded all masked strings into native Python `np.nan` null identifiers to perform accurate counts using `.isna().sum()`.
* Successfully isolated and handled missing values across multiple distinct columns: `Age` (5 missing), `Email` (13 missing), `Join_Date` (19 missing), `Salary` (20 missing), and `Department` (11 missing) using dropping strategies for critical, non-imputable identifiers.

### 4. Mathematical Data Type Integrity
* Cast processed columns from generic python `object` classifications to explicit numerical types (`float` and `int`) to lock down schema memory and support math logic operations.
* Safely converted the fully cleaned `Age` column into precise discrete integers (`int64`).

### 5. Statistical Outlier Detection & Verification
* Conducted statistical auditing using the mathematical **Interquartile Range (IQR)** approach to detect rows falling outside of standard upper and lower boundary thresholds:
  $$Q1 = 25\text{th percentile}, \quad Q3 = 75\text{th percentile}$$
  $$\text{IQR} = Q3 - Q1$$
* Leveraged standard `matplotlib` box plots for visual confirmation. Proved the mathematical integrity of the dataset by confirming that the distribution mean and median values line up tightly, meaning the clean set holds zero invalid skewing outliers.

---

## 📦 Libraries & Environment
* **Language:** Python
* **Environment:** Google Colab / Jupyter Notebook
* **Core Libraries:** `pandas`, `numpy`, `matplotlib`, `datetime`

---

## 📈 Key Deliverables
1. **`3_data_cleaning.ipynb`**: The documented cleaning notebook containing the algorithmic steps and validation checks.
2. **Cleaned CSV Export**: A structured, fully typed, ready-to-analyze dataset free of formatting corruption and missing-data noise.
