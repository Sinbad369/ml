
# Multiple Features (Multiple Linear Regression)

When predicting a target $y$ using multiple input variables (features) rather than just one, univariate linear regression expands into **Multiple Linear Regression**.
![](../../00-Attachments/Pasted%20image%2020261024182804.png)

---

## 1. Notation

| Notation | Meaning | Example from Slide |
| :--- | :--- | :--- |
| $n$ | Total number of features | $n = 4$ |
| $x_j$ | The $j^{\text{th}}$ feature (column) | $x_1 = \text{size}, x_2 = \text{bedrooms}, x_3 = \text{floors}, x_4 = \text{age}$ |
| $\vec{x}^{(i)}$ | Row vector of all features for the $i^{\text{th}}$ training example | $\vec{x}^{(2)} = [1416, 3, 2, 40]$ |
| $x_j^{(i)}$ | Value of feature $j$ in the $i^{\text{th}}$ training example | $x_3^{(2)} = 2$ |
![](../../00-Attachments/Pasted%20image%2020261024182814.png)
---

## 2. Model Formulation

### Unrolled Equation
For $n$ features, each feature $x_j$ gets its own parameter weight $w_j$, plus a single base bias parameter $b$:

$$f_{w,b}(x) = w_1 x_1 + w_2 x_2 + \dots + w_n x_n + b$$

### Vector / Dot Product Representation
Using vector notation:
- $\vec{w} = [w_1, w_2, \dots, w_n]$ (parameter vector)
- $\vec{x} = [x_1, x_2, \dots, x_n]$ (feature vector)

$$f_{\vec{w},b}(\vec{x}) = \vec{w} \cdot \vec{x} + b$$

Where $\vec{w} \cdot \vec{x}$ represents the **dot product** ($w_1 x_1 + w_2 x_2 + \dots + w_n x_n$).
![](../../00-Attachments/Pasted%20image%2020261024182829.png)
![](../../00-Attachments/Pasted%20image%2020261024182850.png)
---

## 3. In-Video Question Summary

- **Question:** What is $x_1^{(4)}$ in the training set table?
- **Answer:** **852**
- **Explanation:** $x_1^{(4)}$ refers to the 1st feature ($x_1 = \text{Size in feet}^2$) of the 4th training example ($i = 4$, row 4).
![](../../00-Attachments/Pasted%20image%2020261024182901.png)

![](../../00-Attachments/Pasted%20image%2020261024182917.png)

# Vectorization

Vectorization uses linear algebra library functions (like NumPy) to run mathematical operations in parallel on hardware (CPU/GPU) rather than sequentially through explicit Python loops.

---

# Vectorization 

## Overview
This note covers the concept of **Vectorization** in NumPy and how it drastically improves computational efficiency compared to using explicit `for` loops (unvectorized code). It also covers how vectorization applies to computing linear regression predictions and updating parameters via gradient descent.

![](../../00-Attachments/Pasted%20image%2020261024190004.png)

---

## 1. Parameters and Features (NumPy Basics)

When working with linear algebra in code (specifically NumPy), the indexing convention changes:
*   **Math Notation:** Indexing usually counts from **1** to $n$.
*   **Code Notation:** Indexing counts from **0** to $n-1$.

**Example Setup:**
Let $n = 3$ features.
*   **Weights:** $\vec{w} = [w_1, w_2, w_3]$
*   **Bias:** $b$ (a single number)
*   **Features:** $\vec{x} = [x_1, x_2, x_3]$

> [!code] NumPy Implementation
> ```python
> w = np.array([1.0, 2.5, -3.3])
> b = 4
> x = np.array([10, 20, 30])
> ```

---

## 2. Computing Predictions (Linear Regression)

The goal is to compute the prediction: $f_{\vec{w},b}(\vec{x}) = \sum_{j=1}^{n} w_jx_j + b$

### ❌ Without Vectorization
Using a `for` loop to iterate through each feature. 
*   *Note:* The mathematical summation goes from $j=1$ to $n$. In Python code, `range(0, n)` goes from $0$ to $n-1$.

> [!failure] Unvectorized Code (Inefficient)
> ```python
> f = 0
> for j in range(0, n):
>     f = f + w[j] * x[j]
> f = f + b
> ```

