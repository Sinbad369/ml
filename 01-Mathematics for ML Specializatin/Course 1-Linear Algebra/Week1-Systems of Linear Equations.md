# Linear Algebra — Week 1 Readiness Quiz

## Question 1: Word Problem to System of Equations
**Problem:**
Let $a$ = weight of an apple (g), $o$ = weight of an orange (g).
- Bag 1: 4 apples, 3 oranges = 700g
- Bag 2: 2 apples, 6 oranges = 1000g

**Solution System:**
$$
\begin{cases}
4a + 3o = 700 \\
2a + 6o = 1000
\end{cases}
$$

---

## Question 2: Matrix Form ($A\mathbf{x} = \mathbf{b}$)
**Given System:**
$$
\begin{cases}
5x + 3y + 5z = 6 \\
7x + 2y + 8z = 17 \\
4x + 3z = 8
\end{cases}
$$

**Matrix Form:**
$$
\begin{bmatrix}
5 & 3 & 5 \\
7 & 2 & 8 \\
4 & 0 & 3
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z
\end{bmatrix}
=
\begin{bmatrix}
6 \\
17 \\
8
\end{bmatrix}
$$
*(Note: $y$-coefficient in row 3 is $0$)*

---

## Question 3: Matrix Determinant
**Matrix:**
$$
A = \begin{bmatrix} 1 & 2 & 1 \\ 0 & 3 & 5 \\ 4 & 3 & 8 \end{bmatrix}
$$

**Calculation (Column 1 Expansion):**
$$
\det(A) = 1 \cdot \begin{vmatrix} 3 & 5 \\ 3 & 8 \end{vmatrix} - 0 \cdot \begin{vmatrix} 2 & 1 \\ 3 & 8 \end{vmatrix} + 4 \cdot \begin{vmatrix} 2 & 1 \\ 3 & 5 \end{vmatrix}
$$
$$
\det(A) = 1(24 - 15) + 4(10 - 3) = 9 + 4(7) = 37
$$

**Answer:** $\det(A) = 37$

---

## Question 4: Linear Dependence
**Answer:** **No**
- **Reason:** $\det(A) = 37 \neq 0$. A non-zero determinant guarantees that all rows and columns are linearly independent.

---

## Question 5: Singular vs. Non-Singular
**Answer:** **Non-singular**
- **Reason:** A matrix is non-singular if $\det(A) \neq 0$ (invertible). Since $\det(A) = 37$, it is non-singular.
## Graphical Interpretation of 2D Linear Systems

For a system of 2 linear equations with 2 variables ($Ax = b$):

| Number of Solutions | Geometric Meaning | Slopes & Intercepts | Determinant ($\det(A)$) |
| :--- | :--- | :--- | :--- |
| **One Unique Solution** | Lines intersect at **1 single point** $(x, y)$ | Different slopes | Non-zero ($\det(A) \neq 0$) |
| **No Solution** | Lines are **parallel** (never touch) | Same slope, different $y$-intercepts | Zero ($\det(A) = 0$) |
| **Infinite Solutions** | Lines **overlap completely** (same line) | Same slope, same $y$-intercept | Zero ($\det(A) = 0$) |

> **Key Takeaway:** The visual intersection point $(x, y)$ of the two graphed lines represents the exact numerical solution to the system of equations.



## Practice Quiz 1 Solutions & Visuals

### 1. Word Problem to Linear System
**Problem:** 3 X-objects + 1 Y-object = 1100g; 1 X-object + 3 Y-objects = 1050g.
**System:**
$$
\begin{cases}
3x + y = 1100 \\
x + 3y = 1050
\end{cases}
$$

---

### 2. Matrix Coefficient for Singularity
To determine the singularity of a linear system, extract the coefficient matrix $A$:
$$
\begin{cases}
2x + 3y = 15 \\
2x + 4y = 16
\end{cases}
\implies A = \begin{bmatrix} 2 & 3 \\ 2 & 4 \end{bmatrix}
$$

---

### 3. Visual Matching of Systems & Plots
- **Plot 1: Parallel Lines (No Solution)**
  $$\begin{cases} x + 3y = 4 \\ x + 3y = 3 \end{cases} \implies \text{Same slope } \left(-\frac{1}{3}\right)\text{, different intercepts}$$



---

## Practice Quiz 2 Solutions

