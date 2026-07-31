---
icon: material/function-variant
tags: [Updating]
comments: true
---

# Mathematics

## Geometric Series


**🔷 Statement**

For ($|r| < 1$):

$$
\sum_{i=0}^{\infty} r^i = \frac{1}{1 - r}
$$

---

**🔹 Step 1: Start with a finite sum**

Let:

$$
S_n = \sum_{i=0}^{n} r^i = 1 + r + r^2 + \cdots + r^n
$$

---

**🔹 Step 2: Multiply by ($r$)**

$$
r S_n = r + r^2 + r^3 + \cdots + r^{n+1}
$$

---

**🔹 Step 3: Subtract**

$$
S_n - rS_n = (1 + r + r^2 + \cdots + r^n) - (r + r^2 + \cdots + r^{n+1})
$$

Everything cancels except:

$$
S_n - rS_n = 1 - r^{n+1}
$$

---

**🔹 Step 4: Factor**

$$
S_n(1 - r) = 1 - r^{n+1}
$$

So:

$$
S_n = \frac{1 - r^{n+1}}{1 - r}
$$

---

**🔹 Step 5: Take the limit**

If ($|r| < 1$), then ($r^{n+1} \to 0$) as ($n \to \infty$).

So:

$$
\lim_{n \to \infty} S_n = \frac{1}{1 - r}
$$

---

**🔹 Final result**

$$
\sum_{i=0}^{\infty} r^i = \frac{1}{1-r}, \quad |r|<1
$$

---