*Drawback:* This becomes incredibly slow when $n$ is large (e.g., $n = 100,000$).

### ✅ With Vectorization
Using the dot product to compute the prediction in a single step.

> [!success] Vectorized Code (Efficient)
> ```python
> f = np.dot(w, x) + b
> ```

**Why is it faster? (The Hardware Level)**
Without vectorization, the computer calculates one multiplication at a time. With `np.dot()`, NumPy utilizes **parallel hardware** to multiply all corresponding elements simultaneously.
*   *Without vectorization:* $t_0 \rightarrow t_1 \rightarrow t_2 \dots \rightarrow t_{15}$ (Sequential)
*   *With vectorization:* All $w_j \times x_j$ multiplications happen in parallel at $t_0$, then are summed together. 

**Takeaway:** Vectorized implementations scale efficiently to large datasets.
![](../../00-Attachments/Pasted%20image%2020261024190039.png)

![](../../00-Attachments/Pasted%20image%2020261024190050.png)
---

## 3. Gradient Descent

Vectorization is also crucial for updating parameters during gradient descent.

**The Math:**
Parameters $\vec{w} = (w_1, w_2, \dots, w_{16})$
Derivatives $\vec{d} = (d_1, d_2, \dots, d_{16})$
Learning rate $= \alpha$

The update rule for each $j$ is: $w_j = w_j - \alpha d_j$

### ❌ Without Vectorization
Updating each weight manually or via a loop.
$w_1 = w_1 - 0.1d_1$
$w_2 = w_2 - 0.1d_2$
$\dots$
$w_{16} = w_{16} - 0.1d_{16}$

> [!failure] Unvectorized Code
> ```python
> for j in range(0, 16):
>     w[j] = w[j] - 0.1 * d[j]
> ```

### ✅ With Vectorization
We can perform the subtraction on the entire arrays simultaneously:
$\vec{w} = \vec{w} - 0.1\vec{d}$

> [!success] Vectorized Code
> ```python
> w = w - 0.1 * d
> ```
NumPy handles the element-wise subtraction automatically.

![](../../00-Attachments/Pasted%20image%2020261024190114.png)
---

## 4. Quiz / Practice Questions

> [!question] Question 1
> Which of the following is a vectorized implementation for computing a linear regression model's prediction?
> 
> A) `f=0; for j in range(n): f = f + w[j] * x[j]; f=f+b`
> B) `f = np.dot(w,x) + b`
> 
> **Answer:** **B** 
> *Reasoning:* The `np.dot` function uses parallel hardware to efficiently calculate the dot product.

> [!question] Question 2
> Which of the following is considered a vectorized implementation?
> 
> A) `f = w[0] * x[0] + w[1] * x[1] + w[2] * x[2] + b`
> B) `f = 0; for j in range(n): f = f + w[j] * x[j]; f = f + b`
> C) `f = np.dot(w,x) + b`
> 
> **Answer:** **C**
> *Reasoning:* Option A is hardcoded and lacks generality, Option B is unvectorized. Option C utilizes NumPy's optimized dot product.

![](../../00-Attachments/Pasted%20image%2020261024190127.png)

# Gradient Descent for Multiple Linear Regression

## Overview
This note covers how the notation and math change when moving from a single feature to multiple features in linear regression. It also details how to implement Gradient Descent for multiple variables using vector notation, and compares it to an alternative method called the "Normal Equation."

---

## 1. Vector Notation

In previous weeks, parameters were written as individual variables. We now group them into vectors to simplify the math and code.

| Concept | Previous Notation | Vector Notation |
| :--- | :--- | :--- |
| **Parameters** | $w_1, \dots, w_n$ <br> $b$ | $\vec{w} = [w_1 \dots w_n]$ (vector of length $n$) <br> $b$ (still a single number) |
| **Model** | $f_{\vec{w},b}(\vec{x}) = w_1x_1 + \dots + w_nx_n + b$ | $f_{\vec{w},b}(\vec{x}) = \vec{w} \cdot \vec{x} + b$ <br> *(dot product)* |
| **Cost Function** | $J(w_1, \dots, w_n, b)$ | $J(\vec{w}, b)$ |
![](../../00-Attachments/Pasted%20image%2020261024195612.png)
---

