
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



# Cost Function Intuition — Simplified 1D Model

To gain visual intuition for the cost function, we simplify the model by setting **$b = 0$**, forcing the linear regression line to pass directly through the origin $(0,0)$


## 1. Model & Cost Function Comparison

| Concept | Full Model ($w, b$) | Simplified Model ($b = 0$) |
| :--- | :--- | :--- |
| **Model Function** | $f_{w,b}(x) = wx + b$[cite: 17] | $f_w(x) = wx$[cite: 17] |
| **Parameters** | $w$ (slope), $b$ (intercept)[cite: 17] | $w$ (slope only)[cite: 17] |
| **Cost Function** | $J(w,b) = \frac{1}{2m} \sum_{i=1}^{m} (f_{w,b}(x^{(i)}) - y^{(i)})^2$[cite: 17] | $J(w) = \frac{1}{2m} \sum_{i=1}^{m} (wx^{(i)} - y^{(i)})^2$[cite: 17] |
| **Optimization Goal** | $\min_{w,b} J(w,b)$[cite: 17] | $\min_w J(w)$[cite: 17] |

> [!important] Key Mental Shift
> - **$f_w(x)$ is a function of $x$:** Given a fixed parameter $w$, it plots a straight line over input features $x$[cite: 18].
> - **$J(w)$ is a function of $w$:** It maps different values of parameter $w$ to their corresponding cost/error value[cite: 18].

---

## 2. Step-by-Step Calculation Examples ($m = 3$)

Given training points: $(1, 1)$, $(2, 2)$, $(3, 3)$

### Case 1: $w = 1$ (Perfect Fit)
- **Model:** $f(x) = 1 \cdot x$
- **Predictions:** $f(1) = 1$, $f(2) = 2$, $f(3) = 3$
- **Cost Calculation:**
  $$J(1) = \frac{1}{2(3)} \left[(1-1)^2 + (2-2)^2 + (3-3)^2\right] = \frac{1}{6}(0) = 0$$
- **Plot Point:** $(w, J(w)) = (1, 0)$

### Case 2: $w = 0.5$ (Underpredicting)
- **Model:** $f(x) = 0.5x$
- **Predictions:** $f(1) = 0.5$, $f(2) = 1.0$, $f(3) = 1.5$
- **Cost Calculation:**
  $$J(0.5) = \frac{1}{2(3)} \left[(0.5-1)^2 + (1-2)^2 + (1.5-3)^2\right] = \frac{1}{6}\left[0.25 + 1 + 2.25\right] = \frac{3.5}{6} \approx 0.58$$
- **Plot Point:** $(w, J(w)) = (0.5, 0.58)$

### Case 3: $w = 0$ (Horizontal Line)
- **Model:** $f(x) = 0$
- **Predictions:** $f(1) = 0$, $f(2) = 0$, $f(3) = 0$
- **Cost Calculation:**
  $$J(0) = \frac{1}{2(3)} \left[(-1)^2 + (-2)^2 + (-3)^2\right] = \frac{1}{6}(1 + 4 + 9) = \frac{14}{6} \approx 2.33$$
- **Plot Point:** $(w, J(w)) = (0, 2.33)$

---

## 3. The Shape of $J(w)$: The Parabola

By evaluating $J(w)$ for various values of $w$ (e.g., $-0.5, 0, 0.5, 1, 1.5, 2, 2.5$), the cost function generates a **bowl-shaped curve (parabola)**.

- **Minimum Point:** The bottom of the U-shape curve occurs at $w = 1$, where $J(w) = 0$.
- **Conclusion:** Finding the optimal parameter $w$ means finding the lowest point on the $J(w)$ curve.
# Visualizing the Cost Function — 3D Surface & Contour Plots

When optimizing both parameters simultaneously ($w$ and $b$), the cost function $J(w,b)$ transitions from a 2D parabola into a 3D surface plot or a 2D contour plot.

---

## 1. 3D Surface Plot (Soup Bowl Shape)

