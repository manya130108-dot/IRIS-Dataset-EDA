# Software Requirements Specification (SRS)
## Iris Dataset Exploratory Data Analysis (EDA) Notebook

**Version:** 1.0
**Date:** 21 November 2026
**Source artifact:** Welcome_To_Colab.ipynb

---

## 1. Introduction

### 1.1 Purpose
This document specifies the requirements for a Jupyter/Google Colab notebook that performs Exploratory Data Analysis (EDA) on the Iris flower dataset. It describes what the notebook must do, its inputs and outputs, and its constraints.

### 1.2 Scope
The notebook loads the Iris dataset, cleans and inspects it, computes descriptive statistics, compares species, visualizes distributions, and records written conclusions. It does not train or deploy any machine-learning model.

### 1.3 Definitions
| Term | Meaning |
|---|---|
| EDA | Exploratory Data Analysis |
| Iris dataset | 150 samples of 3 iris species (setosa, versicolor, virginica) with 4 numeric measurements |
| Colab | Google Colaboratory, a hosted Jupyter environment |

### 1.4 Intended Audience
Students, data analysts, and reviewers who need to understand or reproduce the analysis.

---

## 2. Overall Description

### 2.1 Product Perspective
A standalone, single-file notebook run in Google Colab (or any Jupyter environment). No external database or API is used; data comes from scikit-learn's built-in loader.

### 2.2 Product Functions (summary)
1. Load and label the dataset
2. Inspect structure and summary statistics
3. Check data quality (nulls, duplicates)
4. Count records per species
5. Compute NumPy statistics for selected columns
6. Group by species and compare petal means
7. Rank top records by petal length
8. Visualize species counts and petal-length distribution
9. Document key insights

### 2.3 User Characteristics
Users have basic Python and pandas knowledge and can run notebook cells sequentially.

### 2.4 Operating Environment
- Python 3.x (Colab default)
- Libraries: numpy, pandas, matplotlib, scikit-learn
- Browser with internet access (for Colab)

### 2.5 Assumptions and Dependencies
- scikit-learn's `load_iris` is available.
- Cells are executed in order, since later cells depend on the `df` DataFrame.

---

## 3. Functional Requirements

| ID | Requirement |
|---|---|
| FR-1 | The system shall load the Iris dataset as a pandas DataFrame using `load_iris(as_frame=True)`. |
| FR-2 | The system shall rename columns to `sepal_length`, `sepal_width`, `petal_length`, `petal_width`, `species`. |
| FR-3 | The system shall map numeric species codes (0, 1, 2) to `setosa`, `versicolor`, `virginica`. |
| FR-4 | The system shall display the first and last 5 rows, the shape, data types (`info()`), and `describe()` statistics. |
| FR-5 | The system shall report the count of null values per column. |
| FR-6 | The system shall report the number of duplicate rows and display them. |
| FR-7 | The system shall compute the number of records per species using `value_counts()`. |
| FR-8 | The system shall use NumPy to compute mean, median, min, and max of `sepal_length` and `petal_length`. |
| FR-9 | The system shall compute mean petal length and petal width per species and identify the species with the highest value of each. |
| FR-10 | The system shall compute mean values of all four numeric features per species. |
| FR-11 | The system shall display the top 5 records sorted by `petal_length` in descending order. |
| FR-12 | The system shall render a bar chart of record counts per species with title and axis labels. |
| FR-13 | The system shall render a histogram (15 bins) of petal length with title and axis labels. |
| FR-14 | The system shall include a written summary of findings in a markdown cell. |

---

## 4. Data Requirements

### 4.1 Input Data
| Attribute | Type | Description |
|---|---|---|
| sepal_length | float | Sepal length in cm |
| sepal_width | float | Sepal width in cm |
| petal_length | float | Petal length in cm |
| petal_width | float | Petal width in cm |
| species | categorical (string) | setosa, versicolor, virginica |

Size: 150 rows × 5 columns.

### 4.2 Output Data
- Tabular outputs (head, tail, describe, group means, top-5 table)
- Printed statistics (counts, duplicates, NumPy metrics)
- Two charts (bar chart, histogram)
- Markdown conclusions

### 4.3 Data Quality Expectations (observed)
- No missing values
- 1 duplicate row (rows 101 and 142, virginica), retained as a minor issue
- Balanced classes: 50 records per species

---

## 5. Non-Functional Requirements

| ID | Category | Requirement |
|---|---|---|
| NFR-1 | Performance | The entire notebook shall execute in under 30 seconds on the standard Colab runtime. |
| NFR-2 | Reproducibility | Results shall be deterministic; no random operations are used. |
| NFR-3 | Usability | Each analysis step shall be in its own cell, and charts shall have titles and axis labels. |
| NFR-4 | Portability | The notebook shall run in any Jupyter environment with the listed libraries. |
| NFR-5 | Maintainability | Code shall use clear variable names (`df`, `species_counts`, `petal_means`). |
| NFR-6 | Accuracy | Printed statistics shall be rounded consistently (3 decimals where applicable). |

---

## 6. External Interface Requirements

- **User interface:** Colab/Jupyter cell-based UI; outputs displayed inline.
- **Software interfaces:** numpy, pandas, matplotlib, scikit-learn APIs.
- **Hardware interfaces:** None specific; standard CPU runtime is sufficient.

---

## 7. Key Findings (Acceptance Reference)

1. The dataset is balanced (50 per species), with no nulls and one duplicate row.
2. Petal measurements discriminate species best: mean petal length is 1.462 (setosa), 4.260 (versicolor), 5.552 (virginica); sepal width is similar across species.
3. Overall mean petal length (3.758) differs from the median (4.35) because setosa forms a separate cluster (~1–2 cm); versicolor and virginica overlap somewhat, with virginica generally longer.
4. Virginica has the highest mean petal length and petal width.

---

## 8. Acceptance Criteria

- All cells run top to bottom without errors.
- Outputs match the findings in Section 7.
- Both charts render with correct titles and labels.
- Conclusions are present and consistent with the numeric outputs.

---

## 9. Future Enhancements (Out of Scope)

- Scatter plots and pair plots, and a correlation heatmap
- Box plots per species
- Handling or removing the duplicate row
- Classification model (e.g., logistic regression, KNN) with train/test evaluation