## 2. Gradient Descent (Multiple Features)

The update rules for gradient descent look similar but must be applied to every weight $w_j$ (from $j=1$ to $n$) and the bias $b$.

### The Algorithm (Repeat until convergence)

**One Feature (Previous):**
$$
w = w - \alpha \frac{\partial}{\partial w} J(w,b)
$$
$$
b = b - \alpha \frac{\partial}{\partial b} J(w,b)
$$

**Multiple Features ($n \ge 2$):**
$$
w_j = w_j - \alpha \frac{\partial}{\partial w_j} J(\vec{w},b) \quad \text{for } j=1 \dots n
$$
$$
b = b - \alpha \frac{\partial}{\partial b} J(\vec{w},b)
$$

### Expanded Derivatives
When we expand the derivative term $\frac{\partial}{\partial w_j} J(\vec{w},b)$, we get the actual update formulas used in code.

**For weight $w_j$:**
$$
w_j = w_j - \alpha \frac{1}{m} \sum_{i=1}^{m} (f_{\vec{w},b}(\vec{x}^{(i)}) - y^{(i)}) x_j^{(i)}
$$

**For bias $b$:**
$$
b = b - \alpha \frac{1}{m} \sum_{i=1}^{m} (f_{\vec{w},b}(\vec{x}^{(i)}) - y^{(i)})
$$

> [!warning] Crucial Rule
> **Simultaneously update** $w_j$ (for $j=1, \dots, n$) and $b$. 
> You must calculate all the new values using the *old* values before assigning them.
![](../../00-Attachments/Pasted%20image%2020261024195620.png)
---


## 3. An Alternative to Gradient Descent: Normal Equation

There is another algorithm that can solve for $w$ and $b$ for linear regression specifically.

### The Normal Equation
*   **How it works:** It solves for $w$ and $b$ analytically **without iterations**.
*   **Limitations:** 
    *   It **only** works for linear regression.
    *   It does not generalize to other learning algorithms (like logistic regression or neural networks).
    *   It becomes very slow when the number of features is large (typically $> 10,000$).

### What you need to know for this course:
*   Some machine learning libraries might use the Normal Equation under the hood for linear regression.
*   **Gradient descent is the recommended method** for finding parameters $w$ and $b$ because it scales well to large datasets and generalizes to other algorithms (which you will learn later).
![](../../00-Attachments/Pasted%20image%2020261024195643.png)

# Multiple Linear Regression: Practice & Concepts

## 1. Understanding Notation
When dealing with multiple features, we use specific subscript and superscript notation:

*   **\(x_j^{(i)}\)**: The value of feature \(j\) in the \(i\)-th training example.
    *   **Subscript (\(j\))**: Indicates the feature index (e.g., 1 = size, 2 = bedrooms, 3 = floors, 4 = age).
    *   **Superscript (\(i\))**: Indicates the row/training example index (e.g., 1st house, 2nd house, 3rd house).

> [!example] Example from Quiz
> **Question:** What is \(x_4^{(3)}\)?
> *   Look at feature \(x_4\) ("Age of home").
> *   Look at the 3rd row (training example 3).
> *   **Answer:** 30.

---

## 2. Benefits of Vectorization
Vectorization (using functions like `np.dot` instead of `for` loops) is highly recommended in Machine Learning. 

**Potential benefits include:**
1.  **Speed:** It makes code run significantly faster.
2.  **Conciseness:** It makes code shorter and easier to read.
3.  **Hardware Utilization:** It allows code to run more easily on parallel compute hardware (like GPUs or modern CPUs with SIMD instructions).

> [!tip] Exam Tip
> If asked for the *best* option regarding benefits, **"All of the above"** is usually the correct answer for vectorization questions.

---

## 3. Gradient Descent & Learning Rate
The learning rate \(\alpha\) dictates the size of the steps taken during gradient descent.

> [!warning] Misconception
> **Myth:** Doubling the learning rate \(\alpha\) will always make gradient descent converge twice as fast.
> 
> **Fact:** **False.** 
> *   If \(\alpha\) is too small, convergence is slow.
> *   If \(\alpha\) is too large, gradient descent may overshoot the minimum and **diverge** (fail to converge entirely). 
> *   Finding a good learning rate is a tuning process, not just a matter of scaling it up linearly.

