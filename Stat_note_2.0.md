# Stat 2.0

### Skewness

<img src="Photos/a.png" alt="Skewness" width="600" height="300"/>

**Coefficient of Skewness:** 

\[
\gamma_1 = \frac{\mu_3}{\mu_2^{3/2}}
\]

where  
- $(m_2)$ = second central moment (variance)  
- $(m_3)$ = third central moment  

<br>

**Interpretation of Skewness :**

| Value of Skewness | Interpretation |
|------------------|----------------|
| \(\gamma_1 = 0\) | Symmetric distribution |
| \(\gamma_1 > 0\) | Positively skewed (right-skewed) |
| \(\gamma_1 < 0\) | Negatively skewed (left-skewed) |

<br>

**Example :**

Suppose for a dataset, the central moments are given as:
- $(m_2 = 4)$
- $(m_3 = 8)$

Then the coefficient of skewness is:

\[
\gamma_3 = \frac{8}{4^{3/2}} = \frac{8}{8} = 1
\]

Since \(\gamma_ > 0\), the distribution is **positively skewed (right-skewed)**.

---

### Kurtosis

<img src="Photos/b.png" alt="Kurtosis" width="600" height="300"/>

**Coefficient of Kurtosis:**
\[
\gamma_4 = \frac{\mu_4}{\mu_2^2}
\]

where
- $(m_2)$ = second central moment (variance)
- $(m_4)$ = fourth central moment


<br>

**Interpretation of Kurtosis :**
| Value of Kurtosis | Interpretation |
|------------------|----------------|
| \(\gamma_4 = 3\) | Mesokurtic (normal distribution) |
| \(\gamma_4 > 3\) | Leptokurtic (heavytails) | |
| \(\gamma_4 < 3\) | Platykurtic (light tails) |
<br>
**Example :**
Suppose for a dataset, the central moments are given as:
- $(m_2 = 4)$
- $(m_4 = 64)$

Then the coefficient of kurtosis is:
\[
\gamma_4 = \frac{64}{4^2} = \frac{64}{16} = 4
\]
Since \(\gamma_4 > 3\), the distribution is **leptokurtic (heavy tails)**.

---

### Central moments

**Formula :**
$${m_r} = \frac{\sum f_i (x_i - \bar{x})^r}{\sum f_i}$$

where

- $(m_r)$ = r-th central moment -> 1, 2, 3, ...

---
**Relation between IQR, Range and Kurtosis :**
```html
If Range/2 = IQR then gamma4 = 3
If Range/2 > IQR then gamma4 < 3
If Range/2 < IQR then gamma4 > 3
```

**Relation between quartile and skewness :**
```html
If Q3 ~ Q2 = Q2 ~ Q1 then gamma3 = 0
If Q3 ~ Q2 > Q2 ~ Q1 then gamma3 > 0
If Q3 ~ Q2 < Q2 ~ Q1 then gamma3 < 0
```

---