- **Axes:** 
  - Horizontal axes represent parameters **$w$** and **$b$
  - Vertical height axis represents total cost **$J(w,b)$**
- **Geometry:** Forms a 3D "soup bowl" or "basin" shape
- **Minimum Point:** The global minimum sits at the absolute bottom/center of the bowl. Any point $(w, b)$ on this surface corresponds to a specific line $f_{w,b}(x) = wx + b$ on the scatter plot.

---

## 2. 2D Contour Plot (Contour Map)

A **contour plot** is created by slicing the 3D surface horizontally at constant cost levels $J(w,b)$ (like topographic elevation maps of mountains):

- **Ellipses / Ovals:** Each ring represents a specific value of $J(w,b)$.
- **Same-Cost Ring:** All parameter pairs $(w, b)$ lying on the **exact same contour line** produce the **exact same cost $J$.
- **Center of Ellipses:** The innermost point/center of the concentric rings represents the global **minimum cost** $\min_{w,b} J(w,b)$.

---

## 3. Key Takeaway for Optimization

| Visual Representation | Optimal Fit Location                                |
| :-------------------- | :-------------------------------------------------- |
| **Data Scatter Plot** | Line fits through the center of data points.        |
| **3D Surface Plot**   | Bottom-most point of the bowl.                      |
| **2D Contour Plot**   | Center-most point of the innermost concentric oval. |

# Visualization Examples — Contour Plots vs. Model Predictions

Each point $(w, b)$ selected on a 2D contour plot directly defines a specific linear regression line $f(x) = wx + b$ on the scatter plot:

---

## 1. Suboptimal Fits (Points Far From the Center)

### Example 1: Negative Slope, High Intercept
- **Parameters:** $w = -0.15, b = 800 \implies f(x) = -0.15x + 800$
- **Contour Position:** High up on the top-left outer ring (far from center).
- **Fit Result:** Slope goes downhill while data trends uphill $\rightarrow$ **Extremely high cost $J$** (large vertical error bars).
![[Pasted image 20261012235133.png]]

### Example 2: Horizontal Line (Zero Slope)
- **Parameters:** $w = 0, b = 360 \implies f(x) = 360$
- **Contour Position:** Located on an outer ring along the $w = 0$ axis.
- **Fit Result:** Completely flat line $\rightarrow$ **High cost $J$** (fails to capture the relationship between house size and price).
![[Pasted image 20261012235143.png]]
### Example 3: Parallel Line Shift
- **Parameters:** $w = -0.15, b = 500 \implies f(x) = -0.15x + 500$
- **Contour Position:** Shifted downwards on the outer rings relative to Example 1.
- **Fit Result:** Same wrong slope as Example 1, but shifted lower $\rightarrow$ **Still high cost $J$**.
![[Pasted image 20261012235200.png]]
---

## 2. Optimal Fit (Point at the Minimum Center)

### Example 4: Minimum Cost Point
- **Parameters:** $w = 0.13, b = 71 \implies f(x) = 0.13x + 71$
- **Contour Position:** Sits at the **exact center** of the innermost concentric oval.
- **Fit Result:** The line passes directly through the middle of the data points, minimizing the sum of squared errors $\rightarrow$ **Global Minimum Cost $\min J(w,b)$**.
![[Pasted image 20261012235210.png]]
---
![[Pasted image 20261012235220.png]]
## Key Takeaway

Moving closer to the **center of the concentric rings** on a contour plot directly reduces the vertical prediction errors (distances between actual $y^{(i)}$ points and predicted $\hat{y}^{(i)}$ line), yielding the optimal linear regression model.

## Practice Quiz: Regression Model & Cost Function

### Question 1: Model Inputs / Features
- **Question:** Which of the following are the inputs, or features, that are fed into the model and with which the model is expected to make a prediction?
- **Correct Answer:** **$x$**
- **Reasoning:** 
  - $x$ represents the input feature(s) fed into function $f(x)$
  - $w$ and $b$ are the internal model **parameters** (weights/bias).
  - $m$ is the sample count, and $(x, y)$ is a full labeled training pair.