![](../../00-Attachments/Pasted%20image%2020261024203043.png)

![](../../00-Attachments/Pasted%20image%2020261024203101.png)

# Feature Scaling (Part 1)

## Overview
When we have multiple features, they can have vastly different ranges of values. This discrepancy can cause issues for Gradient Descent. This note covers why feature scaling is necessary and how it improves the shape of the cost function contour plot.

---

## 1. The Problem: Feature Size vs. Parameter Size

Imagine predicting house prices with two features:
*   **$x_1$: Size in feet²** (Range: 300 - 2,000) $\rightarrow$ **Large** values
*   **$x_2$: # Bedrooms** (Range: 0 - 5) $\rightarrow$ **Small** values

**Example:** A house with $x_1 = 2000$, $x_2 = 5$, actual price = $500k.

Let's look at the model: $\hat{price} = w_1x_1 + w_2x_2 + b$

If we choose arbitrary parameters, look at how the magnitude of the features dictates the parameters:
*   **Scenario A:** $w_1 = 50$, $w_2 = 0.1$, $b = 50$ 
    *   The $w_1$ term contributes $100,000$. The model outputs a wildly inaccurate prediction.
*   **Scenario B:** $w_1 = 0.1$, $w_2 = 50$, $b = 50$
    *   Because $x_1$ is so large, $w_1$ must be **very small**.
    *   Because $x_2$ is so small, $w_2$ must be **relatively large**.
    *   The prediction is $500k (reasonable).

**Takeaway:** When features have different scales, their corresponding parameters will also have vastly different scales.
![](../../00-Attachments/Pasted%20image%2020261024224403.png)
---

## 2. Visualizing the Cost Function

Because the parameters ($w_1$ and $w_2$) have different scales, the contour plot of the cost function $J(\vec{w}, b)$ becomes heavily skewed.

*   **Features Scatterplot:** The data looks like a flat oval (because $x_1$ goes up to 2000, while $x_2$ only goes to 5).
*   **Parameter Contour Plot:** The contours form highly elongated, skinny ellipses. The graph is stretched out because the axis for $w_1$ is very small (e.g., 0 to 1), while the axis for $w_2$ is very large (e.g., 10 to 100).
![](../../00-Attachments/Pasted%20image%2020261024224409.png)
---

## 3. Impact on Gradient Descent

> [!warning] The Problem with Unscaled Data
> If you run Gradient Descent on unscaled data, the algorithm will likely "bounce" back and forth. 
> 
> Because the contour plot is a stretched ellipse, the gradient descent path (red arrows) will zigzag heavily and take a very long time to find the global minimum.

> [!success] The Solution: Feature Scaling
> If we rescale the features so they both have a similar range (e.g., both between 0 and 1), the contour plot becomes perfectly circular.
> 
> This allows Gradient Descent to take a direct, straight path to the center (the minimum), converging much faster and more reliably.

![](../../00-Attachments/Pasted%20image%2020261024224421.png)

**Next step:** *How* do we actually scale the features? (Covered in Feature Scaling Part 2 - typically Mean Normalization or Z-score normalization).


# Feature Scaling Methods

## Overview
Feature scaling is the process of transforming features so they all fall within a similar range (typically around $-1$ to $1$). This creates a more spherical contour plot for the cost function, allowing Gradient Descent to converge much faster.

There are three main methods to achieve this.

---

## 1. Simple Scaling (Divide by Max)
The simplest method is to divide the feature by its maximum value.

**Formula:** 
$$x_{scaled} = \frac{x}{x_{max}}$$

**Example:**
*   $x_1$ (size): Range $300 \le x_1 \le 2000$
    *   $x_1 = \frac{x_1}{2000}$
    *   New range: $0.15 \le x_1 \le 1$
*   $x_2$ (bedrooms): Range $0 \le x_2 \le 5$
    *   $x_2 = \frac{x_2}{5}$
    *   New range: $0 \le x_2 \le 1$

> [!note] 
> This is exactly what the quiz question was referring to. It guarantees the new maximum is 1.

