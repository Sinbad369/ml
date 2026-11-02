
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

# Cost Function for Logistic Regression
![](../../00-Attachments/Pasted%20image%2020261102112514.png)
## Overview
In linear regression, we used the Squared Error cost function. However, for logistic regression, applying Squared Error results in a **non-convex** cost function (it looks wiggly with many local minima). If we use gradient descent on a non-convex function, it might get stuck in a local minimum instead of finding the global minimum.

To fix this, we use a new **Logistic Loss Function** that guarantees a convex (bowl-shaped) cost function.

---

## 1. The Problem with Squared Error

The Squared Error cost function looks like this:
`J(w,b) = (1/m) * sum( (1/2) * (f_wb(x) - y)^2 )`

*   **Linear Regression:** Because the model is a straight line, this creates a perfect bowl shape (**convex**). Gradient descent easily finds the bottom.
*   **Logistic Regression:** Because the model uses the non-linear Sigmoid function, plugging it into the squared error creates a **non-convex** shape. Gradient descent can get stuck on the side of a hill (a local minimum) and fail to find the true bottom.
![](../../00-Attachments/Pasted%20image%2020261102112520.png)
---

## 2. The Logistic Loss Function

To ensure the cost function remains convex, we define the loss for a single training example `(x, y)` like this:

**If the true label y = 1:**
`Loss = -log( f_wb(x) )`

**If the true label y = 0:**
`Loss = -log( 1 - f_wb(x) )`

*(Note: `log` here refers to the natural logarithm, often written as `ln`).*
![](../../00-Attachments/Pasted%20image%2020261102112528.png)

![](../../00-Attachments/Pasted%20image%2020261102112541.png)
### Why does this work?
Let's look at the graphs for these two scenarios:

> [!example] Scenario A: y = 1 (The true label is 1)
> The model predicts `f_wb(x)` (a number between 0 and 1). The loss is `-log(f_wb(x))`.
> *   If the model predicts **1** (correct): `-log(1) = 0`. The loss is zero!
> *   If the model predicts **0** (completely wrong): `-log(0)` approaches **infinity**. The model is heavily penalized.
> *   *This forces the model to output values close to 1 when the true label is 1.*

> [!example] Scenario B: y = 0 (The true label is 0)
> The loss is `-log(1 - f_wb(x))`.
> *   If the model predicts **0** (correct): `-log(1 - 0) = -log(1) = 0`. The loss is zero!
> *   If the model predicts **1** (completely wrong): `-log(1 - 1) = -log(0)` approaches **infinity**. The model is heavily penalized.
> *   *This forces the model to output values close to 0 when the true label is 0.*

**The Goal:** We want the loss to be as small as possible. The loss is lowest when the prediction `f_wb(x)` is close to the true label `y`.
![](../../00-Attachments/Pasted%20image%2020261102112558.png)
---

## 3. The Simplified Cost Function

Instead of writing an `if/else` statement, we can combine the two loss functions into a single elegant equation. 

Because `y` is always exactly either `0` or `1`, we can multiply each loss term by `y` and `(1-y)` respectively. Whichever label is false, that term becomes zero and cancels out!

**The Combined Loss:**
`Loss = -y * log( f_wb(x) ) - (1 - y) * log( 1 - f_wb(x) )`

**The Final Cost Function J(w,b):**
To get the total cost over all `m` training examples, we sum the losses and divide by `m`:

`J(w,b) = - (1/m) * sum[ y * log(f_wb(x)) + (1 - y) * log(1 - f_wb(x)) ]`

*(Note: There is no `2` in the denominator here because this function naturally has the correct derivative without needing to cancel out a 2).*

> [!important] Key Takeaway
> This new Logistic Loss function is **convex**. 
> This means when we run Gradient Descent, it will always converge to the global minimum, no matter where we initialize the parameters.

![](../../00-Attachments/Pasted%20image%2020261102112548.png)


# Simplified Cost Function for Logistic Regression

## Overview
We previously defined the logistic loss function using an "if/else" structure (one equation if y=1, and another if y=0). While this works, it's messy to write in code and math. We can combine both cases into a single, elegant equation.

