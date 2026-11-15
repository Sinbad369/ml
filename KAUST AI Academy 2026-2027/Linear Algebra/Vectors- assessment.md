
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