![](../../00-Attachments/Pasted%20image%2020261024230426.png)---

## 2. Mean Normalization
Instead of just dividing by the max, we subtract the mean ($\mu$) first. This centers the data around $0$. 

**Formula:**
$$x = \frac{x - \mu}{x_{max} - x_{min}}$$

**Example:**
*   $x_1$: mean $\mu_1 = 600$, max = 2000, min = 300
    *   $x_1 = \frac{x_1 - 600}{2000 - 300} = \frac{x_1 - 600}{1700}$
    *   New range: $-0.18 \le x_1 \le 0.82$
*   $x_2$: mean $\mu_2 = 2.3$, max = 5, min = 0
    *   $x_2 = \frac{x_2 - 2.3}{5 - 0}$
    *   New range: $-0.46 \le x_2 \le 0.54$

> [!tip] 
> The range doesn't have to be exactly $-1$ to $1$. It just needs to be roughly symmetric around $0$.


![](../../00-Attachments/Pasted%20image%2020261024230450.png)
---


## 3. Z-Score Normalization (Standardization)
This is the most common method. It subtracts the mean and divides by the **standard deviation** ($\sigma$). 

**Formula:**
$$x = \frac{x - \mu}{\sigma}$$

**Example:**
*   $x_1$: mean $\mu_1 = 600$, standard deviation $\sigma_1 = 450$
    *   $x_1 = \frac{x_1 - 600}{450}$
    *   New range: $-0.67 \le x_1 \le 3.1$
*   $x_2$: mean $\mu_2 = 2.3$, standard deviation $\sigma_2 = 1.4$
    *   $x_2 = \frac{x_2 - 2.3}{1.4}$
    *   New range: $-1.6 \le x_2 \le 1.9$

> [!info] 
> Standard deviation is a measure of how spread out the data is from the mean. Z-score normalization results in a distribution with a mean of $0$ and a standard deviation of $1$.

![](../../00-Attachments/Pasted%20image%2020261024230502.png)
---

## 4. When Do You Need to Rescale?

The general rule of thumb is to aim for each feature $x_j$ to be roughly in the range:
**$-1 \le x_j \le 1$**

However, it doesn't have to be perfect. Here is a guide from the course:

| Range | Action | Reasoning |
| :--- | :--- | :--- |
| $0 \le x_1 \le 3$ | **Okay, no rescaling** | Close enough to $1$. |
| $-2 \le x_2 \le 0.5$ | **Okay, no rescaling** | Close enough to $1$. |
| $-100 \le x_3 \le 100$ | **Too large $\rightarrow$ rescale** | Much larger than $1$. |
| $-0.001 \le x_4 \le 0.001$ | **Too small $\rightarrow$ rescale** | Much smaller than $1$. |
| $98.6 \le x_5 \le 105$ | **Too large $\rightarrow$ rescale** | Even though the *range* is small ($7$), the values themselves are huge. We care about the absolute numbers. |

*(Acceptable ranges are generally anywhere from $-3$ to $3$, or $-0.3$ to $0.3$, but you should definitely rescale if the max is in the 100s or the min is in the 0.001s).*

![](../../00-Attachments/Pasted%20image%2020261024230514.png)

![](../../00-Attachments/Pasted%20image%2020261024230534.png)

![](../../00-Attachments/Pasted%20image%2020261024230540.png)

# Checking Gradient Descent for Convergence

## Overview
When running gradient descent, it is crucial to monitor the **learning curve** (the plot of the cost function $J$ over iterations) to ensure the algorithm is actually working and to know when to stop training.

---

## 1. The Learning Curve

The objective of gradient descent is to minimize the cost function: 
$$ \min_{\vec{w},b} J(\vec{w},b) $$

**How to plot it:**
*   **X-axis:** Number of iterations (or epochs).
*   **Y-axis:** The value of the cost function $J(\vec{w},b)$.

> [!success] What a healthy curve looks like
> $J(\vec{w},b)$ **should decrease after every single iteration**. 
> *   At iteration 100, $J$ is lower than at iteration 0.
> *   At iteration 200, $J$ is lower than at iteration 100.
> *   Eventually, the curve will flatten out. This is when the algorithm has **likely converged** (e.g., around 400 iterations in the example). At this point, the parameters $\vec{w}, b$ are close to the global minimum.

