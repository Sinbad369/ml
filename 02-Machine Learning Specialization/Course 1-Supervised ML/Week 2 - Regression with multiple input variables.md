
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