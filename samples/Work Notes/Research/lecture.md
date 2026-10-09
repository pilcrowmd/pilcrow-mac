---
course: Linear Algebra 1
lecture: 7
topic: Eigenvalues and diagonalisation
reading: Chapter 5, sections 5.1–5.3
---

# Lecture 7 – Eigenvalues and diagonalisation

> [!NOTE]
> Last week: determinants. This week we use them to find the directions a matrix only
> stretches. Next week: symmetric matrices.

## 1. Definition

Let $A$ be an $n \times n$ matrix. A number $\lambda$ is an **eigenvalue** of $A$ if there
is a non-zero vector $v$ with

$$
A v = \lambda v .
$$

The vector $v$ is an **eigenvector** for $\lambda$. Moving everything to one side gives
$(A - \lambda I)\,v = 0$, which has a non-zero solution exactly when

$$
\det(A - \lambda I) = 0 .
$$

This polynomial equation in $\lambda$ is the **characteristic equation**.

> [!TIP]
> For a matrix with two rows and two columns, the characteristic equation is always
> $\lambda^2 - (\mathrm{tr}\,A)\,\lambda + \det A = 0$. It saves time in exams.

## 2. Worked example

Take

$$
A = \begin{pmatrix} 4 & 1 \\ 2 & 3 \end{pmatrix}.
$$

Then $\mathrm{tr}\,A = 7$ and $\det A = 10$, so

$$
\lambda^2 - 7\lambda + 10 = (\lambda - 5)(\lambda - 2) = 0,
$$

and the eigenvalues are $\lambda_1 = 5$ and $\lambda_2 = 2$.

**Eigenvectors.** Solve $(A - \lambda I)v = 0$ for each eigenvalue:

$$
\begin{aligned}
\lambda_1 = 5: \quad & \begin{pmatrix} -1 & 1 \\ 2 & -2 \end{pmatrix} v = 0 \;\Rightarrow\; v_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix} \\
\lambda_2 = 2: \quad & \begin{pmatrix} 2 & 1 \\ 2 & 1 \end{pmatrix} v = 0 \;\Rightarrow\; v_2 = \begin{pmatrix} 1 \\ -2 \end{pmatrix}
\end{aligned}
$$

Check: $A v_1 = (5, 5)^T = 5 v_1$. ✓

## 3. Diagonalisation

Put the eigenvectors in the columns of $P$ and the eigenvalues on the diagonal of $D$:

$$
P = \begin{pmatrix} 1 & 1 \\ 1 & -2 \end{pmatrix}, \qquad
D = \begin{pmatrix} 5 & 0 \\ 0 & 2 \end{pmatrix}, \qquad
P^{-1} = \frac{1}{3}\begin{pmatrix} 2 & 1 \\ 1 & -1 \end{pmatrix}.
$$

Then $A = P D P^{-1}$, and powers become easy:

$$
A^n = P D^n P^{-1} = \frac{1}{3}
\begin{pmatrix}
2 \cdot 5^n + 2^n & 5^n - 2^n \\
2 \cdot 5^n - 2 \cdot 2^n & 5^n + 2 \cdot 2^n
\end{pmatrix}.
$$

| $n$ | $A^n$, top row | $A^n$, bottom row | $\mathrm{tr}\,A^n = 5^n + 2^n$ |
|:--:|:--:|:--:|--:|
| 1 | 4, 1 | 2, 3 | 7 |
| 2 | 18, 7 | 14, 11 | 29 |
| 3 | 86, 39 | 78, 47 | 133 |
| 4 | 422, 203 | 406, 219 | 641 |

> [!IMPORTANT]
> **Theorem.** An $n \times n$ matrix is diagonalisable if and only if it has $n$ linearly
> independent eigenvectors. In particular, $n$ different eigenvalues are enough.

<details>
<summary>Proof that different eigenvalues give independent eigenvectors (two vectors)</summary>

Suppose $a v_1 + b v_2 = 0$ with $\lambda_1 \neq \lambda_2$. Apply $A$:
$a \lambda_1 v_1 + b \lambda_2 v_2 = 0$. Subtract $\lambda_2$ times the first equation:
$a(\lambda_1 - \lambda_2) v_1 = 0$. Since $\lambda_1 \neq \lambda_2$ and $v_1 \neq 0$,
$a = 0$, and then $b = 0$. ∎

</details>

## 4. Application: Fibonacci numbers

The Fibonacci numbers are defined by

$$
F_n =
\begin{cases}
0 & n = 0 \\
1 & n = 1 \\
F_{n-1} + F_{n-2} & n \geq 2
\end{cases}
$$

In matrix form,

$$
\begin{pmatrix} F_{n+1} \\ F_n \end{pmatrix}
= \begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}
\begin{pmatrix} F_n \\ F_{n-1} \end{pmatrix}.
$$

The eigenvalues of this matrix are $\varphi = \frac{1+\sqrt{5}}{2}$ and
$\psi = \frac{1-\sqrt{5}}{2}$, which leads to Binet's formula:[^binet]

$$
F_n = \frac{\varphi^n - \psi^n}{\sqrt{5}} .
$$

## 5. Exercises

- [ ] Find the eigenvalues of $\begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix}$.
- [ ] Show that $\begin{pmatrix} 1 & 1 \\ 1 & 0 \end{pmatrix}$ has eigenvalues $\varphi$ and $\psi$.
- [ ] Show that the rotation $\begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$ has no real eigenvalues.
- [ ] Use the formula for $A^n$ above to compute $A^5$, and check it by multiplying.

<details>
<summary>Answers</summary>

1. $\lambda = 2$ and $\lambda = 3$ – a diagonal matrix has its eigenvalues on the diagonal.
2. $\lambda^2 - \lambda - 1 = 0$, so $\lambda = \frac{1 \pm \sqrt{5}}{2}$.
3. $\lambda^2 + 1 = 0$ has no real solution; the eigenvalues are $\pm i$.
4. $A^5 = \begin{pmatrix} 2094 & 1031 \\ 2062 & 1063 \end{pmatrix}$.

</details>

[^binet]: Named after Jacques Binet (1843), though it was known to de Moivre a century earlier.
