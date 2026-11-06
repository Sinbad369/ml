
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

# Gradient Descent for Logistic Regression

## Overview
Now that we have the cost function for Logistic Regression, we need to find the parameters $w$ and $b$ that minimize it. We do this using **Gradient Descent**. 

The great news is that the math for gradient descent looks almost identical to Linear Regression!

![](../../00-Attachments/Pasted%20image%2020261102125406.png)

---

## 1. The Cost Function (Review)
We are trying to minimize this cost function:
`J(w,b) = -(1/m) * sum[ y * log(f_wb(x)) + (1 - y) * log(1 - f_wb(x)) ]`

To use gradient descent, we need to compute the partial derivatives of this cost function with respect to $w_j$ and $b$.

---

## 2. The Gradient Descent Algorithm

**Repeat until convergence (simultaneously update all $w_j$ and $b$):**

`w_j = w_j - alpha * (d/dw_j) J(w,b)`
`b = b - alpha * (d/db) J(w,b)`

*(Where alpha is the learning rate).*

### The Expanded Derivatives
When you do the calculus (which the course skips over, but it's surprisingly clean), the derivatives simplify to:

**For weights $w_j$ (where $j = 1 \dots n$):**
`d/dw_j J(w,b) = (1/m) * sum[ (f_wb(x) - y) * x_j ]`

**For bias $b$:**
`d/db J(w,b) = (1/m) * sum[ (f_wb(x) - y) ]`

![](../../00-Attachments/Pasted%20image%2020261102125419.png)
---

## 3. The Final Update Rules

Putting it all together, the update rules you actually code are:

> [!success] Logistic Regression Update Rules
> `w_j = w_j - alpha * (1/m) * sum[ (f_wb(x) - y) * x_j ]`
> 
> `b = b - alpha * (1/m) * sum[ (f_wb(x) - y) ]`

---

## 4. The Magic: It Looks Just Like Linear Regression!

If you look closely at the update rules above, **they are exactly the same equations** as the ones we used for Linear Regression in Week 1.

**Why?**
Even though the *model* changed (we added the sigmoid function), and the *cost function* changed (we switched to log-loss), the derivative of that new cost function happens to simplify to the exact same form.

> [!important] The Only Difference
> The only difference is what `f_wb(x)` is!
> *   **Linear Regression:** `f_wb(x) = w * x + b`
> *   **Logistic Regression:** `f_wb(x) = 1 / (1 + e^(-(w*x + b)))` (The Sigmoid function)

Because the update rules are the same, everything we learned earlier applies here:
1.  **Monitoring:** You still use a learning curve to check for convergence.
2.  **Vectorization:** You can (and should) use `np.dot()` to speed up the code.
3.  **Feature Scaling:** You should still scale your features so gradient descent converges faster.
![](../../00-Attachments/Pasted%20image%2020261102125428.png)
---

![](../../00-Attachments/Pasted%20image%2020261102125829.png)



# The Problem of Overfitting

## Overview
The goal of machine learning is **generalization**: making accurate predictions on *new, unseen* data. When a model performs well on training data but poorly on new data, it has failed to generalize. This is usually caused by either **Underfitting** or **Overfitting**.

---

## 1. The Three Scenarios (Regression Example)

Imagine predicting house prices based on size.

*   **Underfitting (High Bias):** 
    *   The model is too simple (e.g., a straight line).
    *   It does not fit the training set well.
    *   *Analogy:* "Too cold." You haven't cooked the model enough.
*   **Just Right (Generalization):**
    *   The model is balanced (e.g., a slight curve).
    *   It fits the training set pretty well and should predict new data well.
    *   *Analogy:* "Delicious." Perfectly cooked.
*   **Overfitting (High Variance):**
    *   The model is too complex (e.g., a wiggly polynomial line that hits every single data point).
    *   It fits the training set extremely well (almost zero training error), but it will perform terribly on new data because it memorized the random noise.
    *   *Analogy:* "Too hot." You overcooked it.

![](../../00-Attachments/Pasted%20image%2020261102135410.png)
---

## 2. The Three Scenarios (Classification Example)

The same concepts apply to Logistic Regression with Decision Boundaries.

*   **Underfitting:** Using only linear features (`z = w1x1 + w2x2 + b`). The decision boundary is a straight line, which is too simple to separate the classes properly.
*   **Just Right:** Using some polynomial features (like `x1^2` and `x2^2`). The decision boundary curves nicely to separate the data without being overly complicated.
*   **Overfitting:** Using many high-degree polynomial features. The decision boundary becomes a wildly wiggly shape that tries to perfectly isolate every single red 'x' and blue 'o', including the outliers. 
![](../../00-Attachments/Pasted%20image%2020261102135419.png)
---

## 3. Key Terminology

> [!info] Bias vs. Variance
> *   **High Bias** = **Underfitting**. The model has strong, incorrect assumptions (like assuming the data is a straight line).
> *   **High Variance** = **Overfitting**. The model is highly sensitive to small fluctuations in the training data (it "varies" wildly if you change the data slightly).

> [!question] Quiz Question
> When a model fits the training data well but does not work well with new examples that are not in the training set, this is an example of:
> 
> **Answer:** **Overfitting (high variance)**.
> *Reasoning:* It does not generalize well to new examples.

![](../../00-Attachments/Pasted%20image%2020261102135427.png)
---

## Next Steps
*   How do we fix overfitting? (Coming up next: Regularization).
*   How do we detect it? (Splitting data into Training and Test sets).

# Addressing Overfitting

## Overview
When a model overfits (high variance), it memorizes the training data but fails on new data. There are three main ways to fix this. 

![](../../00-Attachments/Pasted%20image%2020261106213706.png)

![](../../00-Attachments/Pasted%20image%2020261106213722.png)

![](../../00-Attachments/Pasted%20image%2020261106213733.png)

---

## 1. The Three Options

![](../../00-Attachments/Pasted%20image%2020261106213743.png)

### Option 1: Collect More Training Data
*   **How it works:** If you feed the model more data points, it becomes much harder for it to fit a highly wiggly, complex curve. The wiggles get averaged out, and the model is forced to learn a smoother, more general pattern.
*   **Limitation:** Collecting more data is often expensive, time-consuming, or simply impossible.

### Option 2: Select Features (Feature Selection)
*   **How it works:** If you have too many features (e.g., 100 features), the model might overfit. You can manually or algorithmically choose only a subset of the most relevant features and throw away the rest.
*   **Example:** When predicting house prices, maybe you drop "distance to coffee shop" and only keep "size", "bedrooms", and "age".
*   **Limitation:** You might accidentally throw away a feature that is actually useful. *(Note: The professor mentions that automated feature selection will be covered in Course 2).*

### Option 3: Regularization (The Best Method)
*   **How it works:** Instead of completely eliminating features, you keep all of them but **reduce the size of the parameters (\(w_j\))**. 
*   **Why it works:** If a model has very large weights (e.g., \(w_3 = 385\)), that feature is having a massive impact, causing the curve to wiggle wildly. By shrinking the weights to be very small (close to zero), the model becomes smoother and less prone to overfitting.

---

## 2. Visualizing Regularization

*   **Overfit Model:** The equation might look like this: 
    `f(x) = 28x - 385x^2 + 391x^3 - 174x^4 + 100` 
    *(Huge weights, very wiggly curve).*
*   **Regularized Model:** The equation looks like this:
    `f(x) = 13x - 0.23x^2 + 0.000014x^3 - 0.0001x^4 + 10`
    *(Tiny weights for the higher-order polynomials, resulting in a much smoother curve that generalizes better).*

> [!success] The Beauty of Regularization
> By keeping all the features but penalizing large weights, you get the best of both worlds: the model can still use the complex features if they are truly useful, but it won't let them dominate and cause overfitting.

---

## 3. Quiz Practice

> [!question] Applying regularization, increasing the number of training examples, or selecting a subset of the most relevant features are methods for...
> 
> **Answer:** **Addressing overfitting (high variance).**
> *Reasoning:* All three methods help the model generalize better to new examples by preventing it from memorizing the training data.

![](../../00-Attachments/Pasted%20image%2020261106213750.png)


# Cost Function with Regularization

## Overview
We previously learned that **Regularization** works by shrinking the parameters (w) so the model becomes simpler and less likely to overfit. This note explains exactly *how* we modify the cost function to force the model to learn smaller weights.

---

## 1. The Intuition

Imagine a model with polynomial features:
`f(x) = w1*x + w2*x^2 + w3*x^3 + w4*x^4 + b`

*   If the model is overfitting, it's because the higher-order terms (`w3*x^3`, `w4*x^4`) are creating wild wiggles in the curve.
*   To fix this, we want to make **w3 and w4 really small (close to 0)**. 
*   If `w3` and `w4` are close to 0, the terms `x^3` and `x^4` have almost no effect. The model essentially becomes a simpler quadratic curve (`w1*x + w2*x^2 + b`), which is less likely to overfit.

**How do we force the weights to be small?** We add a penalty to the cost function for having large weights!

![](../../00-Attachments/Pasted%20image%2020261106215231.png)
---

## 2. The New Cost Function

We take the original Mean Squared Error cost function and add a **Regularization Term** to the end.

**Formula:**
`J(w,b) = [ (1/2m) * sum( (f_wb(x) - y)^2 ) ] + [ (lambda / 2m) * sum( w^2 ) ]`

*(Note: The sum on the right includes all the weights `w`, but does NOT include the bias `b`).*

### The Lambda Parameter (λ)
*   λ (lambda) is the **Regularization Parameter**.
*   It is a number greater than 0 (λ > 0).
*   It controls the trade-off between fitting the data and keeping the weights small.
![](../../00-Attachments/Pasted%20image%2020261106215240.png)
---

## 3. The Balance (Trade-off)

The new cost function has two competing goals:

1.  **Fit the data well:** Minimizing the first term (Mean Squared Error) encourages the model to fit the training data perfectly.
2.  **Keep parameters small:** Minimizing the second term (Regularization Term) penalizes the model if the weights get too large.

**How λ changes the balance:**
*   **If λ = 0:** The regularization term disappears. You are back to standard linear regression, which might overfit.
*   **If λ is too large (e.g., 10^10):** The penalty is so massive that gradient descent will shrink all the weights to be almost zero (w1, w2, w3, w4 ≈ 0). The model just becomes `f(x) = b` (a flat horizontal line), which is **underfitting**.
*   **If λ is "just right":** It shrinks the weights just enough to smooth out the curve, giving you a model that generalizes well.

---

## 4. Why don't we regularize the bias (b)?

By convention, we only penalize the weights (w). 
Shrinking the bias (b) just shifts the entire curve up or down. It doesn't change the "wiggliness" or complexity of the curve. Therefore, there is no need to penalize it.
![](../../00-Attachments/Pasted%20image%2020261106215251.png)
---

## 5. Quiz Practice

> [!question] For a model that includes the regularization parameter λ (lambda), increasing λ will tend to...
> 
> **Answer:** **Decrease the size of parameters w1, w2, ... wn.**
> *Reasoning:* A larger penalty encourages the algorithm to shrink the weights to minimize the overall cost.

![](../../00-Attachments/Pasted%20image%2020261106215256.png)


# Regularized Linear Regression

## Overview
Now that we have added the regularization term to our cost function, we need to update our Gradient Descent algorithm to minimize this new cost. The good news is that the update rules barely change; we just add one small extra term.
![](../../00-Attachments/Pasted%20image%2020261106220905.png)

![](../../00-Attachments/Pasted%20image%2020261106220915.png)
---

## 1. The New Cost Function

We are trying to minimize:
`J(w,b) = [ (1/2m) * sum( (f_wb(x) - y)^2 ) ] + [ (lambda / 2m) * sum( w^2 ) ]`

*(Note: The first term is the Mean Squared Error. The second term is the Regularization penalty).*

---

## 2. The Gradient Descent Update Rules

To find the minimum, we take the derivative of the new cost function. Because the derivative of `w^2` is `2w`, the `2` cancels out the `2` in the denominator.

**The new update rule for weights (w_j):**
`w_j = w_j - alpha * [ (1/m) * sum( (f_wb(x) - y) * x_j ) + (lambda / m) * w_j ]`

**The new update rule for bias (b):**
`b = b - alpha * (1/m) * sum( f_wb(x) - y )`

> [!important] Crucial Detail
> Notice that the bias term `b` **does not have a regularization term** added to it. By convention, we only penalize the weights (`w`), not the bias.

![](../../00-Attachments/Pasted%20image%2020261106220924.png)
---

## 3. Understanding the "Shrinkage" Effect

The professor shows a clever way to rewrite the update rule for `w_j` to help us understand *why* regularization works.

If we factor out `w_j` from the equation, it looks like this:
`w_j = w_j * (1 - alpha * (lambda / m)) - alpha * (1/m) * sum( (f_wb(x) - y) * x_j )`

Let's break down the two parts:

1.  **The "Shrink" Part:** `w_j * (1 - alpha * (lambda / m))`
    *   Because `alpha`, `lambda`, and `m` are all positive, the term `(1 - alpha * (lambda / m))` is slightly less than 1 (e.g., 0.9998).
    *   Multiplying `w_j` by a number less than 1 makes `w_j` slightly smaller on every single iteration. This is why regularization is sometimes called **"shrinkage"**.
2.  **The "Normal Update" Part:** `- alpha * (1/m) * sum(...)`
    *   This is the standard gradient descent update we already know, which tries to fit the data.

**The Result:** Every iteration, the weight is shrunk slightly, and then updated to fit the data. The regularization term fights against the data-fitting term to keep the weights small!
![](../../00-Attachments/Pasted%20image%2020261106220932.png)
---

## 4. Quiz Practice

> [!question] Assuming alpha is a small number (0.001), lambda is 1, and m is 50, what is the effect of the new part `(1 - alpha * (lambda/m))` on updating w_j?
> 
> **Answer:** **The new part decreases the value of w_j each iteration by a little bit.**
> *Reasoning:* The calculation is `(1 - 0.001 * (1/50)) = (1 - 0.00002) = 0.99998`. Multiplying `w_j` by 0.99998 shrinks it slightly on every iteration.

![](../../00-Attachments/Pasted%20image%2020261106220937.png)
![](../../00-Attachments/Pasted%20image%2020261106220943.png)

# Regularized Logistic Regression

## Overview
Just like with Linear Regression, Logistic Regression can overfit if it has too many complex polynomial features. We fix this by adding a **Regularization Term** to the cost function. This shrinks the weights and makes the decision boundary smoother.

![](../../00-Attachments/Pasted%20image%2020261106222414.png)
---

## 1. The Regularized Cost Function

We take the standard Logistic Regression cost function (the log-loss function) and add the regularization penalty to the end.

**Formula:**
`J(w,b) = [ - (1/m) * sum( y*log(f_wb(x)) + (1-y)*log(1-f_wb(x)) ) ] + [ (lambda / 2m) * sum( w^2 ) ]`

*   The first bracket is the standard logistic loss (fits the data).
*   The second bracket is the **Regularization Term** (keeps weights small).
*   The sum for the regularization term goes from `j=1` to `n` (it does not include the bias `b`).

---

## 2. The Gradient Descent Update Rules

To train the model, we use gradient descent. We take the derivative of the new cost function.

**For the weights (w_j):**
`w_j = w_j - alpha * [ (1/m) * sum( (f_wb(x) - y) * x_j ) + (lambda / m) * w_j ]`

**For the bias (b):**
`b = b - alpha * (1/m) * sum( f_wb(x) - y )`

> [!important] The Only Difference
> If you look closely, these update rules look **exactly the same** as the regularized linear regression update rules.
> 
> The only difference is what `f_wb(x)` is:
> *   **Linear Regression:** `f_wb(x) = w*x + b`
> *   **Logistic Regression:** `f_wb(x) = 1 / (1 + e^-(w*x + b))` (The Sigmoid function)

![](../../00-Attachments/Pasted%20image%2020261106222429.png)
---

## 3. Why does this work?

In the first screenshot, you can see a highly overfit decision boundary (the wiggly purple line). It is trying too hard to separate every single red 'x' and blue 'o'.

When we minimize this new cost function:
1.  Gradient descent wants to fit the data (first term).
2.  Gradient descent wants to keep the weights (w) as small as possible (second term).

By shrinking the weights, the higher-order polynomial features (like `x^3` or `x^4`) have less impact. The decision boundary becomes smoother and simpler, which means it will generalize better to new examples.

---

## 4. Implementation Details

In the programming assignments, you will often see this coded using `scikit-learn` or raw NumPy. 

> [!tip] Scikit-Learn Tip
> If you use Scikit-Learn's `LogisticRegression`, the regularization strength is controlled by the parameter `C`. 
> *   `C` is the **inverse** of regularization strength. 
> *   A smaller `C` means stronger regularization (equivalent to a larger lambda).
> *   A larger `C` means weaker regularization (equivalent to a smaller lambda).

---

## 5. Quiz Practice

> [!question] For regularized **logistic** regression, how do the gradient descent update steps compare to the steps for linear regression?
> 
> **Answer:** **They look very similar, but the f(x) is not the same.**
> *Reasoning:* The mathematical structure of the derivatives is identical, but the prediction function `f(x)` uses the sigmoid curve for logistic regression, and a straight line for linear regression.


![](../../00-Attachments/Pasted%20image%2020261106222436.png)

# Quiz Review: The Problem of Overfitting

## 1. Methods to Address Overfitting
When a model overfits (high variance), it memorizes the training data and fails to generalize. The valid methods to fix this are:
*   **Collect more training data:** Forces the model to learn general patterns rather than memorizing noise.
*   **Apply regularization:** Shrinks the parameters to make the model simpler.
*   **Select a subset of features:** Removes irrelevant features that might be causing the model to overcomplicate itself.

*(Note: You should never just "remove a random set of training examples"—you need all the data you can get!)*
![](../../00-Attachments/Pasted%20image%2020261106222955.png)
---

## 2. Diagnosing Overfitting vs. Underfitting
Look at the decision boundary:
*   **Overfitting (High Variance):** The boundary is wildly complex and wiggly, trying to perfectly separate every single point (including outliers). 
*   **Underfitting (High Bias):** The boundary is too simple (e.g., a straight line) and fails to capture the shape of the data.

> [!tip] Does adding data help?
> *   If the model is **overfitting** (high variance), adding more data **will help** smooth out the curve and improve generalization.
> *   If the model is **underfitting** (high bias), adding more data will **not help** because the model is already too simple (you need more features or a more complex model).

![](../../00-Attachments/Pasted%20image%2020261106223015.png)
---

## 3. The Effect of Lambda (λ)
The regularization parameter λ controls the penalty for having large weights.

*   **Increase λ:** Increases the penalty. Gradient descent will shrink the parameters (w1, w2, ..., wn) to be closer to zero.
*   **Decrease λ:** Decreases the penalty. The model is allowed to have larger weights (closer to standard linear regression), which increases the risk of overfitting.

> [!warning] Remember
> Increasing the regularization parameter **reduces** the size of the parameters.

![](../../00-Attachments/Pasted%20image%2020261106223036.png)