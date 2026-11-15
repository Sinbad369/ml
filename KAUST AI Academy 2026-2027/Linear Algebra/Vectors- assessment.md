
# Linear Algebra: Vectors Assessment Review

## Question 1
**Write u = (3, -2, 5) using the standard unit vectors e₁, e₂, e₃ of ℝ³.**
*   ○ 3e₁ + 2e₂ + 5e₃
*   ● 3e₁ - 2e₂ + 5e₃
*   ○ 5e₁ - 2e₂ + 3e₃
*   ○ 6(e₁ + e₂ + e₃)

*   **Correct Answer:** 3e₁ - 2e₂ + 5e₃
*   **Rule:** A vector `(x, y, z)` is written as `x*e₁ + y*e₂ + z*e₃`.
*   **Solution:** The components are 3, -2, and 5.

---

## Question 2
**Which vector lies in the plane spanned by u = (1, 1, 0) and v = (0, 1, 1)?**
*   ● (2, 5, 3)
*   ○ (2, 3, 4)
*   ○ (1, 1, 1)
*   ○ (0, 0, 1)

*   **Correct Answer:** (2, 5, 3)
*   **Rule:** A vector `w` is in the span if `w = au + bv`. This means `a = x`, `b = z`, and `a + b = y`.
*   **Solution:** For (2, 5, 3): `a=2`, `b=3`. `2 + 3 = 5`. It works. 
*(Your previous answer (1,1,1) failed because 1 + 1 = 2, not 1).*

---

## Question 3
**Each house in a dataset is described by four features: area, bedrooms, bathrooms, and age.**
*   ○ ℝ¹⁵⁰
*   ● ℝ⁴
*   ○ ℝ¹⁶⁶
*   ○ ℝ²

*   **Correct Answer:** ℝ⁴
*   **Rule:** The dimension of the space equals the number of features.
*   **Solution:** There are 4 features, so the vector lives in 4-dimensional space.

---

## Question 4
**Let u = (1, 0, 1) and v = (0, 1, 2). Is w = (3, 1, 5) in the span of u and v?**
*   ● Yes: w = 3u + v
*   ○ Yes: w = 3u + 2v
*   ○ Yes: w = u + 3v
*   ○ No

*   **Correct Answer:** Yes: w = 3u + v
*   **Rule:** Find scalars `a` and `b` such that `a(1,0,1) + b(0,1,2) = (3,1,5)`.
*   **Solution:** `a=3`, `b=1`. Check: `3(1,0,1) + 1(0,1,2) = (3, 1, 5)`.

---

## Question 5
**Find the vector x such that x + u = v, where u = (2, -1) and v = (5, 3).**
*   ○ (3, 2)
*   ● (3, 4)
*   ○ (-3, -4)
*   ○ (7, 2)

*   **Correct Answer:** (3, 4)
*   **Rule:** `x = v - u`.
*   **Solution:** `(5, 3) - (2, -1) = (3, 4)`.

---

## Question 6
**In the RGB color model, r = (1,0,0), g = (0,1,0) and b = (0,0,1). How is a color described?**
*   ○ As the sum r + g + b...
*   ○ As one number...
*   ○ As the three vectors r, g, b multiplied entry by entry
*   ● As c₁r + c₂g + c₃b, each cᵢ the brightness of that primary

*   **Correct Answer:** As c₁r + c₂g + c₃b...
*   **Rule:** A color is a linear combination of the basis vectors.
*   **Solution:** `c₁`, `c₂`, `c₃` represent the intensity of Red, Green, and Blue.

---

## Question 7
**Let 1 be the ones vector in ℝ³ and u = (4, 0, -3). What is u + 2·1?**
*   ○ (8, 0, -6)
*   ○ (6, 2, -5)
*   ○ (6, 0, -3)
*   ● (6, 2, -1)

*   **Correct Answer:** (6, 2, -1)
*   **Rule:** The ones vector in ℝ³ is `(1, 1, 1)`.
*   **Solution:** `2 * (1, 1, 1) = (2, 2, 2)`. Then `(4, 0, -3) + (2, 2, 2) = (6, 2, -1)`.

---