> [!warning] What an unhealthy curve looks like
> If $J(\vec{w},b)$ **increases** after an iteration, or if it goes up and down repeatedly, it usually means one of two things:
> 1.  Your **learning rate ($\alpha$) is too large** (the algorithm is overshooting the minimum).
> 2.  There is a **bug in your code** (e.g., a typo in the derivative calculation).

---

## 2. How Many Iterations Do You Need?

There is no fixed number of iterations that works for every model. 
*   The number of iterations needed varies wildly depending on the dataset and the problem.
*   It could be **30** iterations, **1,000**, **100,000**, or even more.

Because of this, plotting the learning curve is the best way to visually find the convergence point. However, visual inspection can be tedious for automated systems.

---

## 3. Automatic Convergence Test

To automate the stopping process, we can use a mathematical threshold to declare convergence.

**The Rule:**
1.  Choose a small number, **$\epsilon$ (epsilon)**. 
    *   *A common choice is $\epsilon = 10^{-3}$ (or $0.001$).*
2.  If the cost function $J(\vec{w},b)$ **decreases by $\le \epsilon$** in one iteration, declare convergence.
3.  Stop training and output the current parameters $\vec{w}, b$.

> [!example] How it works in practice
> If the cost at iteration 400 is $0.5000$ and the cost at iteration 401 is $0.4995$, the difference is $0.0005$. 
> Since $0.0005 \le 0.001$, the algorithm automatically stops and declares convergence.

> [!tip] Debugging Tip
> If you aren't sure if gradient descent is working, always plot $J$ vs. iterations. Look for a smooth downward trend. 

![](../../00-Attachments/Pasted%20image%2020261024231300.png)


# Choosing the Learning Rate

## Overview
The learning rate (alpha) is one of the most important hyperparameters in machine learning. If it is too large, gradient descent will fail to converge (diverge). If it is too small, gradient descent will be painfully slow. This note covers how to debug and choose the right learning rate.

---

## 1. Identifying Problems with Gradient Descent

By plotting the learning curve (Cost J vs. number of iterations), you can diagnose issues:

*   **Healthy:** The curve smoothly goes down and eventually flattens out.
*   **Problem 1 (Bug or alpha too large):** The curve goes up and down (zig-zags). 
    *   *Check:* Ensure your update rule uses a **minus sign** (w_1 = w_1 - alpha * d_1). A plus sign is a common coding bug that causes divergence.
*   **Problem 2 (alpha too large):** The curve continuously goes **up**.
    *   *Fix:* Decrease alpha.
![](../../00-Attachments/Pasted%20image%2020261024232921.png)
---

## 2. Visualizing the Learning Rate

Imagine the cost function as a bowl. The goal is to reach the bottom (minimum).

> [!failure] Alpha is too big
> Gradient descent takes massive steps, constantly overshooting the minimum and bouncing from one side of the bowl to the other. It may even diverge completely (going up the sides).

> [!success] Use a smaller alpha
> With a small enough learning rate, the cost J **should decrease on every single iteration**. Gradient descent will take a smooth, direct path to the minimum.

> [!warning] If alpha is too small
> The algorithm will eventually reach the minimum, but it will take a massive number of iterations to get there. The tiny steps make the process very slow.

![](../../00-Attachments/Pasted%20image%2020261024232931.png)
---

## 3. How to Tune Alpha (Values to Try)

When trying to find a good learning rate, test a range of values by multiplying by roughly **3x** each time.

*Example sequence:*
0.001 → 0.003 → 0.01 → 0.03 → 0.1 → 0.3 → 1

**Workflow:**
1.  Start with a small value (e.g., alpha = 0.001). 
2.  If it's too slow, increase to 0.003, then 0.01, etc.
3.  Find the largest value that causes J to decrease on *every* iteration. 

*(For example, if alpha=0.3 causes the cost to increase, but alpha=0.1 decreases smoothly, then 0.1 is a good choice).*

---

## 4. Practice Question / Debugging

