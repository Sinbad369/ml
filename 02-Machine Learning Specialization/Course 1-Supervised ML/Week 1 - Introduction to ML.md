
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
![](../../00-Attachments/Pasted%20image%2020261012235133.png)

### Example 2: Horizontal Line (Zero Slope)
- **Parameters:** $w = 0, b = 360 \implies f(x) = 360$
- **Contour Position:** Located on an outer ring along the $w = 0$ axis.
- **Fit Result:** Completely flat line $\rightarrow$ **High cost $J$** (fails to capture the relationship between house size and price).
![](../../00-Attachments/Pasted%20image%2020261012235143.png)
### Example 3: Parallel Line Shift
- **Parameters:** $w = -0.15, b = 500 \implies f(x) = -0.15x + 500$
- **Contour Position:** Shifted downwards on the outer rings relative to Example 1.
- **Fit Result:** Same wrong slope as Example 1, but shifted lower $\rightarrow$ **Still high cost $J$**.
![](../../00-Attachments/Pasted%20image%2020261012235200.png)
---

## 2. Optimal Fit (Point at the Minimum Center)

### Example 4: Minimum Cost Point
- **Parameters:** $w = 0.13, b = 71 \implies f(x) = 0.13x + 71$
- **Contour Position:** Sits at the **exact center** of the innermost concentric oval.
- **Fit Result:** The line passes directly through the middle of the data points, minimizing the sum of squared errors $\rightarrow$ **Global Minimum Cost $\min J(w,b)$**.
![](../../00-Attachments/Pasted%20image%2020261012235210.png)
---
![](../../00-Attachments/Pasted%20image%2020261012235220.png)
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

![](../../00-Attachments/Pasted%20image%2020261013000528.png)


# Gradient Descent — Concept & Intuition

**Gradient Descent** is an optimization algorithm used to minimize any cost function $J(w, b)$ (or higher-dimensional functions $J(w_1, w_2, \dots, w_n, b)$)
![](../../00-Attachments/Pasted%20image%2020261017052019.png)

---

## 1. Core Algorithm Outline

1. **Initialize Parameters:** Start with initial values for parameters (e.g., set $w = 0, b = 0$).
2. **Iterative Steps:** Keep changing parameters $w$ and $b$ to decrease cost $J(w, b)$.
3. **Convergence Goal:** Repeat until reaching or settling near a **minimum**.

---

## 2. Intuition: Hill Descent Analogy

Imagine standing at a high point on a hilly landscape (a 3D cost surface):
![](../../00-Attachments/Pasted%20image%2020261017052101.png)

- **Find Steepest Slope:** Look $360^\circ$ around your current location and determine which direction leads downhill most steeply.
- **Take a Step:** Walk one small step in that direction.![](../../00-Attachments/Pasted%20image%2020261017052141.png)
- **Repeat:** From the new spot, re-evaluate the steepest downhill path and take another step.
![](../../00-Attachments/Pasted%20image%2020261017052224.png)
- **Stop at Bottom:** Continue until reaching a valley floor where no further step goes downhill.
![](../../00-Attachments/Pasted%20image%2020261017052255.png)

---

## 3. Local Minima & Sensitivity to Initial Conditions

