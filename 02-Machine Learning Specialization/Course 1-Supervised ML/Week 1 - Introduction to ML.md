
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


## Supervised Learning Model Pipeline & Representation

### 1. Training Workflow
1. **Training Set:** Consists of **features** ($x$) and **targets** ($y$).
2. **Learning Algorithm:** Processes training data to produce a mapping function $f$ (the **model**).
3. **Inference/Prediction:** Feature $x$ goes into model $f$, producing prediction $\hat{y}$ (**y-hat**, estimated value of $y$).

$$\text{Feature } (x) \longrightarrow \text{Model } (f) \longrightarrow \text{Prediction } (\hat{y})$$

---

### 2. Linear Regression Formula (Single Variable)

The hypothesis/model function $f_{w,b}(x)$ is represented as:

$$f_{w,b}(x) = wx + b$$

> [!note] Simplified Notation
> $f_{w,b}(x)$ can also be written simply as $f(x)$.

- **$w, b$:** Parameters (weights/bias) adjusted by the learning algorithm.
- **$x$:** Input feature (e.g., house size).
- **$\hat{y}$:** Predicted output (e.g., estimated price).

---

### 3. Key Terminology

- **$\hat{y}$ ("y-hat"):** The **estimated/predicted** value of $y$, distinguishing model output from actual ground-truth labels $y$.
- **Univariate Linear Regression:** Linear regression with **one variable/feature** $x$.

# Optional Lab: Model Representation

## 1. Mathematical Notation Reference

| General Notation | Description | Python Variable |
| :--- | :--- | :--- |
| $x$ | Scalar input feature (e.g., Size in $1000\text{ sqft}$) | `x_train` |
| $y$ | Scalar target output (e.g., Price in $\$1000\text{s}$) | `y_train` |
| $x^{(i)}, y^{(i)}$ | $i^{\text{th}}$ Training Example tuple | `x_i, y_i` |
| $m$ | Total number of training examples | `m` |
| $w$ | Model parameter: Weight (Slope) | `w` |
| $b$ | Model parameter: Bias (Y-intercept) | `b` |
| $f_{w,b}(x^{(i)})$ | Model output/prediction evaluated at $x^{(i)}$ | `f_wb` |

---

## 2. Dataset Setup & Exploration

``
import numpy as np
import matplotlib.pyplot as plt

# 1. Define Training Set (House Size vs. Price)
x_train = np.array([1.0, 2.0])      # Size in 1000 sqft
y_train = np.array([300.0, 500.0])  # Price in $1000s

# 2. Get Number of Training Examples (m)
m = x_train.shape[0]  # Or len(x_train)
print(f"Number of training examples is: {m}")  # Outputs: 2

# 3. Access Specific Training Example (Zero-Indexed)
i = 0
x_i, y_i = x_train[i], y_train[i]
print(f"(x^({i}), y^({i})) = ({x_i}, {y_i})")  # Outputs: (1.0, 300.0)



# Linear Regression — Model Parameters & Cost Function

## 1. Model Parameters ($w$ and $b$)

In the model function $f_{w,b}(x) = wx + b$:
- **$w$ (Weight / Coefficient / Slope):** Controls the steepness or angle of the line.
- **$b$ (Bias / Y-intercept):** Controls where the line crosses the y-axis ($x = 0$).

### Visualizing Parameter Effects
1. **$w = 0, b = 1.5$:** Horizontal line at $y = 1.5$ (constant prediction regardless of $x$).
2. **$w = 0.5, b = 0$:** Passes through the origin $(0,0)$ with a slope of $0.5$ (rise of $0.5$ for every $1$ unit run).
3. **$w = 0.5, b = 1$:** Shifted vertically up by $1$ unit, crossing the y-axis at $(0,1)$ with a slope of $0.5$.

---

## 2. The Cost Function (Squared Error)

The **Cost Function** measures how well a choice of $w$ and $b$ fits the training dataset by calculating the total error between predictions $\hat{y}^{(i)}$ and actual targets $y^{(i)}$.

### Error Definition
$$\text{Error for example } i = \hat{y}^{(i)} - y^{(i)} = f_{w,b}(x^{(i)}) - y^{(i)}$$

### Mathematical Formula: $J(w,b)$
$$J(w,b) = \frac{1}{2m} \sum_{i=1}^{m} \left( \hat{y}^{(i)} - y^{(i)} \right)^2$$

Substituting $\hat{y}^{(i)} = f_{w,b}(x^{(i)})$:

$$J(w,b) = \frac{1}{2m} \sum_{i=1}^{m} \left( f_{w,b}(x^{(i)}) - y^{(i)} \right)^2$$

> [!note] Formula Breakdown
> - **$m$:** Total number of training examples.
> - **$\frac{1}{m}$:** Computes the average squared error across all $m$ examples.
> - **$\frac{1}{2}$:** A mathematical convenience that cancels out the power of $2$ when taking derivatives during Gradient Descent.

---

## 3. Optimization Goal

The objective of linear regression is to find parameter values $w$ and $b$ that **minimize** $J(w,b)$:

$$\min_{w,b} J(w,b)$$

This ensures predictions $\hat{y}^{(i)}$ are as close as possible to the actual target values $y^{(i)}$ across all training examples $(x^{(i)}, y^{(i)})$.