## Question 8
**Two houses are described as x = (120, 3) and y = (150, 4). Which option gives y - x?**
*   ● (30, 1): house y has 30m² more area and one more bedroom
*   ○ (270, 7): the two houses together...
*   ○ (30, 1): house x has 30m² more area...
*   ○ (-30, -1): house y has...

*   **Correct Answer:** (30, 1): house y has 30m² more area and one more bedroom
*   **Rule:** Vector subtraction is component-wise.
*   **Solution:** `(150, 4) - (120, 3) = (30, 1)`.

---

## Question 9
**Why does the span of u and v always contain the origin?**
*   ○ It does not...
*   ○ Because u and v are both drawn starting from the origin
*   ○ Because u + v is always the zero vector
*   ● Because choosing c = d = 0 gives 0u + 0v = 0

*   **Correct Answer:** Because choosing c = d = 0 gives 0u + 0v = 0
*   **Rule:** The span is the set of all linear combinations. 
*   **Solution:** Setting all coefficients to zero always yields the zero vector, which is the origin.

---

## Question 10
**Let u = (1, 2, 3). Which change produces a vector that is different from u?**
*   ○ Writing the second entry as 4/2 instead of 2
*   ○ Writing the entries between parentheses instead of square brackets
*   ● Swapping the first and second entries
*   ○ Calling the vector v instead of u

*   **Correct Answer:** Swapping the first and second entries
*   **Rule:** Vectors are ordered. Changing the order changes the vector.
*   **Solution:** `(1, 2, 3)` becomes `(2, 1, 3)`, which is different.


# Linear Algebra: Span in ℝ²

## Question 11
**What is the span of u = (1, 0) and v = (1, 1) in ℝ²?**
*   ○ The parallelogram with sides u and v
*   ● All of ℝ²
*   ○ Only the vectors whose two entries are both nonnegative
*   ○ A line through the origin

---

## Rule
*   **Span:** The set of all possible linear combinations of the given vectors (`c₁u + c₂v`).
*   **Independence:** If two vectors in ℝ² are linearly independent (they do not lie on the same line), their span is the entire 2D plane (ℝ²). 
*   **Dependence:** If they are multiples of each other, their span is just a single line through the origin.

---

## Solution
1.  Look at `u = (1, 0)` and `v = (1, 1)`.
2.  Are they multiples of each other? No. (There is no single number you can multiply `u` by to get `v`).
3.  Because they point in different directions, they can combine to reach any coordinate in the 2D plane. 
4.  Therefore, the span is **All of ℝ²**.

*(Note: A "parallelogram" is not a vector space—the span extends infinitely in all directions, not just within a bounded shape!)*

# Linear Algebra: Span of a Single Vector

## Question 12
**Which vector lies in the span of u = (2, -1, 3)?**
*   ○ (4, -2, 3)
*   ○ (3, 0, 4)
*   ○ (-4, 2, 6)
*   ● (-4, 2, -6)

---

## Rule
*   **Span of one vector:** The span of a single non-zero vector is just a **line** passing through the origin. 
*   **Mathematical Condition:** A vector `v` is in the span of `u` if and only if `v = c * u` for some scalar `c`. In other words, `v` must be a **scalar multiple** of `u`. The ratios of their components must be exactly the same.

---

## Solution
We need to find which option is a multiple of `u = (2, -1, 3)`.

1.  Test the correct option: `(-4, 2, -6)`
2.  What number multiplies `2` to get `-4`? The answer is **-2**.
3.  Check if applying `-2` to the other components works:
    *   `-1 * -2 = 2` (Matches the y-component)
    *   `3 * -2 = -6` (Matches the z-component)
4.  Since `(-4, 2, -6) = -2 * (2, -1, 3)`, it lies in the span.

# Linear Algebra: Linear Combinations

## Question
**For u = (1, 2) and v = (3, -1), what is the linear combination 2u + 3v?**
*   ○ (4, 1)
*   ● (11, 1)
*   ○ (11, 7)
*   ○ (9, 4)

---

## Rule
*   **Scalar Multiplication:** Multiply each component of the vector by the scalar.
*   **Vector Addition:** Add the corresponding components (x to x, y to y) together.