### 1. 2x2 Determinant & Singularity
$$
A = \begin{bmatrix} 2 & 3 \\ 2 & 4 \end{bmatrix} \implies \det(A) = (2)(4) - (3)(2) = 2
$$
- Since $\det(A) = 2 \neq 0$, the matrix is **non-singular**.

---

### 2. Row Linear Independence Test
$$
M = \begin{bmatrix} 1 & 2 \\ 2 & 3 \end{bmatrix} \implies \det(M) = (1)(3) - (2)(2) = -1
$$
- Since $\det(M) = -1 \neq 0$, the rows are **Linearly Independent**.
---

## Coursera Lab Troubleshooting & Reference Guide

### 1. Download Notebook Locally
- `File` $\rightarrow$ `Save and Checkpoint`
- `File` $\rightarrow$ `Download as` $\rightarrow$ `Notebook (.ipynb)`

---

### 2. Reset / Refresh Broken Lab (Fix 404 or Corrupted Workspace)
1. Open notebook $\rightarrow$ `File` $\rightarrow$ `Open`
2. Select the `.ipynb` file $\rightarrow$ Click `Shutdown` (green icon turns gray)
3. Select file $\rightarrow$ `Rename` (e.g., `lab_v1.ipynb`)
4. Click **Help** (top right) $\rightarrow$ Click **Get latest version** $\rightarrow$ Click **Update Lab**
# Linear Algebra — Week 1 Graded Quiz Solutions
![](../../00-Attachments/Pasted%20image%2020261009225330.png)
## 1. System of Sentences to Equations
$$
\begin{cases}
5a + 10b + 10c = 5 \\
10a + 5b + 15c = 7 \\
4a + 6b + 5c = 6
\end{cases}
$$

---
![](../../00-Attachments/Pasted%20image%2020261009225347.png)
## 2. Matrix Singularity Representation
Extracted $3 \times 3$ coefficient matrix $A$:
$$
A = \begin{bmatrix} 3 & 2 & 1 \\ 1 & 1 & 2 \\ 5 & -6 & 3 \end{bmatrix}
$$

---
![](../../00-Attachments/Pasted%20image%2020261009225401.png)
## 3. 3x3 Determinant Calculation
$$
A = \begin{bmatrix} 1 & 2 & 1 \\ 2 & 1 & 1 \\ -1 & 2 & 1 \end{bmatrix} \implies \det(A) = -2
$$
- **Conclusion:** $\det(A) = -2 \neq 0 \implies$ **Non-singular**

---
![](../../00-Attachments/Pasted%20image%2020261009225420.png)
## 4. Row Linear Independence Test
$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 3 & 2 & 1 \\ 2 & 2 & 1 \end{bmatrix} \implies \det(A) = 4 \neq 0
$$
- **Conclusion:** **Linearly independent**

---
![](../../00-Attachments/Pasted%20image%2020261009225445.png)
## 5. Finding Linear Dependence Values
$$
\text{Row } 3 = \text{Row } 1 + \text{Row } 2 \implies [2+1, 1+2, 5+1] = [3, 3, 6]
$$
- **Values:** $x = 3, y = 3, z = 6$

---
![](../../00-Attachments/Pasted%20image%2020261009225500.png)
## 6. Singular Matrix Determinant
$$
A = \begin{bmatrix} 1 & 2 & 3 \\ 0 & 2 & 2 \\ 1 & 4 & 5 \end{bmatrix} \implies \det(A) = 0
$$
- **Conclusion:** $\det(A) = 0 \implies$ **Singular**

---
![](../../00-Attachments/Pasted%20image%2020261009225514.png)
## 7. Properties of Non-Singular Matrices
- Rows are **linearly independent**.
- System has **exactly one unique solution**.

---
![](../../00-Attachments/Pasted%20image%2020261009225531.png)
## 8. 2D Visual System Classifications
1. **Zero Solutions:** Parallel lines (never touch).
2. **One Solution:** Intersecting lines at 1 point.
3. **Infinitely Many Solutions:** Overlapping lines.

---
![](../../00-Attachments/Pasted%20image%2020261009225547.png)
## 9. 3D Plane System Classifications
1. **Zero Solutions:** Parallel planes (no common point).
2. **One Solution:** Planes intersect at a single point (marked with a dot).
3. **Infinitely Many Solutions:** Planes intersect along a single line axis.