> [!question] Quiz Scenario
> You run gradient descent for 15 iterations with alpha = 0.3 and compute J(w). You find that the value of J(w) **increases** over time. How should you adjust alpha?
> 
> **Answer:** Try a **smaller** value of alpha (e.g., alpha = 0.1).
> 
> *Reasoning:* An increasing cost function means gradient descent is diverging. The steps are too large. We must lower the learning rate to take smaller steps so the cost decreases.

![](../../00-Attachments/Pasted%20image%2020261024232941.png)

![](../../00-Attachments/Pasted%20image%2020261024232946.png)

# Feature Engineering

## Overview
Sometimes the original features you are given aren't the most useful for predicting the target. **Feature Engineering** is the process of using your intuition about the problem to design *new* features by transforming or combining the original ones. 

This often allows the model to fit the data much better than just using raw inputs.

---

## 1. The Problem: Raw Features Aren't Always Enough
Imagine you are predicting house prices. You are given two raw features:
*   $x_1$: **Frontage** (the width of the lot)
*   $x_2$: **Depth** (how far back the lot goes)

A basic linear model would look like this:
$$f_{w,b}(x) = w_1x_1 + w_2x_2 + b$$

However, human intuition tells us that the *actual value* of a house might be highly dependent on the total land area, not just the width and depth separately.

---

## 2. Creating a New Feature
We know from basic geometry that:
$$Area = Frontage \times Depth$$

So, we can **create a new feature** $x_3$:
*   $x_3 = x_1 \times x_2$ (New feature: Area)

Now, we can update our model to use this new, more informative feature:
$$f_{w,b}(x) = w_1x_1 + w_2x_2 + w_3x_3 + b$$

The model can now learn a weight ($w_3$) specifically for the area of the house.

---

## 3. Key Takeaways
> [!tip] The Core Concept
> Feature engineering is all about **domain knowledge**. You use what you know about the real-world problem to create features that make the machine learning algorithm's job easier.

*   You are not limited to just multiplying features. You might use addition, division, squares, or even more complex transformations based on your intuition.
*   It allows linear models to capture complex, non-linear relationships (like $x_1 \times x_2$) without changing the underlying algorithm.

*(Note: In later courses, you will learn about Neural Networks, which can sometimes learn these complex features automatically. But for linear regression, manual feature engineering is a very powerful tool.)*

![](../../00-Attachments/Pasted%20image%2020261025003931.png)

# Polynomial Regression & Choice of Features

## Overview
Linear regression doesn't just have to fit straight lines. By using **Polynomial Regression**, we can fit complex, curved data by creating new features that are powers of the original feature. This is a direct application of Feature Engineering.

---

## 1. Polynomial Regression

Sometimes a straight line (linear model) underfits the data. To fit a curve, we can modify the model to include powers of the feature $x$.

Let $x$ be the size of a house, and $y$ be the price.

