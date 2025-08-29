# 📧 Spam Email Classification

This project implements an automatic email spam classification system using machine learning techniques and data balancing methods.

## 📊 Dataset

**Source:** [Spam Email Classification Dataset - Kaggle](https://www.kaggle.com/datasets/somesh24/spambase/data)

The dataset contains information about emails labeled as spam or not spam, with the following details:

* **Total instances:** 4,601 emails
* **Class distribution:**

  * Spam (1): 1,813 emails (39.40%)
  * Not spam (0): 2,788 emails (60.60%)

### 📋 Attribute Description

The dataset includes 57 attributes plus the target variable:

* **48 continuous attributes \[0,100]:** Percentage frequency of specific words in the email

  * `word_freq_WORD = 100 * (number of times WORD appears) / total words`

* **6 continuous attributes \[0,100]:** Percentage frequency of specific characters

  * `char_freq_CHAR = 100 * (number of CHAR occurrences) / total characters`

* **3 attributes for capital letter sequences:**

  * `capital_run_length_average`: Average length of uninterrupted capital letter sequences
  * `capital_run_length_longest`: Length of the longest uninterrupted sequence of capital letters
  * `capital_run_length_total`: Total number of capital letters in the email

* **Target variable:** `spam` (0 = not spam, 1 = spam)

---

## 🔧 Methodology

### 🛠️ Data Preprocessing

The preprocessing pipeline includes:

**For numerical variables:**

* 🔢 Missing value imputation (mean)
* 🔲 Square root transformation
* 📏 Standardization (StandardScaler)

**For categorical variables:**

* 🔡 Missing value imputation (mode)
* 🏷️ One-hot encoding

### 🤖 Models Evaluated

Multiple classification algorithms were tested:

| Model                                  | Accuracy   | Std. Deviation |
| -------------------------------------- | ---------- | -------------- |
| 🌳 **Random Forest**                   | **98.75%** | **0.50%**      |
| 🚀 **Gradient Boosting**               | **98.51%** | **0.50%**      |
| 🎯 **SVC**                             | **97.47%** | **0.67%**      |
| 📈 **Logistic Regression**             | **97.09%** | **0.67%**      |
| 📊 **Linear Discriminant Analysis**    | **95.14%** | **1.13%**      |
| 📉 **Quadratic Discriminant Analysis** | **95.03%** | **1.03%**      |
| 🧠 **Gaussian Naive Bayes**            | **93.10%** | **1.75%**      |

### ⚖️ Data Balancing Techniques

Several resampling techniques were explored:

#### 📉 Undersampling

* **TomekLinks:** 98.7% (0.5%)
* **Edited Nearest Neighbours (ENN):** 98.7% (0.5%)
* **Repeated ENN:** 98.6% (0.5%)
* **One-Sided Selection:** 98.7% (0.5%)
* **Neighbourhood Cleaning Rule:** 98.7% (0.5%)

#### 📈 Oversampling

* **Random OverSampler:** 98.8% (0.5%)
* **SMOTE:** 98.7% (0.6%)
* **BorderlineSMOTE:** 98.8% (0.5%)
* **ADASYN:** 98.8% (0.5%)

---

## 🏆 Final Model

### ⚙️ Optimal Configuration

**Algorithm:** 🌳 Calibrated Random Forest

* Estimators: 1,000 trees
* Class balancing: `class_weight="balanced"`
* Probability calibration: Isotonic Regression (CV=3)
* Balancing technique: BorderlineSMOTE

### 📊 Performance Metrics

| Metric                   | Value     |
| ------------------------ | --------- |
| 🎯 **ROC-AUC**           | **0.982** |
| 📐 **Average Precision** | **0.978** |
| 📏 **PR-AUC**            | **0.979** |

---

## 💻 Technologies Used

* 🐍 **Python 3.8+**
* 🤖 **scikit-learn**: ML models and preprocessing
* ⚖️ **imbalanced-learn**: Balancing techniques
* 🐼 **pandas**: Data manipulation
* 🔢 **numpy**: Numerical operations

---

## 📈 Conclusions

* 🌳 **Random Forest** was the most effective algorithm for this task.
* 📈 **Oversampling techniques** (especially BorderlineSMOTE) significantly improved performance.
* 🎯 **Probability calibration** provided more reliable probability estimates.
* 🏆 The final model achieved exceptional performance with **ROC-AUC of 0.982**.
