
# Supervised Machine Learning — Week 1: Core Concepts

## 1. Supervised vs. Unsupervised Learning

| Machine Learning Type | Definition | Key Characteristics | Common Examples |
| :--- | :--- | :--- | :--- |
| **Supervised Learning** | Learns from labeled data containing input $x$ and target $y$. | Predicts a target variable based on input features. | - House price prediction<br>- Spam detection<br>- Emotion recognition |
| **Unsupervised Learning** | Learns from unlabeled data containing only input $x$. | Discovers hidden structures or patterns automatically. | - Customer segmentation<br>- Anomaly detection<br>- Gene clustering |

---

## 2. Supervised Learning Subtypes

- **Regression:** Used when predicting a **continuous numerical value** (infinitely many possible numbers).
  - *Example:* Predicting house prices based on size, predicting temperature, or forecasting stock prices.
- **Classification:** Used when predicting a **discrete category or class** (small set of possibilities).
  - *Example:* Predicting whether an email is "Spam" or "Not Spam", or classifying emotions into discrete classes (Happy, Sad, Neutral).

---

## 3. Unsupervised Learning Subtypes

- **Clustering:** Automatically groups unlabeled data points into clusters based on shared similarities.
  - *Example:* Grouping news articles by topic without manual tagging.

---

## Practice Quiz 1 Solutions

### Question 1: Types of Supervised Learning
- **Correct Selections:** **Regression** and **Classification**
- **Reason:** Regression predicts continuous numbers, while classification predicts discrete categories.

### Question 2: Types of Unsupervised Learning
- **Correct Selection:** **Clustering**
- **Reason:** Clustering groups unlabeled data points based on features without predefined targets.


## Linear Regression Model & Terminology

### 1. Regression vs. Classification Core Distinctions
- **Supervised Learning:** The dataset provides explicit "right answers" (targets $y$ for inputs $x$).
- **Regression Model:** Predicts **continuous numbers** (infinitely many possible numeric values).
  - *Example:* Predicting house price based on size ($\text{size} = 1250 \text{ sq ft} \implies \text{price} \approx \$220\text{k}$).
- **Classification Model:** Predicts **discrete categories** (small/finite set of possible outputs).
  - *Example:* Cat vs. Dog, Disease diagnosis (Positive/Negative).

---

### 2. Standard Mathematical Notation

| Symbol | Mathematical Term | Description / Example |
| :--- | :--- | :--- |
| **$x$** | Input Variable / Feature | Size of house in $\text{ft}^2$ |
| **$y$** | Output / Target Variable | Price in $\$1000$'s |
| **$m$** | Number of Training Examples | Total number of rows in data table (e.g., $m = 47$) |
| **$(x, y)$** | Single Training Example | A specific data pair $(2104, 400)$ |
| **$(x^{(i)}, y^{(i)})$** | $i^{\text{th}}$ Training Example | The entry at row index $i$ (1st, 2nd, 3rd, ...) |

> [!warning] Critical Notation Rules
> - **$(i)$ superscript:** Refers to the **row index** in the training set (e.g., $x^{(1)} = 2104$, $x^{(2)} = 1416$).
> - **Exponent Warning:** $x^{(2)}$ is **NOT** $x^2$ (it is an index indicator, not an exponentiation).