*   **Quadratic Model:** 
    $$f_{w,b}(x) = w_1x + w_2x^2 + b$$
    *   *Note:* This will eventually curve back down (like a parabola), which might not make sense for house prices (prices don't decrease just because a house gets too big).
*   **Cubic Model:**
    $$f_{w,b}(x) = w_1x + w_2x^2 + w_3x^3 + b$$
    *   *Note:* This will continue to go up as size increases, which is usually more realistic for prices.

### ⚠️ The Importance of Feature Scaling
When you use polynomial features, **Feature Scaling becomes absolutely critical.**

Look at the ranges:
*   $x$: size (e.g., $1$ to $1,000$)
*   $x^2$: size squared (e.g., $1$ to $1,000,000$)
*   $x^3$: size cubed (e.g., $1$ to $1,000,000,000$)

Because the ranges are vastly different, you **must** apply feature scaling (like Z-score normalization) before running gradient descent, or the algorithm will struggle to converge.

![](../../00-Attachments/Pasted%20image%2020261025004805.png)
---

## 2. Choice of Features (Other Transformations)

You are not limited to just squaring or cubing features. You can use intuition to pick any mathematical function. 

For example, if the data curves but then flattens out, a **Square Root** function might be better:
$$f_{w,b}(x) = w_1x + w_2\sqrt{x} + b$$

> [!tip] How to choose?
> Deciding *which* features to use (linear, quadratic, cubic, square root, etc.) requires plotting the data and using intuition. As the course notes, choosing the exact right features for complex data will be covered more deeply in Course 2 (Advanced Learning Algorithms / Neural Networks).


![](../../00-Attachments/Pasted%20image%2020261025004819.png)
---

## 3. Implementation with Scikit-Learn

### Why use Scikit-Learn?
In the real world, you don't usually write loops or manually create `x**2` and `x**3` arrays in raw NumPy for complex models. **Scikit-Learn** (sklearn) is the standard Python library for machine learning. It provides a clean, standardized way to apply feature scaling, create polynomial features, and train models without writing the math from scratch.

### How we use it (The Pipeline)
1.  **PolynomialFeatures:** We use this to automatically generate all polynomial combinations of the features.
2.  **StandardScaler:** We use this to normalize the massive numbers generated by exponents.
3.  **LinearRegression:** We fit the model on the scaled, engineered features.

> [!example] Scikit-Learn Implementation
> ```python
> import numpy as np
> from sklearn.preprocessing import PolynomialFeatures, StandardScaler
> from sklearn.linear_model import LinearRegression
> from sklearn.pipeline import make_pipeline
> 
> # Assume X is your original data (e.g., house sizes) and y is prices
> # X = np.array([...]).reshape(-1, 1)
> # y = np.array([...])
> 
> # Create a pipeline that:
> # 1. Generates Polynomial Features (x, x^2, x^3)
> # 2. Scales them so they are in the same range
> # 3. Fits a Linear Regression model
> model = make_pipeline(
>     PolynomialFeatures(degree=3, include_bias=False),
>     StandardScaler(),
>     LinearRegression()
> )
> 
> # Train the model
> model.fit(X, y)
> 
> # Predict
> predictions = model.predict(X_new)
> ```


# Week 2: Regression Concepts (Quiz Review)

## 1. Feature Scaling Methods
Feature scaling is used to bring all features into a similar range (typically around $-1$ to $1$).

*   **Mean Normalization** is a valid scaling step.
    *   **Formula:** $x = \frac{x - \mu}{x_{max} - x_{min}}$
    *   **Action:** You **subtract** the mean (average) from each value, and then divide by the range (max - min). 
    *   *(Note: Adding the mean instead of subtracting is incorrect).*

**When is it helpful?**
Feature scaling is particularly helpful when **one feature is much larger (or smaller) than another feature** (e.g., Size in feet² vs. Number of bedrooms). 
*   If all features already range from $0$ to $1$, scaling is not strictly necessary.

---

## 2. Identifying Learning Rate (\(\alpha\)) Issues

By plotting the learning curve (Cost \(J\) vs. Number of iterations), we can diagnose the learning rate:

*   **Healthy (\(\alpha\) is good):** The cost curve smoothly decreases and eventually flattens out (Case A).
*   **Diverging (\(\alpha\) is too large):** The cost curve increases over time. The algorithm is overshooting the minimum (Case B).

> [!tip] Rule of thumb
> If the learning curve goes UP, the learning rate is too large. Try a smaller \(\alpha\).

---

## 3. Feature Engineering
Feature Engineering is the process of using intuition to design new features by transforming or combining original features.

**Example:** Predicting grocery store revenue.
*   Given features: `items_sold`, `price_per_item`
*   **Useful Engineered Feature:** `items_sold * price_per_item` (This calculates the total revenue per product, which is highly predictive of overall store revenue).
*   *(Note: Dividing items by price is generally not as useful as multiplying them).*

---

## 4. Polynomial Regression Characteristics

> [!info] True or False?
> "With polynomial regression, the predicted values \(f_{w,b}(x)\) do not necessarily have to be a straight line (or linear) function of the input feature \(x\)."
> 
> **Answer: TRUE.**
> 
> *Reasoning:* While the *parameters* (\(w, b\)) remain linear, the *features* can be non-linear (e.g., \(x^2\), \(x^3\), \(\sqrt{x}\)). This allows the model to fit complex, curved data rather than just straight lines.


![](../../00-Attachments/Pasted%20image%2020261025010229.png)

![](../../00-Attachments/Pasted%20image%2020261025010254.png)

![](../../00-Attachments/Pasted%20image%2020261025010312.png)

![](../../00-Attachments/Pasted%20image%2020261025010327.png)