---

### Question 2: Cost Function Intuition ($J(w, b) \approx 0$)
- **Question:** For linear regression, if you find parameters $w$ and $b$ so that $J(w, b)$ is very close to zero, what can you conclude?
- **Correct Answer:** **The selected values of the parameters $w$ and $b$ cause the algorithm to fit the training set really well.**
- **Reasoning:** 
  - Cost $J(w,b)$ measures average squared prediction error across training data. 
  - $J(w,b) \approx 0$ means predictions $\hat{y}^{(i)}$ almost perfectly match actual ground-truth targets $y^{(i)}$.

![[Pasted image 20261013000528.png]]


# Gradient Descent — Concept & Intuition

**Gradient Descent** is an optimization algorithm used to minimize any cost function $J(w, b)$ (or higher-dimensional functions $J(w_1, w_2, \dots, w_n, b)$)
![[Pasted image 20261017052019.png]]

---

## 1. Core Algorithm Outline

1. **Initialize Parameters:** Start with initial values for parameters (e.g., set $w = 0, b = 0$).
2. **Iterative Steps:** Keep changing parameters $w$ and $b$ to decrease cost $J(w, b)$.
3. **Convergence Goal:** Repeat until reaching or settling near a **minimum**.

---

## 2. Intuition: Hill Descent Analogy

Imagine standing at a high point on a hilly landscape (a 3D cost surface):
![[Pasted image 20261017052101.png]]

- **Find Steepest Slope:** Look $360^\circ$ around your current location and determine which direction leads downhill most steeply.
- **Take a Step:** Walk one small step in that direction.![[Pasted image 20261017052141.png]]
- **Repeat:** From the new spot, re-evaluate the steepest downhill path and take another step.
![[Pasted image 20261017052224.png]]
- **Stop at Bottom:** Continue until reaching a valley floor where no further step goes downhill.
![[Pasted image 20261017052255.png]]

---

## 3. Local Minima & Sensitivity to Initial Conditions

General non-convex cost surfaces (unlike linear regression's single bowl shape) can contain multiple valleys

- **Sensitivity to Starting Point:** Starting at slightly different initial parameter values $(w, b)$ can lead down a different path to an entirely different valley floor.
- **Local Minima:** These valley bottoms are called **local minima. A non-convex function may have multiple local minima rather than one single global minimum.
![[Pasted image 20261017052331.png]]
![[Pasted image 20261017052351.png]]
> [!note] Linear Regression Property
> Squared error cost functions for linear regression form a **convex bowl** (always leading to one single global minimum). General non-linear or deep learning cost functions often have multiple **local minima].

# Gradient Descent Algorithm & Update Rules

## 1. Mathematical Update Equations

To minimize cost $J(w, b)$, parameters $w$ and $b$ are updated repeatedly in small steps until convergence:

$$\text{Repeat until convergence: } \{$$

$$w = w - \alpha \frac{\partial}{\partial w} J(w, b)$$

$$b = b - \alpha \frac{\partial}{\partial b} J(w, b)$$

$$\}$$

### Notation Breakdown
- **$\alpha$ (Alpha):** **Learning rate**. Controls how large of a step is taken downhill during each update.
- **$\frac{\partial}{\partial w} J(w, b)$:** **Derivative term. Determines the slope and direction of the update.
- **$=$ (Assignment operator):** In programming code, `=` represents assigning a new value to a variable ($a = a + 1$), NOT mathematical truth equality ($a == c$).

---

## 2. Simultaneous Update Requirement

When implementing gradient descent in code, **both $w$ and $b$ MUST be updated simultaneously**.

```python
# CORRECT: Simultaneous Update
tmp_w = w - alpha * d_J_dw
tmp_b = b - alpha * d_J_db

w = tmp_w  # Update w after computing both terms
b = tmp_b  # Update b after computing both terms
```
![[Pasted image 20261017054043.png]]