---

## Solution
1.  Calculate `2u`: 
    `2 * (1, 2) = (2, 4)`
2.  Calculate `3v`: 
    `3 * (3, -1) = (9, -3)`
3.  Add them together:
    `(2, 4) + (9, -3) = (2+9, 4-3) = (11, 1)`

# Linear Algebra: Scalar Multiplication by Zero

## Question
**For u = (5, -1, 2), what is 0u?**
*   ○ The vector (5, -1, 2), unchanged
*   ○ The number 0
*   ● The zero vector (0, 0, 0)
*   ○ It is undefined, because a vector cannot be scaled by zero

---

## Rule
*   **Scalar Multiplication:** Multiplying a vector by a scalar means multiplying every individual component of the vector by that number.
*   **Zero Property:** Multiplying any vector by the scalar `0` always results in the **zero vector** (a vector where all components are `0`). 

---

## Solution
1.  Take the vector `u = (5, -1, 2)`.
2.  Multiply each component by `0`:
    `(0 * 5, 0 * -1, 0 * 2)`
3.  The result is `(0, 0, 0)`.

*(Note: The zero vector is a vector, not a scalar. The scalar `0` is just a single number, but the zero vector has the same dimension as the original vector).*

# Linear Algebra: Verifying Span

## Question
**Let u = (1, 0, 1) and v = (0, 1, 2). Is w = (3, 1, 5) in the span of u and v, and if so, how?**
*   ○ Yes: w = u + 3v
*   ○ Yes: w = 3u + 2v
*   ● Yes: w = 3u + v
*   ○ No: w is not a multiple of u or of v

---

## Rule
*   **Definition of Span:** A vector `w` is in the span of `u` and `v` if there exist scalars `a` and `b` such that `w = au + bv`.
*   **How to check:** Set up the equation `a*u + b*v = w`, break it into individual components (x, y, z), and solve for `a` and `b`.

---

## Solution
We want to find `a` and `b` such that:
`a(1, 0, 1) + b(0, 1, 2) = (3, 1, 5)`

This gives us a system of three equations:
1.  `a + 0 = 3`  →  **`a = 3`**
2.  `0 + b = 1`  →  **`b = 1`**
3.  `a + 2b = 5` →  **Check:** `3 + 2(1) = 5` (This is true!)

So, `w = 3u + 1v`, or simply **w = 3u + v**.

# Linear Algebra: Definition of Span

## Question 6
**What is the span of two vectors u and v?**
*   ○ The single vector u + v
*   ● The set of all cu + dv, for all real numbers c and d
*   ○ The set of all vectors that have the same size as u and v
*   ○ The set of all cu + dv with 0 ≤ c ≤ 1 and 0 ≤ d ≤ 1

---

## Rule
*   **Span:** The span of a set of vectors is the set of **all possible linear combinations** of those vectors.
*   **Linear Combination:** Given vectors `u` and `v`, a linear combination is `cu + dv`, where `c` and `d` are scalars (real numbers).

---

## Solution
The definition of span requires that the scalars can be **any real number**. 
*   `c` and `d` can be 5, -3, 0.5, 1000, etc.
*   If you restrict the scalars (like the last option: `0 ≤ c ≤ 1`), you only get a small bounded region, not the full infinite span (the entire plane or line).

Therefore, the correct definition is the set of **all cu + dv, for all real numbers c and d**.

# Linear Algebra: Solving for Coefficients

## Question
**Let yellow be y = r + g = (1, 1, 0) and white be w = r + g + b = (1, 1, 1). Which coefficients give αy + βw = (0.8, 0.8, 0.3)?**
*   ● α = 0.5, β = 0.3
*   ○ α = 0.5, β = 0.8
*   ○ α = 0.3, β = 0.5
*   ○ α = 0.8, β = 0.3

---

## Rule
*   To find the coefficients of a linear combination, set up a system of equations by matching the x, y, and z components of the resulting vector.
*   `α(v1) + β(v2) = target_vector`

---

## Solution
Set up the equation:
`α(1, 1, 0) + β(1, 1, 1) = (0.8, 0.8, 0.3)`

