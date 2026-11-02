
# Classification & Motivations

## Overview
Up to this point (Week 1 & 2), we have focused on **Regression**, where the model predicts a continuous number (like the price of a house). 
Now, we are moving to **Classification**, where the model predicts a specific category or class.

---

## 1. What is Classification?

In classification, the target variable $y$ can only take on a small, discrete set of values.

**Real-world Examples:**
![](../../00-Attachments/Pasted%20image%2020261102095604.png)
Because there are only **two** possible outcomes, this is specifically called **Binary Classification**.
*   `class` = category
*   The output $y$ can only be one of two values.
![](../../00-Attachments/Pasted%20image%2020261102095618.png)
---

## 2. Terminology: Classes

By convention, we assign numerical values to the two classes:
*   **Negative Class:** `0` (e.g., False, No, Absence)
    *   *Note:* "Negative" does NOT mean "bad". It just means the absence of the feature.
*   **Positive Class:** `1` (e.g., True, Yes, Presence)
    *   *Note:* "Positive" does NOT mean "good". It just means the presence of the feature.

---

## 3. Why Linear Regression Fails for Classification

Imagine we are trying to predict if a tumor is malignant ($y=1$) or benign ($y=0$) based on tumor size ($x$). 

If we try to use Linear Regression ($f_{w,b}(x) = wx + b$), we get a straight line. 
To make a prediction, we might set a **threshold** at $0.5$:
*   If $f_{w,b}(x) < 0.5 \rightarrow \hat{y} = 0$
*   If $f_{w,b}(x) \ge 0.5 \rightarrow \hat{y} = 1$

**The Problem:**
1.  **Skewed Data:** If there is one single extreme outlier (e.g., a massive tumor on the far right), the linear line will tilt to try and fit it. This shift will cause the threshold to move, misclassifying the normal examples.
2.  **Outputs outside 0 and 1:** A straight line will eventually go below 0 and above 1. If a prediction is $1.5$ or $-0.2$, it doesn't make sense for a classification problem.
![](../../00-Attachments/Pasted%20image%2020261102095634.png)

---

## 4. The Solution: Logistic Regression

Because linear regression doesn't work well here, we introduce a new algorithm: **Logistic Regression**.
*   Despite the name, it is used for **Classification**.
*   It ensures that the output is always between **0 and 1**.
*   The point where the model crosses the threshold ($0.5$) is called the **Decision Boundary**. 

*(We will learn exactly how Logistic Regression works in the next videos).*

![](../../00-Attachments/Pasted%20image%2020261102095645.png)
---

## 5. Quiz Practice

> [!question] Which of the following is an example of a classification task?
> A) Estimate the weight of a cat based on its height.
> B) Decide if an animal is a cat or not a cat.
> 
> **Answer:** **B**
> *Reasoning:* Deciding "cat vs. not cat" is a binary classification task (Yes/No, True/False, 1/0). Estimating weight is a regression task because weight is a continuous number.



# Logistic Regression

## Overview
To solve classification problems (where $y$ is $0$ or $1$), we cannot use standard Linear Regression because it outputs values outside the \(0\) to \(1\) range. Instead, we use **Logistic Regression**, which uses the Sigmoid function to ensure the output is always a probability between \(0\) and \(1\).

---

## 1. The Sigmoid Function

The core of logistic regression is the **Sigmoid function** (also called the logistic function). 

**Formula:**
$$ g(z) = \frac{1}{1 + e^{-z}} $$

**Key Properties:**
*   **Outputs:** Always between $0$ and $1$ ($0 < g(z) < 1$).
*   **$z = 0$:** $g(0) = \frac{1}{1 + e^0} = \frac{1}{2} = 0.5$
*   **Large positive $z$:** $e^{-z}$ approaches $0$, so $g(z)$ approaches $1$.
*   **Large negative $z$:** $e^{-z}$ becomes a huge number, so $g(z)$ approaches $0$.
![](../../00-Attachments/Pasted%20image%2020261102101135.png)
---

## 2. The Logistic Regression Model

To build our model, we take the linear equation we already know ($z = \vec{w} \cdot \vec{x} + b$) and pass it through the Sigmoid function.

**The Model:**
$$ f_{\vec{w},b}(\vec{x}) = g(\vec{w} \cdot \vec{x} + b) = \frac{1}{1 + e^{-(\vec{w} \cdot \vec{x} + b)}} $$

*   $z$ is the linear combination: $z = \vec{w} \cdot \vec{x} + b$
*   $g(z)$ is the sigmoid function.
*   The output $f_{\vec{w},b}(\vec{x})$ is the final prediction.
![](../../00-Attachments/Pasted%20image%2020261102101141.png)
---

## 3. Interpretation of the Output

In logistic regression, the output is not just a random number between 0 and 1. It represents a **probability**.

**Mathematical Notation:**
$$ f_{\vec{w},b}(\vec{x}) = P(y = 1 | \vec{x}; \vec{w},b) $$

This reads as: "The probability that $y = 1$, given the input $\vec{x}$, parameterized by $\vec{w}$ and $b$."

**Example (Tumor Classification):**
*   $y = 0$ (Not malignant)
*   $y = 1$ (Malignant)
*   If the model outputs $f_{\vec{w},b}(\vec{x}) = 0.7$, it means there is a **70% chance** that the tumor is malignant ($y=1$).

