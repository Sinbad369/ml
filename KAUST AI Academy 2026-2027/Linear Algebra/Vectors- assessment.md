
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