
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