> [!info] Probability Rules
> Because there are only two possible outcomes:
> $$ P(y = 0) + P(y = 1) = 1 $$
> So, if the model predicts a 70% chance of it being malignant ($P(y=1) = 0.7$), there is a 30% chance it is not malignant ($P(y=0) = 0.3$).

![](../../00-Attachments/Pasted%20image%2020261102101154.png)
---

## 4. Quiz Practice

> [!question] What happens if $z$ is a large negative number in the sigmoid function $g(z) = \frac{1}{1+e^{-z}}$?
> 
> **Answer:** $g(z)$ is near zero.
> *Reasoning:* If $z = -100$, then $e^{-(-100)} = e^{100}$. This is a massive number, so the denominator becomes huge ($1 + \text{huge}$). Dividing \(1\) by a huge number gives a result extremely close to \(0\).

![](../../00-Attachments/Pasted%20image%2020261102101201.png)


# Threshold Selection in Classification

## Overview
By default, logistic regression uses a threshold of **0.5**. However, depending on the real-world problem, you may want to change this threshold. The threshold determines your balance between **False Positives** and **False Negatives**.

---

## 1. The Trade-off
Let's look at a tumor detection algorithm:
*   **Positive Class ($y=1$):** Has a malignant tumor.
*   **Negative Class ($y=0$):** Healthy.

When we change the threshold, we affect the types of errors the model makes:
*   **False Negative:** Model predicts $0$ (healthy), but the patient actually has a tumor. *(Very dangerous!)*
*   **False Positive:** Model predicts $1$ (tumor), but the patient is actually healthy. *(Causes anxiety and requires more tests, but not deadly).*
![](../../00-Attachments/Pasted%20image%2020261102103541.png)
---

## 2. Choosing a High Threshold (e.g., 0.9)
*   **Rule:** Predict $\hat{y}=1$ only if the model is 90% or more certain.
*   **Result:** The model becomes very "cautious" about predicting tumors.
*   **Consequence:** It will miss many actual tumors (High False Negatives). 
*   **When to use:** When False Positives are extremely costly (e.g., triggering an automatic system shutdown).
![](../../00-Attachments/Pasted%20image%2020261102103553.png)
---
![](../../00-Attachments/Pasted%20image%2020261102103624.png)![](../../00-Attachments/Pasted%20image%2020261102103605.png)
## 3. Choosing a Low Threshold (e.g., 0.2)
*   **Rule:** Predict $\hat{y}=1$ even if the model is only 20% certain.
*   **Result:** The model becomes very "sensitive" and flags almost anything suspicious.
*   **Consequence:** It will flag many healthy people as sick (High False Positives), but it will **rarely miss a tumor**.
*   **When to use:** When it is critical not to miss a positive case (e.g., Tumor detection, fraud detection, spam filtering).


> [!important] The Golden Rule of Thresholds
> **The threshold does not have to be 0.5!** 
> 
> *   If you want to avoid missing positive cases (high recall), **lower** the threshold.
> *   If you want to be very confident before predicting positive (high precision), **raise** the threshold.

> [!tip] Real-world context
> In this quiz example, the algorithm is just a *flagging tool* for a specialist to review. Even if it falsely flags 10 healthy people (False Positives), the specialist can quickly dismiss them. But if it misses 1 real tumor (False Negative), that's a life-threatening error. Therefore, you use a **low threshold**.


![](../../00-Attachments/Pasted%20image%2020261102103700.png)


# Practice Quiz: Classification with Logistic Regression

## 1. Identifying Classification Tasks
**Rule:** Classification predicts discrete categories (Yes/No, True/False, Cat/Dog). Regression predicts continuous numbers (price, weight, dosage).

*   ✅ *Classification:* Determine if a tumor is malignant or not.
*   ❌ *Regression:* Determine how much medication to prescribe (measured in milligrams).

---

## 2. The Sigmoid Function Behavior
Recall the sigmoid function: `g(z) = 1 / (1 + e^(-z))`

*   **If z is a large positive number:** `e^(-z)` approaches 0. The denominator becomes `1 + 0`. The output `g(z)` is **near one (1)**.
*   **If z is a large negative number:** `e^(-z)` becomes a huge number. The denominator becomes massive. The output `g(z)` is **near zero (0)**.
*   **If z = 0:** `e^0 = 1`. The output is `1 / (1+1) = 0.5`.

---

## 3. Predicting with Thresholds
By default, logistic regression uses a threshold of **0.5**.

*   If the model outputs `g(z) >= 0.5`, predict the positive class (e.g., "It is a cat").
*   If the model outputs `g(z) < 0.5`, predict the negative class (e.g., "It is not a cat").

*(Remember: You can change this threshold based on your specific problem, like we saw with the tumor detection example!).*

---

## 4. Decision Boundaries and Features
> [!question] True/False: No matter what features you use, the decision boundary learned by logistic regression will be linear.
> 
> **Answer: FALSE.**
> 
> **Reasoning:** 
> *   If you only use linear features (x1, x2), the boundary is a straight line.
> *   If you use **polynomial features** (x1^2, x2^2, x1*x2), the decision boundary becomes a curve (like a circle or ellipse). The logistic regression model itself is still linear in its *parameters* (w, b), but the shape of the boundary in the feature space depends entirely on the features you feed it.

![](../../00-Attachments/Pasted%20image%2020261102104156.png)

![](../../00-Attachments/Pasted%20image%2020261102104215.png)

![](../../00-Attachments/Pasted%20image%2020261102104231.png)

![](../../00-Attachments/Pasted%20image%2020261102104244.png)