General non-convex cost surfaces (unlike linear regression's single bowl shape) can contain multiple valleys

- **Sensitivity to Starting Point:** Starting at slightly different initial parameter values $(w, b)$ can lead down a different path to an entirely different valley floor.
- **Local Minima:** These valley bottoms are called **local minima. A non-convex function may have multiple local minima rather than one single global minimum.
![](../../00-Attachments/Pasted%20image%2020261017052331.png)
![](../../00-Attachments/Pasted%20image%2020261017052351.png)
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



![](../../00-Attachments/Pasted%20image%2020261017054043.png)


# Gradient Descent Intuition — Slope & Derivatives

The derivative term $\frac{\partial}{\partial w} J(w, b)$ determines the direction in which parameter $w$ moves (increases or decreases) to reach the minimum cost.

---

## 1. Derivative Cases & Parameter Updates

### Case 1: Positive Slope / Derivative ($> 0$)
- **Tangent Line:** Slopes **upward** to the right.
- **Update Formula:** 
  $$w = w - \alpha \cdot (\text{positive number})$$
- **Result:** **$w$ decreases** (moves left toward the minimum).

### Case 2: Negative Slope / Derivative ($< 0$)
- **Tangent Line:** Slopes **downward** to the right.
- **Update Formula:** 
  $$w = w - \alpha \cdot (\text{negative number}) = w + \alpha \cdot (\text{positive number})$$
- **Result:** **$w$ increases** (moves right toward the minimum)[.

---

## 2. In-Video Question Summary

- **Question:** When $\frac{\partial J(w,b)}{\partial w} > 0$, what happens to $w$ after one update step?
- **Correct Answer:** ** $w$ decreases.
- **Reasoning:** Since $\alpha > 0$ and the derivative is positive, subtracting their product from $w$ results in a smaller value for $w$, moving it closer to the bottom of the curve.

![](../../00-Attachments/Pasted%20image%2020261017061424.png)

![](../../00-Attachments/Pasted%20image%2020261017061432.png)


# Gradient Descent — Learning Rate ($\alpha$) & Convergence Properties

The **learning rate ($\alpha$)** scales the step size taken towards the minimum in each iteration.

---

## 1. Impact of Learning Rate Choice

| Learning Rate | Algorithm Behavior | Consequence |
| :--- | :--- | :--- |
| **Too Small** | Takes microscopic steps downhill[cite: 41]. | Gradient descent will be **extremely slow** to reach the minimum[cite: 41]. |
| **Too Large** | Overshoots the minimum and bounces across the valley[cite: 41]. | May **fail to converge** or completely **diverge** (cost $J(w)$ increases)[cite: 41]. |
![](../../00-Attachments/Pasted%20image%2020261024170450.png)
---

## 2. Fixed Point at a Local Minimum

When $w$ is already at a **local minimum**:
- The tangent line is completely flat $\implies$ **Slope / Derivative $\frac{d}{dw}J(w) = 0$**.
- **Update Calculation:**
  $$w = w - \alpha \cdot (0) \implies w = w$$
- **Result:** Once at a minimum, gradient descent leaves $w$ unchanged, keeping the algorithm at the minimum.
![](../../00-Attachments/Pasted%20image%2020261024170459.png)
---

## 3. Automatic Step-Size Decay (With Fixed $\alpha$)

Gradient descent can reach a local minimum using a **fixed learning rate $\alpha$** without manually reducing $\alpha$ over time:

1. As $w$ approaches a minimum, the slope of the curve becomes flatter $\implies$ **Derivative $\frac{d}{dw}J(w)$ becomes smaller.
2. Because the step length is $\alpha \cdot \frac{d}{dw}J(w)$, smaller derivatives produce **progressively smaller update steps**.
3. **Conclusion:** The algorithm naturally slows down and settles smoothly into the minimum.
![](../../00-Attachments/Pasted%20image%2020261024170512.png)

# Gradient Descent for Linear Regression

By substituting the explicit partial derivatives of the mean squared error cost function into the gradient descent algorithm, we get the exact update formulas used to train a linear regression model.
![](../../00-Attachments/Pasted%20image%2020261024171916.png)

---

## 1. Derivation of Partial Derivatives (Optional Calculus Details)

Given the cost function:
$$J(w,b) = \frac{1}{2m} \sum_{i=1}^{m} \left(f_{w,b}(x^{(i)}) - y^{(i)}\right)^2 = \frac{1}{2m} \sum_{i=1}^{m} \left(wx^{(i)} + b - y^{(i)}\right)^2$$

### Derivative with respect to $w$:
$$\frac{\partial}{\partial w} J(w,b) = \frac{\partial}{\partial w} \frac{1}{2m} \sum_{i=1}^{m} \left(wx^{(i)} + b - y^{(i)}\right)^2$$

Applying the chain rule brings down the exponent $2$, cancelling with the $\frac{1}{2}$ denominator:
$$\frac{\partial}{\partial w} J(w,b) = \frac{1}{m} \sum_{i=1}^{m} \left(f_{w,b}(x^{(i)}) - y^{(i)}\right) x^{(i)}$$

### Derivative with respect to $b$:
$$\frac{\partial}{\partial b} J(w,b) = \frac{1}{m} \sum_{i=1}^{m} \left(f_{w,b}(x^{(i)}) - y^{(i)}\right)$$
![](../../00-Attachments/Pasted%20image%2020261024171930.png)
---

## 2. Complete Linear Regression Gradient Descent Algorithm

$$\text{Repeat until convergence: } \{$$

$$w = w - \alpha \frac{1}{m} \sum_{i=1}^{m} \left(f_{w,b}(x^{(i)}) - y^{(i)}\right) x^{(i)}$$

$$b = b - \alpha \frac{1}{m} \sum_{i=1}^{m} \left(f_{w,b}(x^{(i)}) - y^{(i)}\right)$$

$$\}$$

> [!important] Simultaneous Updates
> Both $w$ and $b$ must be updated **simultaneously** in each iteration using temporary variables (`tmp_w`, `tmp_b`) before overwriting $w$ and $b$.

![](../../00-Attachments/Pasted%20image%2020261024171953.png)

## 3. Convexity & "Batch" Gradient Descent

### Convex Function (Single Global Minimum)
- **General Functions:** Non-linear models can have multiple local minima depending on initial values.
- **Linear Regression:** The squared error cost function always produces a **convex function** (soup-bowl shape).
- **Key Guarantee:** Linear regression has **no local minima**—only a single **global minimum**. As long as learning rate $\alpha$ is chosen properly, gradient descent is guaranteed to converge to the global minimum.
![](../../00-Attachments/Pasted%20image%2020261024172004.png)
### "Batch" Gradient Descent Definition
- This algorithm is called **"Batch" Gradient Descent** because each step evaluates **all $m$ training examples** in the summation $\sum_{i=1}^{m}$.
![](../../00-Attachments/Pasted%20image%2020261024172012.png)

# Running Gradient Descent in Action

Visualizing how gradient descent updates parameters $w$ and $b$ step-by-step to fit linear regression onto training data.

---

## 1. Visualizing Convergence Across Three Plots

As gradient descent runs through multiple iterations:

1. **Model Fit Line ($f_{w,b}(x)$ vs. Data):** 
   - Starts as a poor-fitting line (e.g., negative slope or incorrect intercept).
   - Rotates and shifts with each update until it smoothly intersects the center of the training data points.
2. **Contour Plot ($J(w, b)$ Surface):**
   - Each step draws a trajectory moving inward across concentric elliptical contour rings.
   - Cost drops rapidly at first (e.g., $77,237 \to 45,401 \to 29,109 \dots$), then decelerates as it reaches the center (minimum cost $\approx 2,311$).
3. **3D Surface Plot:**
   - Trajectory steps downward from a high point on the convex bowl directly into the global minimum valley.
![](../../00-Attachments/Pasted%20image%2020261024172627.png)

---

## 2. "Batch" Gradient Descent Definition

- **Batch Gradient Descent:** Refers to gradient descent algorithms where **every single training example** ($i = 1 \dots m$) is processed in the summation term during each step.
- **Formula Requirement:**
  $$\frac{1}{m}\sum_{i=1}^{m} \left(f_{w,b}(x^{(i)}) - y^{(i)}\right)$$
- **Comparison:** While some gradient descent variants look at small subsets (mini-batches) of data per step, "Batch" gradient descent computes exact derivatives using the entire dataset at once.
![](../../00-Attachments/Pasted%20image%2020261024172636.png)