---

## 1. The Combined Loss Function

Because the target label $y$ can only be exactly **1** or **0**, we can use them as mathematical switches to turn parts of the equation on and off.

**The Simplified Loss Function:**
$$ L(f_{\vec{w},b}(\vec{x}), y) = -y \log(f_{\vec{w},b}(\vec{x})) - (1 - y) \log(1 - f_{\vec{w},b}(\vec{x})) $$

### How the "Switches" Work:

> [!example] Case 1: If the true label $y = 1$
> *   The first term becomes: $-1 \cdot \log(f)$ (This stays active)
> *   The second term becomes: $-(1 - 1) \cdot \log(1-f) = -0 \cdot \log(1-f) = 0$ (This disappears entirely)
> *   **Result:** $L = -\log(f_{\vec{w},b}(\vec{x}))$

![](../../00-Attachments/Pasted%20image%2020261102114439.png)

> [!example] Case 2: If the true label $y = 0$
> *   The first term becomes: $-0 \cdot \log(f) = 0$ (This disappears entirely)
> *   The second term becomes: $-(1 - 0) \cdot \log(1-f) = -1 \cdot \log(1 - f)$ (This stays active)
> *   **Result:** $L = -\log(1 - f_{\vec{w},b}(\vec{x}))$

![](../../00-Attachments/Pasted%20image%2020261102114449.png)
---

## 2. The Simplified Cost Function

To get the total Cost Function $J(\vec{w},b)$ for the entire training set of $m$ examples, we simply sum up the losses for all examples and divide by $m$.

**The Final Equation:**
$$ J(\vec{w},b) = -\frac{1}{m} \sum_{i=1}^{m} \left[ y^{(i)} \log(f_{\vec{w},b}(\vec{x}^{(i)})) + (1 - y^{(i)}) \log(1 - f_{\vec{w},b}(\vec{x}^{(i)})) \right] $$

*(Note: I have factored out the negative sign to the front of the sum to make it look cleaner, which is standard practice in textbooks).*
![](../../00-Attachments/Pasted%20image%2020261102114513.png)
---

## 3. Why This Matters

> [!success] A Convex Landscape
> This specific cost function has a special mathematical property: it is **convex**. 
> 
> This means it looks like a single, smooth bowl. When we use Gradient Descent, it is guaranteed to find the single "global minimum" at the bottom of the bowl, regardless of where we start.

*(Note on the last screenshot: The professor mentions "Maximum Likelihood Estimation." This is a statistics concept that proves mathematically why this specific log-loss function is the "correct" one to use for logistic regression. You don't need to know the deep math behind it for this course, just that it works!)*

![](../../00-Attachments/Pasted%20image%2020261102114521.png)

# Quiz Review: Cost Function for Logistic Regression

## 1. Loss vs. Cost (Terminology)

In machine learning, these two words are often used interchangeably in casual conversation, but in this course, they have very strict definitions:

*   **Loss (L):** The error for a **single** training example.
    *   Formula: `L(f_wb(x), y)`
*   **Cost (J):** The **average** of all the losses across the entire training set of `m` examples.
    *   Formula: `J(w,b) = (1/m) * sum( Loss )`

> [!tip] Memory Trick
> Think of a grocery bill. The **loss** is the price of one single apple. The **cost** is the total bill for all the apples you bought.

![](../../00-Attachments/Pasted%20image%2020261102114902.png)
---

## 2. Simplifying the Loss Function

The combined loss function is:
`L = -y * log(f) - (1 - y) * log(1 - f)`

Because `y` can only be 0 or 1, it acts like a switch:

*   **If y = 1:** The second half `(1 - 1)` becomes 0. The expression simplifies to `-log(f)`.
*   **If y = 0:** The first half `-0 * log(f)` becomes 0. The second half `(1 - 0)` becomes 1. The expression simplifies to `-log(1 - f)`.

This is why we don't have to write an `if/else` statement in our code; the math handles it automatically!

![](../../00-Attachments/Pasted%20image%2020261102114915.png)