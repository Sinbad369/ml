
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