This gives three equations:
1.  `α + β = 0.8` (from the x-component)
2.  `α + β = 0.8` (from the y-component)
3.  `β = 0.3` (from the z-component)

From equation 3, we know **β = 0.3**.
Substitute β into equation 1:
`α + 0.3 = 0.8`
**α = 0.5**


# Linear Algebra: Geometric Meaning of Scalar Multiplication

## Question
**Compared with a nonzero vector u, the vector -3u is:**
*   ○ one third as long, pointing in the opposite direction
*   ● three times as long, pointing in the opposite direction
*   ○ one third as long, pointing in the same direction
*   ○ three times as long, pointing in the same direction

---

## Rule
When multiplying a vector by a scalar `c` (i.e., `cu`):
1.  **Magnitude (Length):** The length is scaled by the absolute value of the scalar (`|c|`). 
    *   If `|c| > 1`, the vector gets longer.
    *   If `0 < |c| < 1`, the vector gets shorter.
2.  **Direction:** 
    *   If `c > 0`, the vector points in the **same direction**.
    *   If `c < 0`, the vector points in the **opposite direction**.

---

## Solution
Look at the scalar: `c = -3`.
*   **Length:** `| -3 | = 3`. The vector is three times as long.
*   **Direction:** The negative sign means it points in the opposite direction.

# Linear Algebra: Dot Product and Distance

## Question 1
**A simple model predicts y = wᵀx + b. What is b?**
*   ○ The weight that multiplies the first feature
*   ● The bias term, added to the weighted sum of the features
*   ○ The predicted output of the model
*   ○ The vector of input features

---

## Rule
*   **Linear Equation:** In a linear model, `y = wᵀx + b`.
*   **wᵀx:** The dot product (weighted sum) of the feature vector `x` and weight vector `w`.
*   **b:** The **bias** (or intercept). It is a scalar value added to the weighted sum, allowing the model to shift up or down even when all features are zero.

---

## Solution
The equation is composed of two parts:
1.  `wᵀx`: The weighted sum of features.
2.  `b`: The bias term.

Therefore, `b` is the bias term added to the weighted sum.

## Question 2
**A vector u has ||u|| = 3. For which values of c is ||cu|| = 6?**
*   ● c = 2 or c = -2
*   ○ c = 4 or c = -4
*   ○ c = 1/2 or c = -1/2
*   ○ Only c = 2
---
## Rule
*   **Scalar Multiplication and Norms:** When you multiply a vector by a scalar `c`, the new length (norm) is multiplied by the absolute value of `c`.
*   **Formula:** `||cu|| = |c| * ||u||`
---
## Solution
1.  We know `||u|| = 3` and we want `||cu|| = 6`.
2.  Substitute into the formula: `|c| * 3 = 6`.
3.  Solve for `|c|`: `|c| = 2`.
4.  Since `|c| = 2`, the scalar `c` can be either **2** or **-2**. 
*(Note: A negative scalar stretches the vector by that amount but flips its direction, so the length is still positive).*


  
## Question 3
**What is the unit vector in the direction of x = (0, -5, 12)?**
*   ○ (0, 5/13, 12/13)
*   ○ (0, -5/17, 12/17)
*   ○ (0, -5/169, 12/169)
*   ● (0, -5/13, 12/13)
---
## Rule
*   **Unit Vector:** A vector with a length (magnitude) of 1. 
*   **How to find it:** Divide the vector by its magnitude (norm). 
*   **Formula:** `u = x / ||x||`
---
## Solution
1.  **Find the magnitude:** 
    `||x|| = sqrt(0^2 + (-5)^2 + 12^2)`
    `||x|| = sqrt(0 + 25 + 144)`
    `||x|| = sqrt(169) = 13`
2.  **Divide each component by the magnitude:**
    `u = (0/13, -5/13, 12/13)`
    `u = (0, -5/13, 12/13)`
*(Note: The option selected in the screenshot had 17 in the denominator, which is incorrect).*


## Question 4 - Vector Transpose
**Let u = [2, 5, -1] (as a column vector). What is uᵀ?**
*   ○ [-2 -5 1]
*   ○ [-1 5 2]
*   ● [2 5 -1] (as a row vector)
*   ○ The number 30
---
## Rule
*   **Transpose (ᵀ):** The transpose operation flips a matrix or vector over its diagonal.
*   **Column to Row:** A column vector (shape `n x 1`) becomes a row vector (shape `1 x n`) when transposed.
*   **Order:** The order of the elements does **not** change. The top element stays first, the bottom element stays last.
---
## Solution
Given the column vector:
`u = [2, 5, -1]` (written vertically)
Transposing it makes it horizontal:
`uᵀ = [2 5 -1]` (written horizontally)
*(Note: The number 30 would be the dot product `uᵀu`, not the transpose itself).*


# Linear Algebra: Norm and Scalar Multiplication

## Question 5
**A vector u has ||u|| = 4. What is ||-3u||?**
*   ○ 4
*   ○ 36
*   ● 12
*   ○ -12

---

## Rule
*   **Scaling Norms:** When you multiply a vector by a scalar `c`, the new norm (length) is multiplied by the absolute value of `c`.
*   **Formula:** `||cu|| = |c| * ||u||`
*   **Key Concept:** The norm (length) of a vector is always non-negative. It can never be negative, even if the vector points in the negative direction.

---

## Solution
1.  Identify the scalar: `c = -3`.
2.  Take the absolute value of the scalar: `|-3| = 3`.
3.  Multiply by the original norm: `3 * ||u|| = 3 * 4 = 12`.

Therefore, `||-3u|| = 12`.

## Question 6 - Dot Product of Vectors
![](../../00-Attachments/Pasted%20image%2020261116021525.png)
**For u = [-1, 4, 2] and v = [3, 1, -2], what is uᵀv?**
*   ○ 11
*   ○ 3
*   ● -3
*   ○ [-3 4 -4]

---

## Rule
*   **Dot Product (uᵀv):** Multiplying a row vector (`uᵀ`) by a column vector (`v`) results in a single scalar number.
*   **How to calculate:** Multiply the corresponding entries of each vector and sum the results.
*   **Formula:** `(u1 * v1) + (u2 * v2) + (u3 * v3)`

---

## Solution
Multiply the x, y, and z components together and add them:

1.  First component: `-1 * 3 = -3`
2.  Second component: `4 * 1 = 4`
3.  Third component: `2 * -2 = -4`

Add them up: 
`-3 + 4 + (-4) = -3`

*(Note: The last option `[-3 4 -4]` is the result of element-wise multiplication, not the dot product).*



## Question 7 - Cosine Similarity vs. Euclidean Distance
**A query q = (1, 1) is compared with candidates a = (2, 0) and b = (3, 3). Using cosine similarity, which candidate is closest in direction to q?**
*   ● b, with cosine similarity 1, against about 0.71 for a
*   ○ a, since its cosine similarity with q is the larger one
*   ○ a, since ||q - a|| is smaller than ||q - b||
*   ○ Neither; both have the same cosine similarity with q

---

## Rule
*   **Cosine Similarity:** Measures the **angle** between two vectors, ignoring their magnitude (length). It is calculated as `(u · v) / (||u|| * ||v||)`.
    *   Value of 1: Vectors point in the exact same direction.
    *   Value of 0: Vectors are perpendicular (90 degrees).
    *   Value of -1: Vectors point in exact opposite directions.
*   **Euclidean Distance (||q - a||):** Measures the straight-line distance between the tips of the vectors. It cares about both direction AND magnitude.

---

## Solution
The question specifically asks for the closest **in direction** using **cosine similarity**. This means we ignore how far apart the points are.

1.  **Compare q and b:** 
    *   `q = (1, 1)` and `b = (3, 3)`. 
    *   Vector `b` is just `3 * q`. Because they are scalar multiples, they point in the exact same direction. 
    *   Angle = 0°, **Cosine Similarity = 1**.
2.  **Compare q and a:**
    *   `q = (1, 1)` (45 degrees) and `a = (2, 0)` (0 degrees).
    *   There is a 45° angle between them.
    *   **Cosine Similarity = cos(45°) ≈ 0.71**.

*(Note: The option "a, since ||q - a|| is smaller..." is a trap. It uses Euclidean distance, which is not what the question asked for).*

### Deep Dive: Calculating the 0.71 Cosine Similarity

To understand why the similarity between `q` and `a` is 0.71, we use the cosine similarity formula:
`cos(θ) = (u · v) / (||u|| * ||v||)`

**1. Dot Product (q · a):**
`(1 * 2) + (1 * 0) = 2`

**2. Magnitude of q (||q||):**
`sqrt(1² + 1²) = sqrt(2) ≈ 1.414`

**3. Magnitude of a (||a||):**
`sqrt(2² + 0²) = sqrt(4) = 2`

**4. Calculate Cosine:**
`cos(θ) = 2 / (1.414 * 2) = 2 / 2.828 ≈ 0.71`

**Geometric Explanation:**
*   Vector `a = (2, 0)` lies flat on the x-axis (0°).
*   Vector `q = (1, 1)` goes diagonally up and right, forming a 45° angle with the x-axis.
*   The angle between them is 45°. The cosine of 45° is exactly `sqrt(2)/2`, which is approximately 0.707.

## Question 8 - Calculating the Dot Product
**For u = (2, -1, 3) and v = (4, 0, -2), what is u · v?**
*   ○ (8, 0, -6)
*   ○ -2
*   ● 2
*   ○ 14

---

## Rule
*   **Dot Product:** The dot product of two vectors of the same size results in a single scalar (a number, not a vector).
*   **Formula:** Multiply corresponding components and add the results.
    `u · v = (u1 * v1) + (u2 * v2) + (u3 * v3)`

---

## Solution
1.  Multiply the x-components: `2 * 4 = 8`
2.  Multiply the y-components: `-1 * 0 = 0`
3.  Multiply the z-components: `3 * -2 = -6`

Add them all together:
`8 + 0 + (-6) = 2`

*(Note: The option (8, 0, -6) is the element-wise multiplication, not the dot product).*

## Question 9 - Triangle Inequality for Vectors
**For which pair of nonzero vectors does ||u + v|| = ||u|| + ||v|| hold exactly?**
*   ● Vectors in the same direction, such as u and v = 2u
*   ○ None; for nonzero vectors the inequality is always strict
*   ○ Perpendicular vectors, such as u = (1, 0) and v = (0, 1)
*   ○ Vectors in opposite directions, such as u and v = -2u

---

## Rule
*   **Triangle Inequality:** For any two vectors, the length of their sum is always less than or equal to the sum of their lengths:
    `||u + v|| ≤ ||u|| + ||v||`
*   **Equality Condition:** The equality holds *exactly* (meaning `||u + v|| = ||u|| + ||v||`) only when the vectors point in the **same direction** (i.e., one is a positive scalar multiple of the other).

---

## Solution
*   If vectors point in the **same direction** (like `u` and `2u`), their lengths add up perfectly, just like walking in a straight line.
*   If vectors are **perpendicular**, they form a right triangle, and the hypotenuse (the sum) is strictly shorter than the sum of the two legs.
*   If vectors point in **opposite directions** (like `u` and `-2u`), they partially cancel each other out, making the sum shorter.
![](../../00-Attachments/Pasted%20image%2020261116022209.png)


## Question 10 - Dot Product via Angle
**Vectors u and v have ||u|| = 2, ||v|| = 3, and the angle between them is 120°. What is uᵀv?**
*   ○ 6
*   ○ -3√3
*   ○ 3
*   ● -3

---

## Rule
*   **Geometric Definition of Dot Product:** The dot product can be calculated using the magnitudes of the vectors and the angle between them.
*   **Formula:** `u · v = ||u|| * ||v|| * cos(θ)`

---

## Solution
1.  Identify the magnitudes: `||u|| = 2`, `||v|| = 3`.
2.  Identify the angle: `θ = 120°`.
3.  Recall the unit circle: `cos(120°) = -0.5`.
4.  Multiply them together:
    `u · v = 2 * 3 * (-0.5)`
    `u · v = 6 * (-0.5)`
    `u · v = -3`

*(Note: A negative dot product means the angle between the vectors is obtuse, i.e., greater than 90°).*

